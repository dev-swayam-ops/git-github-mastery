# Git Branching and Merging - Solutions

## Exercise 1: Create Your First Branch - Solution

### Command:
```bash
# Check current branch
git branch

# Create new branch
git branch feature/first-branch

# List all branches
git branch
```

### Example Output:
```
$ git branch
* main

$ git branch feature/first-branch

$ git branch
  feature/first-branch
* main
```

### Explanation:
The `git branch` command without arguments lists all local branches. The asterisk (*) marks the currently active branch. `git branch <branch-name>` creates a new branch at the current commit but doesn't switch to it.

---

## Exercise 2: Switch Between Branches - Solution

### Commands:
```bash
# Create and switch to new branch in one command
git checkout -b feature/user-auth

# Or use the newer syntax
git switch -c feature/user-auth

# Create a new file
echo "// Authentication module" > auth.js
git add auth.js
git commit -m "Add authentication module"

# Switch back to main
git switch main
# or: git checkout main

# Verify file doesn't exist
ls -la auth.js  # Should show file not found on Windows: dir auth.js
```

### Example Output:
```
$ git switch -c feature/user-auth
Switched to a new branch 'feature/user-auth'

$ echo "// Authentication module" > auth.js

$ git add auth.js

$ git commit -m "Add authentication module"
[feature/user-auth a1b2c3d] Add authentication module
 1 file changed, 1 insertion(+)

$ git switch main
Switched to branch 'main'

$ ls auth.js
File not found
```

### Explanation:
`git switch` is the modern command for switching branches (replaces `git checkout`). The `-c` flag creates the branch if it doesn't exist. Each branch maintains its own working directory state, so switching branches changes which files are visible.

---

## Exercise 3: List All Branches - Solution

### Commands:
```bash
# Create three branches
git branch feature/dashboard
git branch bugfix/login-error
git branch docs/readme

# List only local branches
git branch

# List all branches (local and remote-tracking)
git branch -a

# Show current branch with more info
git branch -v

# Show branches with upstream tracking
git branch -vv
```

### Example Output:
```
$ git branch
  bugfix/login-error
  docs/readme
  feature/dashboard
  feature/user-auth
* main

$ git branch -v
  bugfix/login-error     a1b2c3d Initial commit
  docs/readme            a1b2c3d Initial commit
  feature/dashboard      a1b2c3d Initial commit
  feature/user-auth      a1b2c3d Add authentication module
* main                   a1b2c3d Initial commit
```

### Explanation:
- `git branch` shows only local branches
- `git branch -a` shows local + remote-tracking branches
- `git branch -v` shows branches with their latest commit
- `-vv` shows upstream tracking information (useful for remote repositories)

---

## Exercise 4: Fast-Forward Merge - Solution

### Commands:
```bash
# Ensure you're on main
git switch main

# Create and switch to feature branch
git switch -c feature/simple-feature

# Make first commit
echo "Feature code v1" > feature.js
git add feature.js
git commit -m "Add feature code version 1"

# Make second commit
echo "Feature code v2" >> feature.js
git add feature.js
git commit -m "Add feature code version 2"

# Switch back to main
git switch main

# Merge the feature branch
git merge feature/simple-feature

# View the merge result
git log --oneline

# Delete the feature branch
git branch -d feature/simple-feature
```

### Example Output:
```
$ git log --oneline
e4f5g6h (main) Add feature code version 2
d3e4f5g Add feature code version 1
a1b2c3d Initial commit

$ git merge feature/simple-feature
Updating a1b2c3d..e4f5g6h
Fast-forward
 feature.js | 2 +
 1 file changed, 2 insertions(+)

$ git branch -d feature/simple-feature
Deleted branch feature/simple-feature (was e4f5g6h).
```

### Explanation:
Fast-forward merge occurs when the feature branch contains all commits from main plus new ones. Git simply moves the main pointer forward to the feature branch's latest commit. The `-d` flag deletes the branch safely (fails if not fully merged).

---

