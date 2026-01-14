# Git Branching and Merging - Exercises

## Exercise 1: Create Your First Branch
**Difficulty:** Easy

Create a new branch called `feature/first-branch` from the current branch.

**Instructions:**
1. Check your current branch status
2. Create a new local branch named `feature/first-branch`
3. Verify the branch was created
4. Do NOT switch to it yet

**Expected Outcome:**
- You should see the new branch in your branch list
- Your current branch should remain unchanged

---

## Exercise 2: Switch Between Branches
**Difficulty:** Easy

Switch between multiple branches to understand branch navigation.

**Instructions:**
1. Create a branch called `feature/user-auth`
2. Switch to the new branch
3. Create a new file called `auth.js` and add some code
4. Switch back to your main branch
5. Verify that `auth.js` does not exist on main

**Expected Outcome:**
- File exists on `feature/user-auth`
- File does not exist on main branch
- You can navigate between branches seamlessly

---

## Exercise 3: List All Branches
**Difficulty:** Easy

Explore different ways to view your branches.

**Instructions:**
1. Create 3 new branches: `feature/dashboard`, `bugfix/login-error`, `docs/readme`
2. List all local branches
3. List all branches including remote tracking branches
4. Show the current branch with a special marker

**Expected Outcome:**
- You can see all 3 new branches in the list
- Current branch is clearly marked with an asterisk
- Understand the difference between local and all branches

---

## Exercise 4: Fast-Forward Merge
**Difficulty:** Medium

Perform a simple fast-forward merge when no conflicting changes exist.

**Instructions:**
1. Start on your main branch
2. Create a branch called `feature/simple-feature`
3. Make 2 commits on this feature branch (add/modify files)
4. Switch back to main
5. Merge the feature branch into main using default merge
6. Verify the merge succeeded and commits appear on main
7. Delete the feature branch after merging

**Expected Outcome:**
- Main branch now includes commits from feature branch
- Commit history is linear (fast-forward)
- Feature branch is deleted
- Git log shows all commits in order

---

## Exercise 5: Three-Way Merge
**Difficulty:** Medium

Create and merge branches that both modified the codebase independently.

**Instructions:**
1. Start on main branch
2. Create `feature/header` and make a commit modifying `header.js`
3. Switch back to main and create `feature/footer`
4. Make a commit modifying `footer.js` on the footer branch
5. Switch to main branch
6. Merge `feature/header` (should be fast-forward)
7. Then merge `feature/footer` (should create a merge commit)
8. View the merge commit in your history

**Expected Outcome:**
- Both features are merged into main
- A merge commit is created for the second merge
- Git log shows the branch structure
- Both feature commits are reachable from main

---

## Exercise 6: Detect and Resolve Merge Conflicts
**Difficulty:** Medium

Create a merge conflict intentionally and resolve it.

**Instructions:**
1. Create a file `config.js` on main with content: `const API_URL = "http://localhost:3000";`
2. Commit this file
3. Create a branch `feature/prod-config`
4. Modify the same line to: `const API_URL = "https://api.production.com";`
5. Commit this change
6. Switch back to main
7. Modify the same line differently: `const API_URL = "http://staging:8000";`
8. Commit this change
9. Try to merge `feature/prod-config` (this will conflict)
10. Resolve the conflict by keeping the production URL
11. Complete the merge

**Expected Outcome:**
- Git detects the conflict in `config.js`
- You can see conflict markers in the file
- After resolution, merge completes successfully
- Git log shows the merge commit

---

## Exercise 7: Abort a Merge
**Difficulty:** Medium

Learn how to cancel a merge operation if something goes wrong.

**Instructions:**
1. Create two branches: `feature/branch-a` and `feature/branch-b`
2. Make conflicting changes on both branches
3. Attempt to merge `feature/branch-b` into `feature/branch-a`
4. When you see the conflict, abort the merge without resolving
5. Verify your working directory is clean
6. Verify you're still on `feature/branch-a` with original content

**Expected Outcome:**
- Merge is safely aborted
- No files are modified
- You're back to pre-merge state
- No merge commit is created

---

## Exercise 8: Rename a Branch
**Difficulty:** Easy

Rename an existing branch locally and understand naming conventions.

**Instructions:**
1. Create a branch called `feature/old-name`
2. Rename it to `feature/new-feature-name`
3. Verify the old name no longer exists
4. Verify the new name exists
5. Create another branch with a good naming pattern: `bugfix/issue-123-description`

**Expected Outcome:**
- Branch is successfully renamed
- Old branch name is gone
- New branch name exists and is usable
- You understand branch naming conventions

---

## Exercise 9: Merge with Merge Commit
**Difficulty:** Medium

Perform a merge that creates an explicit merge commit even when fast-forward is possible.

**Instructions:**
1. Create a new branch `feature/explicit-merge`
2. Make a commit on this branch
3. Switch back to main
4. Merge the feature branch using the `--no-ff` flag (no fast-forward)
5. You'll be prompted to enter a merge commit message (enter a descriptive message)
6. View the history to see the merge commit

**Expected Outcome:**
- A merge commit is created even though fast-forward was possible
- The merge commit has a message you provided
- Git log shows the branch structure clearly
- Both commits are included in the history

---

## Exercise 10: Compare Branches
**Difficulty:** Medium

Compare different branches to understand what commits differ between them.

**Instructions:**
1. Create a branch `feature/compare-me` from main
2. Make 2 commits on this feature branch
3. Switch back to main and make 1 commit
4. Compare the feature branch to main to see:
   - Commits in feature that aren't in main
   - Commits in main that aren't in feature
5. Compare specific files between branches
6. View the actual differences in a file between branches

**Expected Outcome:**
- You can see which commits are unique to each branch
- You can see file-level differences between branches
- You understand how to review changes before merging
- You can make informed decisions about merging

