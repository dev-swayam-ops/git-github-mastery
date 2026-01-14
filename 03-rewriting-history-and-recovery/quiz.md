# Rewriting History and Recovery - Quiz

## Multiple Choice Questions (7 Questions)

**Question 1:** What is the key difference between `git reset` and `git revert`?
- A) Reset is faster than revert
- B) Reset rewrites history, revert adds a new commit
- C) Revert is only for branches, reset is for commits
- D) They do the exact same thing

**Correct Answer:** B

**Explanation:** `git reset` moves the HEAD pointer and rewrites history (only safe for unpushed commits). `git revert` creates a new commit that undoes changes (safe for public commits).

---

**Question 2:** What does `git commit --amend --no-edit` do?
- A) Deletes the last commit
- B) Adds staged changes to the last commit without changing the message
- C) Renames the last commit
- D) Merges the last two commits

**Correct Answer:** B

**Explanation:** `--amend` modifies the last commit, `--no-edit` keeps the existing message. Staged changes are added to that commit.

---

**Question 3:** When you use `git reset --hard HEAD~1`, what happens?
- A) The last commit is kept, but changes are unstaged
- B) The last commit is removed and all its changes are discarded
- C) A revert commit is created
- D) The working directory is cleaned but commits remain

**Correct Answer:** B

**Explanation:** `--hard` discards all changes. `HEAD~1` targets the previous commit. Combined, this undoes and discards the last commit completely.

---

**Question 4:** What is the purpose of `git cherry-pick`?
- A) To merge entire branches
- B) To apply specific commits from one branch to another
- C) To delete commits
- D) To reorder all commits in history

**Correct Answer:** B

**Explanation:** `git cherry-pick <commit>` applies the specified commit's changes to your current branch, creating a new commit with the same changes but a new hash.

---

**Question 5:** In an interactive rebase, what does the `squash` command do?
- A) Deletes the commit
- B) Combines the commit with the previous one
- C) Renames the commit
- D) Moves the commit to a different branch

**Correct Answer:** B

**Explanation:** `squash` combines the commit's changes with the previous commit, resulting in fewer commits with combined content.

---

**Question 6:** What does `git reflog` show?
- A) All commits in the repository
- B) Recent changes to files
- C) Your recent HEAD movements and operations
- D) Remote branch history

**Correct Answer:** C

**Explanation:** `git reflog` shows a log of where HEAD has been, allowing you to recover "lost" commits even after reset or rebase operations.

---

**Question 7:** What happens to the commit hash when you amend a commit?
- A) The hash stays the same
- B) The hash changes because history is rewritten
- C) Git randomly generates a new hash
- D) The hash is not affected by amendments

**Correct Answer:** B

**Explanation:** Amending changes the commit's content, so Git calculates a new hash. This is why amendments only work for unpushed commits.

---

## Short Answer Questions (3 Questions)

**Question 8:** Explain the steps to recover a commit that was accidentally deleted with `git reset --hard`.

**Suggested Answer:**
1. Use `git reflog` to view recent HEAD movements
2. Find the commit hash you want to recover in the reflog output
3. Run `git reset --hard <commit-hash>` to restore to that point
4. Or use `git reset --hard HEAD@{<n>}` where n is the reflog entry number
5. Verify the commit is restored with `git log`

**Scoring:** Full points for mentioning reflog, finding commit hash, and resetting. Partial credit for incomplete steps.

---

**Question 9:** You have 4 commits where the second commit has a typo in the message. You want to fix just that message without changing other commits. How would you do this?

**Suggested Answer:**
1. Use `git rebase -i HEAD~3` to start interactive rebase for the last 3 commits
2. Change the second commit's operation from `pick` to `reword`
3. Save and exit the editor
4. In the next editor that opens, fix the commit message
5. Save and exit
6. The rebase completes with the fixed message
7. Other commits remain unchanged

**Scoring:** Full points for correct rebase approach and reword command. Partial credit if missing some details.

---

**Question 10:** What is the safest way to undo a commit that has already been pushed to a remote branch that others might be using?

**Suggested Answer:**
Use `git revert <commit-hash>` instead of reset or amend because:
- Creates a new commit that undoes the changes
- Doesn't rewrite history
- Doesn't confuse other developers
- Safe for public/shared branches
- Other developers won't have conflicts with pushed history

Do NOT use `git reset` or amend for pushed commits as this rewrites shared history and causes problems for team members.

**Scoring:** Full points for explaining revert and why it's safe for pushed commits. Partial credit for correct command but incomplete explanation.

---

## Answer Key Summary

| Question | Answer | Type |
|----------|--------|------|
| 1 | B | Multiple Choice |
| 2 | B | Multiple Choice |
| 3 | B | Multiple Choice |
| 4 | B | Multiple Choice |
| 5 | B | Multiple Choice |
| 6 | C | Multiple Choice |
| 7 | B | Multiple Choice |
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
- 13-15 points: Excellent understanding of history rewriting
- 10-12 points: Good understanding, practice reflog recovery
- 7-9 points: Basic understanding, review interactive rebase
- Below 7: Review reset vs revert concepts