## Exercise 5: Three-Way Merge - Solution

### Commands:
```bash
# Start on main
git switch main

# Create and switch to header branch
git switch -c feature/header
echo "// Header component" > header.js
git add header.js
git commit -m "Add header component"

# Switch back to main
git switch main

# Create and switch to footer branch
git switch -c feature/footer
echo "// Footer component" > footer.js
git add footer.js
git commit -m "Add footer component"

# Switch to main
git switch main

# Merge header (fast-forward)
git merge feature/header

# Merge footer (creates merge commit)
git merge feature/footer

# View the history
git log --graph --oneline --all
```

### Example Output:
```
$ git merge feature/header
Fast-forward
 header.js | 1 +
 1 file changed, 1 insertion(+)

$ git merge feature/footer
Merge made by the 'recursive' strategy.
 footer.js | 1 +
 1 file changed, 1 insertion(+)

$ git log --graph --oneline --all
*   f6g7h8i (main) Merge branch 'feature/footer'
|\
| * e5f6g7h (feature/footer) Add footer component
* | d4e5f6g (feature/header) Add header component
|/
* c3d4e5f Initial commit
```

### Explanation:
Three-way merge creates an explicit merge commit because both branches diverged from a common ancestor. The graph shows the branching structure with `*` for commits and `|` for connections.

---

## Exercise 6: Detect and Resolve Merge Conflicts - Solution

### Commands:
```bash
# Create config file on main
echo 'const API_URL = "http://localhost:3000";' > config.js
git add config.js
git commit -m "Add config with localhost"

# Create feature branch
git switch -c feature/prod-config

# Modify for production
echo 'const API_URL = "https://api.production.com";' > config.js
git add config.js
git commit -m "Update config for production"

# Switch back to main
git switch main

# Modify for staging
echo 'const API_URL = "http://staging:8000";' > config.js
git add config.js
git commit -m "Update config for staging"

# Try to merge (will conflict)
git merge feature/prod-config

# View conflict markers in the file
cat config.js

# Resolve by editing the file
echo 'const API_URL = "https://api.production.com";' > config.js

# Stage the resolved file
git add config.js

# Complete the merge
git commit -m "Merge feature/prod-config: use production URL"

# View the result
git log --oneline -n 3
```

### Example Output:
```
$ git merge feature/prod-config
Auto-merging config.js
CONFLICT (content): Merge conflict in config.js
Automatic merge failed; fix conflicts and then commit the result.

$ cat config.js
<<<<<<< HEAD
const API_URL = "http://staging:8000";
=======
const API_URL = "https://api.production.com";
>>>>>>> feature/prod-config

$ git add config.js
$ git commit -m "Merge feature/prod-config: use production URL"
[main f7g8h9i] Merge feature/prod-config: use production URL
 2 parents a1b2c3d e4f5g6h
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### Explanation:
- Conflict markers show `<<<<<<< HEAD` (current branch), `=======` (separator), and `>>>>>>> branch-name` (incoming branch)
- Resolve by choosing one version or combining both
- After editing, `git add` marks as resolved
- `git commit` completes the merge with a merge commit

---

## Exercise 7: Abort a Merge - Solution

### Commands:
```bash
# Create two branches with conflicting changes
git switch -c feature/branch-a
echo "Version A" > data.txt
git add data.txt
git commit -m "Add data version A"

git switch main
git switch -c feature/branch-b
echo "Version B" > data.txt
git add data.txt
git commit -m "Add data version B"

# Switch to branch-a
git switch feature/branch-a

# Attempt to merge branch-b (will conflict)
git merge feature/branch-b

# Abort the merge
git merge --abort

# Verify working directory is clean
git status

# Verify original content is intact
cat data.txt
```

### Example Output:
```
$ git merge feature/branch-b
Auto-merging data.txt
CONFLICT (add/add): Merge conflict in data.txt
Automatic merge failed; fix conflicts and then commit the result.

$ git merge --abort

