# Git Branching and Merging - Quiz

## Multiple Choice Questions (7 Questions)

**Question 1:** What command creates a new branch called `feature/login`?
- A) `git new-branch feature/login`
- B) `git branch feature/login`
- C) `git create feature/login`
- D) `git checkout feature/login`

**Correct Answer:** B

**Explanation:** `git branch <branch-name>` creates a new branch. The other options are not valid Git commands.

---

**Question 2:** What is the difference between `git switch -c feature/new` and `git branch feature/new`?
- A) They are identical
- B) `-c` creates the branch and doesn't switch to it
- C) `-c` creates the branch and switches to it immediately
- D) `git switch` cannot create branches

**Correct Answer:** C

**Explanation:** `git switch -c` creates and automatically switches to the branch. `git branch` only creates the branch without switching.

---

**Question 3:** When does a fast-forward merge occur?
- A) When two branches have no common commits
- B) When the feature branch contains all commits from main plus new ones
- C) When merging main into a feature branch
- D) When there are merge conflicts

**Correct Answer:** B

**Explanation:** Fast-forward happens when the target branch can simply move forward to the feature branch's commit without creating a merge commit.

---

**Question 4:** What do conflict markers `<<<<<<< HEAD` and `>>>>>>> branch-name` indicate?
- A) A successful merge
- B) That the merge has been automatically resolved
- C) The boundaries of conflicting changes that need manual resolution
- D) That the branch is ready to be deleted

**Correct Answer:** C

**Explanation:** These markers show where Git couldn't automatically merge changes. The section between `<<<<<<<` and `=======` is your current code, and between `=======` and `>>>>>>>` is the incoming code.

---

**Question 5:** How do you cancel a merge that's in progress?
- A) `git reset --hard HEAD`
- B) `git merge --cancel`
- C) `git merge --abort`
- D) `git branch -delete-merge`

**Correct Answer:** C

**Explanation:** `git merge --abort` safely cancels a merge and restores your working directory to its pre-merge state.

---

**Question 6:** What does `git log main..feature/branch` show?
- A) All commits in both main and feature/branch
- B) Commits that are in feature/branch but not in main
- C) Commits that are in main but not in feature/branch
- D) The last commit from each branch

**Correct Answer:** B

**Explanation:** The syntax `branch1..branch2` shows commits in branch2 that are not in branch1. Useful for seeing what would be merged.

---

**Question 7:** What is the purpose of the `--no-ff` flag in `git merge --no-ff feature/branch`?
- A) No flag is needed, it's the default behavior
- B) Prevents the merge from completing
- C) Creates a merge commit even if fast-forward is possible
- D) Skips conflict detection

**Correct Answer:** C

**Explanation:** `--no-ff` ensures a merge commit is created, preserving the branch structure in history even when fast-forward would be possible.

---

## Short Answer Questions (3 Questions)

**Question 8:** Explain the steps you would take to resolve a merge conflict in a file named `config.js`.

**Suggested Answer:**
1. Open `config.js` and locate the conflict markers (`<<<<<<`, `=======`, `>>>>>>>`)
2. Review the changes from both sides (HEAD and the branch being merged)
3. Edit the file to keep the correct version or combine both changes
4. Remove the conflict markers
5. Run `git add config.js` to mark the file as resolved
6. Run `git commit -m "message"` to complete the merge

**Scoring:** Full points for mentioning editing, resolving markers, git add, and git commit. Partial credit for incomplete steps.

---

**Question 9:** You have a feature branch that's 5 commits ahead of main, but main has 2 new commits that your branch doesn't have. How would you update your feature branch with the latest changes from main? List the steps.

**Suggested Answer:**
Option 1 (Merge):
1. `git switch feature/branch`
2. `git merge main`
3. Resolve any conflicts if they occur
4. Commit the merge

Option 2 (Rebase):
1. `git switch feature/branch`
2. `git rebase main`
3. Resolve any conflicts if they occur
4. Continue with `git rebase --continue`

**Scoring:** Full points for either complete approach. Merge is simpler for beginners, rebase gives cleaner history.

---

**Question 10:** Describe the difference between deleting a branch with `-d` flag versus `-D` flag. When would you use each one?

**Suggested Answer:**
- `-d` (delete): Safely deletes a branch only if it has been fully merged. It prevents accidental data loss.
- `-D` (force delete): Forces deletion of a branch regardless of merge status. Use only when you're certain you want to discard unmerged commits.

Example:
```bash
git branch -d feature/complete  # Safe, requires merged status
git branch -D feature/abandoned  # Force, even if unmerged
```

**Scoring:** Full points for explaining both flags and when to use them. Partial credit for just describing the difference.

---

## Answer Key Summary

| Question | Answer | Type |
|----------|--------|------|
| 1 | B | Multiple Choice |
| 2 | C | Multiple Choice |
| 3 | B | Multiple Choice |
| 4 | C | Multiple Choice |
| 5 | C | Multiple Choice |
| 6 | B | Multiple Choice |
| 7 | C | Multiple Choice |
| 8 | See above | Short Answer |
| 9 | See above | Short Answer |
| 10 | See above | Short Answer |

---

## Scoring Guide

- **Multiple Choice:** 1 point each (7 points total)
- **Short Answer Q8:** 2 points
- **Short Answer Q9:** 2 points
- **Short Answer Q10:** 2 points
- **Total:** 15 points

### Grading Scale
- 13-15 points: Excellent understanding
- 10-12 points: Good understanding, review edge cases
- 7-9 points: Basic understanding, practice more exercises
- Below 7: Review core concepts in the module

