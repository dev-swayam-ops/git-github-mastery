# Rewriting History and Recovery - Solutions

## Exercise 1: Amend Your Last Commit - Solution

### Commands:
```bash
# Create and commit initial file
echo "First note" > notes.md
git add notes.md
git commit -m "Add initial notes"

# Add more content
echo "Second note" >> notes.md

# Amend the last commit
git add notes.md
git commit --amend --no-edit

# Or with a new message
git commit --amend -m "Add initial notes with second note"

# Verify the result
git log -n 1
cat notes.md
```

### Example Output:
```
$ git commit -m "Add initial notes"
[main a1b2c3d] Add initial notes
 1 file changed, 1 insertion(+)

$ echo "Second note" >> notes.md
$ git add notes.md
$ git commit --amend --no-edit
[main e4f5g6h] Add initial notes
 1 file changed, 2 insertions(+)

$ cat notes.md
First note
Second note
```

### Explanation:
- `git commit --amend` adds staged changes to the previous commit
- `--no-edit` keeps the same message
- Without `--no-edit`, you can edit the message
- Commit hash changes because history is rewritten
- Only works for unpushed commits

---

## Exercise 2: Reset to a Previous Commit (Soft) - Solution

### Commands:
```bash
# Make 3 commits
echo "Change 1" > file1.txt
git add file1.txt
git commit -m "First commit"

echo "Change 2" > file2.txt
git add file2.txt
git commit -m "Second commit"

echo "Change 3" > file3.txt
git add file3.txt
git commit -m "Third commit"

# Check log
git log --oneline

# Soft reset to first commit
git reset --soft HEAD~2

# Check status (all changes staged)
git status

# Verify changes exist
ls *.txt
```

### Example Output:
```
$ git log --oneline
c6d7e8f (main) Third commit
b5c6d7e Second commit
a4b5c6d First commit

$ git reset --soft HEAD~2
$ git status
On branch main
Changes to be committed:
  new file:   file2.txt
  new file:   file3.txt

$ ls *.txt
file1.txt  file2.txt  file3.txt
```

### Explanation:
- `git reset --soft <commit>` moves HEAD but keeps changes staged
- Changes are ready to be re-committed
- Useful for re-organizing commits
- HEAD~2 means 2 commits back (3 commits ago in this case)

---

## Exercise 3: Reset to a Previous Commit (Hard) - Solution

### Commands:
```bash
# Make 2 commits
echo "Initial" > initial.txt
git add initial.txt
git commit -m "First commit"
FIRST_COMMIT=$(git rev-parse HEAD)

echo "Second change" > second.txt
git add second.txt
git commit -m "Second commit"

# Check log
git log --oneline

# Hard reset to first commit
git reset --hard $FIRST_COMMIT

# Verify hard reset result
git log --oneline
ls -la *.txt
```

### Example Output:
```
$ git log --oneline
b5c6d7e (main) Second commit
a4b5c6d First commit

$ git reset --hard a4b5c6d
HEAD is now at a4b5c6d First commit

$ git log --oneline
a4b5c6d (main) First commit

$ ls -la *.txt
-rw-r--r--  1 user  group  10 Jan 15 12:00 initial.txt
```

### Explanation:
- `git reset --hard` moves HEAD, index, and working directory
- All changes after the reset point are destroyed
- second.txt no longer exists
- Cannot be undone easily (but reflog can help)
- Use with caution!

---

## Exercise 4: Revert a Commit - Solution

### Commands:
```bash
# Create two commits
echo "Important data" > important.txt
git add important.txt
git commit -m "Add important data"

echo "Log entry" > log.txt
git add log.txt
git commit -m "Add log file"

# Check the commits
git log --oneline

# Revert the first commit (not the last one)
git revert <commit-hash-of-important.txt>

# Editor opens for revert commit message, save it

# Verify result
git log --oneline
ls -la *.txt
cat log.txt
```

### Example Output:
```
$ git log --oneline
b5c6d7e (main) Add log file
a4b5c6d Add important data

$ git revert a4b5c6d
[main c6d7e8f] Revert "Add important data"
 1 file changed, 1 deletion(-)

$ git log --oneline
c6d7e8f (main) Revert "Add important data"
b5c6d7e Add log file
a4b5c6d Add important data

$ ls -la *.txt
-rw-r--r--  1 user  group  10 Jan 15 12:00 log.txt
```

### Explanation:
- `git revert <commit>` creates a new commit that undoes changes
- Original commit stays in history
- Safe for already-pushed commits (history is added to, not rewritten)
- Editor opens for revert commit message
- Different from reset (which rewrites history)

---

## Exercise 5: Cherry-Pick a Single Commit - Solution