$ git status
On branch feature/branch-a
nothing to commit, working tree clean

$ cat data.txt
Version A
```

### Explanation:
`git merge --abort` cancels the merge operation and restores your working directory to its pre-merge state. No merge commit is created. Use this if you realize merging was a mistake before you've resolved conflicts.

---

## Exercise 8: Rename a Branch - Solution

### Commands:
```bash
# Create a branch with old name
git branch feature/old-name

# Rename the branch (while on a different branch)
git branch -m feature/old-name feature/new-feature-name

# Or if you're on the branch being renamed
git branch -m feature/new-feature-name

# Verify old name is gone
git branch | grep old-name  # Should find nothing

# Verify new name exists
git branch | grep new-feature-name

# Create a properly named branch
git branch bugfix/issue-123-description
```

### Example Output:
```
$ git branch
  feature/old-name
  main

$ git branch -m feature/old-name feature/new-feature-name

$ git branch
  feature/new-feature-name
  main

$ git branch bugfix/issue-123-description
$ git branch
  bugfix/issue-123-description
  feature/new-feature-name
  main
```

### Explanation:
- `git branch -m <old-name> <new-name>` renames any branch
- `git branch -m <new-name>` renames the current branch
- Good naming: `feature/<description>`, `bugfix/<issue>`, `docs/<topic>`

---

## Exercise 9: Merge with Merge Commit - Solution

### Commands:
```bash
# Create feature branch
git switch -c feature/explicit-merge
echo "Explicit merge feature" > explicit.js
git add explicit.js
git commit -m "Add explicit merge feature"

# Switch to main
git switch main

# Merge with --no-ff flag (no fast-forward)
git merge --no-ff feature/explicit-merge

# When editor opens, enter merge commit message:
# Merge feature/explicit-merge: Description of what was merged

# View the history with graph
git log --graph --oneline --all
```

### Example Output:
```
$ git merge --no-ff feature/explicit-merge
Merge made by the 'recursive' strategy.
 explicit.js | 1 +
 1 file changed, 1 insertion(+)

$ git log --graph --oneline
*   f8g9h0i (main) Merge branch 'feature/explicit-merge'
|\
| * e7f8g9h (feature/explicit-merge) Add explicit merge feature
|/
* d6e7f8g Initial commit
```

### Explanation:
- `--no-ff` prevents fast-forward merge, always creates a merge commit
- Preserves branch history even when fast-forward is possible
- Useful for keeping branch structure visible in history
- The `|` and `\` in the graph show the branch separation

---

## Exercise 10: Compare Branches - Solution

### Commands:
```bash
# Start on main
git switch main

# Create and switch to feature branch
git switch -c feature/compare-me

# Make 2 commits
echo "Feature change 1" > file1.js
git add file1.js
git commit -m "Feature commit 1"

echo "Feature change 2" > file2.js
git add file2.js
git commit -m "Feature commit 2"

# Switch back to main
git switch main

# Make 1 commit on main
echo "Main change" > file3.js
git add file3.js
git commit -m "Main commit 1"

# Compare commits in feature that aren't in main
git log main..feature/compare-me --oneline

# Compare commits in main that aren't in feature
git log feature/compare-me..main --oneline

# Compare file differences
git diff main feature/compare-me

# Show summary of differences
git diff --stat main feature/compare-me
```

### Example Output:
```
$ git log main..feature/compare-me --oneline
e8f9g0h (feature/compare-me) Feature commit 2
d7e8f9g Feature commit 1

$ git log feature/compare-me..main --oneline
c6d7e8f (main) Main commit 1

$ git diff --stat main feature/compare-me
 file1.js | 1 +
 file2.js | 1 +
 file3.js | 1 -
 3 files changed, 2 insertions(+), 1 deletion(-)
```

### Explanation:
- `main..feature` shows commits in feature not in main
- `feature..main` shows commits in main not in feature
- `git diff` shows line-by-line changes between branches
- `--stat` shows summary of changes without details
- Use this before merging to review what will be merged

