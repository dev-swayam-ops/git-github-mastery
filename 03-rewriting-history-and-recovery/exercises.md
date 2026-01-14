# Rewriting History and Recovery - Exercises

## Exercise 1: Amend Your Last Commit
**Difficulty:** Easy

Fix a recent commit without creating a new one.

**Instructions:**
1. Create a file `notes.md` with content "First note"
2. Commit it with message "Add initial notes"
3. Realize you forgot to add more content to the file
4. Add another line: "Second note"
5. Use git amend to add this change to the last commit
6. Verify the commit message is still the same
7. Verify the file has both lines

**Expected Outcome:**
- Last commit now includes the new content
- Only one commit exists instead of two
- Commit hash changed but message remained the same

---

## Exercise 2: Reset to a Previous Commit (Soft)
**Difficulty:** Easy

Undo commits but keep changes in staging area.

**Instructions:**
1. Make 3 commits with changes to different files
2. Check your git log
3. Reset to the first commit using soft reset
4. Run `git status` to see what's staged
5. Verify all file changes are still there
6. Verify all 3 commits' changes are staged
7. Create new commits as desired or discard changes

**Expected Outcome:**
- Commits are undone
- Changes remain staged for re-committing
- Git log shows you're back at the original commit

---

## Exercise 3: Reset to a Previous Commit (Hard)
**Difficulty:** Easy

Discard all changes and move back to an older commit completely.

**Instructions:**
1. Make 2 commits with file changes
2. Note your commit hashes
3. Reset hard to the first commit
4. Verify the second commit is gone
5. Verify files from the second commit no longer exist
6. Check that your working directory is clean

**Expected Outcome:**
- All commits after the reset point are discarded
- Working directory matches the reset commit
- Changes are completely removed (not recoverable easily)

---

## Exercise 4: Revert a Commit
**Difficulty:** Medium

Safely undo a commit by creating a new commit that reverses it.

**Instructions:**
1. Create a file `important.txt` with content "Important data"
2. Commit it: "Add important data"
3. Create another file `log.txt` with content "Log entry"
4. Commit it: "Add log file"
5. Realize the "Add important data" commit shouldn't exist
6. Revert that commit using git revert
7. Verify that `important.txt` no longer exists
8. Verify `log.txt` still exists
9. Verify a new commit was created with the revert

**Expected Outcome:**
- A new commit is created that undoes the previous commit
- The original commit is still in history
- Safe for already-pushed commits

---

## Exercise 5: Cherry-Pick a Single Commit
**Difficulty:** Medium

Apply a specific commit from one branch to another without merging.

**Instructions:**
1. Create a branch `feature/bugfix`
2. On that branch, make 3 commits to different files
3. Switch to main branch
4. Use cherry-pick to apply only the second commit from bugfix branch
5. Verify that only the second commit's changes appear on main
6. Verify the other commits are not applied
7. Check the commit hash (it will be different)

**Expected Outcome:**
- Only the selected commit's changes are applied
- A new commit is created on main with the changes
- The original commit remains on feature/bugfix
- Commit hash is different (new commit)

---

## Exercise 6: Cherry-Pick Multiple Commits
**Difficulty:** Medium

Apply several specific commits from another branch.

**Instructions:**
1. Create a branch `feature/multi` with 4 commits
2. Switch to main branch
3. Cherry-pick commits 2 and 4 from the feature branch
4. Verify both commits' changes are now on main
5. Verify they appear as new commits with new hashes
6. Verify the original commits remain on feature/multi branch

**Expected Outcome:**
- Multiple commits can be cherry-picked in sequence
- Each gets a new commit hash on the destination branch
- Commits 1 and 3 are skipped as expected
- Original branch is unchanged

---

## Exercise 7: Interactive Rebase to Reorder Commits
**Difficulty:** Medium

Change the order of your commits in the current branch.

**Instructions:**
1. Make 4 commits: "Add A", "Add B", "Add C", "Add D"
2. Use interactive rebase to reorder them so they become: A, C, B, D
3. Follow the interactive rebase editor prompts
4. Save and complete the rebase
5. Verify the new commit order in git log
6. Verify all files and their content match expectations

**Expected Outcome:**
- Commits are reordered in history
- All commit hashes change (new history)
- All files have correct content
- Works only for unpushed commits

---

## Exercise 8: Interactive Rebase to Squash Commits
**Difficulty:** Medium

Combine multiple commits into one.

**Instructions:**
1. Make 4 small commits for the same feature
2. Use interactive rebase to squash all 4 into 1 commit
3. You'll be prompted for a new commit message - enter a good one
4. Verify git log now shows 1 combined commit instead of 4
5. Verify all changes from 4 commits are in the single commit

**Expected Outcome:**
- 4 commits become 1 commit with combined changes
- Final commit message describes the entire feature
- Good for cleaning up history before merging

---

## Exercise 9: Recover a Deleted Commit with Reflog
**Difficulty:** Medium

Use git reflog to find and restore a commit you accidentally deleted.

**Instructions:**
1. Create a commit: "Important feature"
2. Note the commit hash
3. Hard reset to the previous commit, deleting it
4. Realize you need that commit back
5. Use `git reflog` to find the deleted commit
6. Use `git checkout` or `git reset` to restore to that commit
7. Verify your important feature is back

**Expected Outcome:**
- Reflog shows all your recent commits
- You can find the "lost" commit by hash
- You can restore it using the commit hash
- Nothing is truly lost in git until reflog expires

---

## Exercise 10: Interactive Rebase with Multiple Operations
**Difficulty:** Medium

Combine reordering, squashing, and editing in one interactive rebase.

**Instructions:**
1. Create 5 commits with these messages:
   - "Initial setup"
   - "Add feature 1"
   - "Fix typo in feature 1"
   - "Add feature 2"
   - "Update documentation"
2. Use interactive rebase to:
   - Squash "Fix typo" into "Add feature 1"
   - Reorder so "Update documentation" is last
   - Keep other commits as-is
3. Complete the rebase with appropriate commit messages
4. Verify final history shows 4 commits in correct order

**Expected Outcome:**
- Multiple changes in one interactive rebase
- Commits are reordered and squashed as specified
- Final history is clean and logical
- All changes preserved correctly