### Commands:
```bash
# Create feature branch with 3 commits
git switch -c feature/bugfix
echo "Commit 1" > file1.txt
git add file1.txt
git commit -m "First commit"

echo "Commit 2" > file2.txt
git add file2.txt
git commit -m "Second commit"

echo "Commit 3" > file3.txt
git add file3.txt
git commit -m "Third commit"

# Get the hash of the second commit
git log --oneline
CHERRY_COMMIT=$(git rev-list --all | grep -A1 "First commit" | tail -1)

# Switch to main
git switch main

# Cherry-pick only the second commit
git cherry-pick <second-commit-hash>

# Verify result
git log --oneline
ls -la file2.txt
test -f file1.txt && echo "file1 exists" || echo "file1 missing"
```

### Example Output:
```
$ git switch main
$ git cherry-pick b5c6d7e
[main d7e8f9g] Second commit
 1 file changed, 1 insertion(+)

$ git log --oneline
d7e8f9g (main) Second commit
a4b5c6d Initial commit

$ ls -la file2.txt
-rw-r--r--  1 user  group  10 Jan 15 12:00 file2.txt

$ test -f file1.txt && echo "exists" || echo "missing"
missing
```

### Explanation:
- `git cherry-pick <commit>` applies a specific commit to current branch
- Creates a new commit (different hash)
- Useful for selective commit application
- Original commit remains on source branch

---

## Exercise 6: Cherry-Pick Multiple Commits - Solution

### Commands:
```bash
# Create feature branch with 4 commits
git switch -c feature/multi
echo "A" > a.txt && git add a.txt && git commit -m "Commit A"
echo "B" > b.txt && git add b.txt && git commit -m "Commit B"
echo "C" > c.txt && git add c.txt && git commit -m "Commit C"
echo "D" > d.txt && git add d.txt && git commit -m "Commit D"

# Note commit hashes
git log --oneline

# Switch to main
git switch main

# Cherry-pick commits 2 and 4 (B and D)
git cherry-pick <commit-B-hash>
git cherry-pick <commit-D-hash>

# Verify result
git log --oneline
ls *.txt
```

### Example Output:
```
$ git log --oneline
e9f0g1h (feature/multi) Commit D
d8e9f0g Commit C
c7d8e9f Commit B
b6c7d8e Commit A
a5b6c7d Initial commit

$ git switch main
$ git cherry-pick c7d8e9f
[main f0g1h2i] Commit B
 1 file changed, 1 insertion(+)

$ git cherry-pick e9f0g1h
[main g1h2i3j] Commit D
 1 file changed, 1 insertion(+)

$ ls *.txt
b.txt  d.txt
```

### Explanation:
- Multiple cherry-picks can be done in sequence
- Each creates a new commit
- Commits A and C are not applied (as intended)
- Useful for applying selected features across branches

---

## Exercise 7: Interactive Rebase to Reorder Commits - Solution

### Commands:
```bash
# Make 4 commits
echo "A" > a.txt && git add a.txt && git commit -m "Add A"
echo "B" > b.txt && git add b.txt && git commit -m "Add B"
echo "C" > c.txt && git add c.txt && git commit -m "Add C"
echo "D" > d.txt && git add d.txt && git commit -m "Add D"

# Check current order
git log --oneline

# Start interactive rebase
git rebase -i HEAD~3

# In the editor, reorder the lines to:
# pick c7d8e9f Add A
# pick b6c7d8e Add C
# pick a5b6c7d Add B
# pick <last> Add D

# Save and exit editor
# Git will reapply commits in new order

# Verify new order
git log --oneline
```

### Example Output:
```
$ git rebase -i HEAD~3
# Editor opens with:
# pick c7d8e9f Add A
# pick b6c7d8e Add B
# pick a5b6c7d Add C
# pick <hash> Add D

# After reordering and saving:
[detached HEAD e0f1g2h] Add C
 1 file changed, 1 insertion(+)
[detached HEAD f1g2h3i] Add B
 1 file changed, 1 insertion(+)
[main g2h3i4j] Add D
 3 files changed, 3 insertions(+)

$ git log --oneline
g2h3i4j (main) Add D
f1g2h3i Add B
e0f1g2h Add C
d0e1f2g Add A
```

### Explanation:
- `git rebase -i HEAD~3` opens editor for last 3 commits
- Reorder lines to change commit order
- Git reapplies commits in new order
- All commit hashes change
- Only works for unpushed commits

---

## Exercise 8: Interactive Rebase to Squash Commits - Solution

### Commands:
```bash
# Make 4 related commits
echo "Step 1" > feature.txt && git add feature.txt && git commit -m "Add feature step 1"
echo "Step 2" >> feature.txt && git add feature.txt && git commit -m "Add feature step 2"
echo "Step 3" >> feature.txt && git add feature.txt && git commit -m "Add feature step 3"
echo "Step 4" >> feature.txt && git add feature.txt && git commit -m "Add feature step 4"

# Check log
git log --oneline

# Interactive rebase to squash
git rebase -i HEAD~3

# In editor, change commits 2-4 from "pick" to "squash"
# pick <hash1> Add feature step 1
# squash <hash2> Add feature step 2
# squash <hash3> Add feature step 3
# squash <hash4> Add feature step 4

# Save, then in next editor enter new combined message:
# Add complete feature with all steps

# Verify result
git log --oneline
cat feature.txt
```

### Example Output:
```
$ git log --oneline
d0e1f2g (main) Add feature step 4
c0d1e2f Add feature step 3
b0c1d2e Add feature step 2
a0b1c2d Add feature step 1

$ git rebase -i HEAD~3
# After editing to squash and saving:
[main e1f2g3h] Add complete feature with all steps
 1 file changed, 4 insertions(+)

$ git log --oneline
e1f2g3h (main) Add complete feature with all steps
a0b1c2d Add feature step 1

$ cat feature.txt
Step 1
Step 2
Step 3
Step 4
```

### Explanation:
- Use `squash` command in interactive rebase to combine commits
- First commit keeps its message (by default)
- Subsequent commits' messages are shown for editing
- Result is 1 commit with combined changes
- Great for cleaning up before PR merge

---

## Exercise 9: Recover a Deleted Commit with Reflog - Solution

### Commands:
```bash
# Create a commit
echo "Important" > important.txt
git add important.txt
git commit -m "Important feature"

# Note the commit hash
LOST_HASH=$(git rev-parse HEAD)
echo "Commit hash: $LOST_HASH"

# Hard reset, deleting the commit
git reset --hard HEAD~1

# Oops! Need that commit back
# Use reflog to find it
git reflog

# Restore using the commit hash from reflog
git reset --hard $LOST_HASH

# Or use the reflog directly
git reset --hard HEAD@{1}  # Go to previous HEAD position

# Verify restoration
git log --oneline
cat important.txt
```

### Example Output:
```
$ git reflog
a1b2c3d (HEAD -> main) HEAD@{0}: reset: moving to HEAD~1
e4f5g6h HEAD@{1}: commit: Important feature
d3e4f5g HEAD@{2}: commit: Initial commit

$ git reset --hard e4f5g6h
HEAD is now at e4f5g6h Important feature

$ git log --oneline
e4f5g6h (main) Important feature
d3e4f5g Initial commit

$ cat important.txt
Important
```

### Explanation:
- `git reflog` shows your recent HEAD movements
- Lists even commits that appear deleted
- Reflog entries expire after ~90 days (configurable)
- Safe way to recover "lost" commits
- No data is truly deleted until reflog expires

---

## Exercise 10: Interactive Rebase with Multiple Operations - Solution

### Commands:
```bash
# Create 5 commits
echo "Setup" > setup.txt && git add setup.txt && git commit -m "Initial setup"
echo "Feature 1" > feature1.txt && git add feature1.txt && git commit -m "Add feature 1"
echo "Fixed typo" > feature1.txt && git add feature1.txt && git commit -m "Fix typo in feature 1"
echo "Feature 2" > feature2.txt && git add feature2.txt && git commit -m "Add feature 2"
echo "Docs updated" > README.md && git add README.md && git commit -m "Update documentation"

# Check log
git log --oneline

# Interactive rebase for all 5 commits
git rebase -i HEAD~4

# In editor, configure:
# pick <h1> Initial setup
# pick <h2> Add feature 1
# squash <h3> Fix typo in feature 1
# pick <h4> Add feature 2
# pick <h5> Update documentation

# Save, edit commit message for squash
# Result: 4 commits in order

# Verify final state
git log --oneline
```

### Example Output:
```
$ git log --oneline
e5f6g7h (main) Update documentation
d4e5f6g Add feature 2
c3d4e5f Fix typo in feature 1
b2c3d4e Add feature 1
a1b2c3d Initial setup

$ git rebase -i HEAD~4
# After configuring rebase operations:
[main f6g7h8i] Add feature 1
 1 file changed, 1 insertion(+)
[main g7h8i9j] Add feature 2
 1 file changed, 1 insertion(+)
[main h8i9j0k] Update documentation
 1 file changed, 1 insertion(+)

$ git log --oneline
h8i9j0k (main) Update documentation
g7h8i9j Add feature 2
f6g7h8i Add feature 1
a1b2c3d Initial setup
```

### Explanation:
- Interactive rebase supports multiple operations at once
- Reorder, squash, reword all in one rebase session
- Each operation is applied in sequence
- All new commits get new hashes
- Powerful tool for history cleanup

