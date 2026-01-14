# 13-troubleshooting-and-best-practices: Exercises

## Exercise 1: Debugging Detached HEAD State
**Difficulty:** Medium

Recover from detached HEAD state.

**Instructions:**
1. Checkout specific commit (detached HEAD)
2. Notice you're no longer on a branch
3. Make a test commit
4. Check status
5. Create branch to save work
6. Return to main

**Expected Outcome:** Understand detached HEAD and recovery

---

## Exercise 2: Recover Lost Commits
**Difficulty:** Medium

Use reflog to find and restore lost commits.

**Instructions:**
1. Reset to earlier commit (git reset --hard)
2. Try to find "lost" commits
3. Use git reflog to find them
4. Reset back to lost commit
5. Create branch to save it

**Expected Outcome:** Recover commits using reflog

---

## Exercise 3: Fix Upstream Issues
**Difficulty:** Medium

Handle problems with remote repository.

**Instructions:**
1. Simulate remote being reset
2. Try to push/pull (fails)
3. Diagnose issue with git remote -v
4. Use force-with-lease
5. Sync teams on what happened

**Expected Outcome:** Resolve remote sync issues

---

## Exercise 4: Handle Large Files
**Difficulty:** Medium

Deal with accidentally committed large files.

**Instructions:**
1. Accidentally commit large file
2. Remove from git history
3. Use git filter-branch or BFG
4. Force push carefully
5. Configure .gitignore to prevent

**Expected Outcome:** Remove large files from history

---

## Exercise 5: Performance Optimization
**Difficulty:** Medium

Improve repository performance.

**Instructions:**
1. Check repository size
2. Identify large objects
3. Clean up reflog/garbage
4. Run git gc
5. Monitor performance

**Expected Outcome:** Optimized repository

---

## Exercise 6: Fixing Collaborator Mistakes
**Difficulty:** Medium

Help when team member makes Git error.

**Instructions:**
1. Teammate creates wrong branch
2. Makes commits to wrong branch
3. Pushed accidentally to main
4. Help them recover
5. Document what happened

**Expected Outcome:** Resolve collaborator mistakes

---

## Exercise 7: Complex Merge Scenarios
**Difficulty:** Medium

Handle complicated merge situations.

**Instructions:**
1. Create scenario with multiple branches
2. Create complex conflict
3. Need selective merge (cherry-pick)
4. Different merge strategies
5. Resolve with appropriate tool

**Expected Outcome:** Handle complex merges

---

## Exercise 8: Debugging CI/CD Failures
**Difficulty:** Medium

Diagnose and fix CI/CD pipeline issues.

**Instructions:**
1. Create failing workflow
2. View workflow logs
3. Identify root cause
4. Fix locally first
5. Push fix to trigger re-run

**Expected Outcome:** Resolve CI/CD issues

---

## Exercise 9: Audit and Compliance
**Difficulty:** Medium

Ensure repository meets standards.

**Instructions:**
1. Check branch protection rules
2. Review collaborators
3. Check for security issues
4. Review commit history
5. Document compliance

**Expected Outcome:** Repository audit complete

---

## Exercise 10: Preventing Common Mistakes
**Difficulty:** Medium

Set up preventative measures.

**Instructions:**
1. Set pre-commit hooks
2. Configure hooks to lint/test
3. Prevent pushing secrets
4. Enforce commit style
5. Require tests before push

**Expected Outcome:** Automated prevention in place

---

## Summary

| Exercise | Topic | Difficulty |
|----------|-------|-----------|
| 1 | Detached HEAD | Medium |
| 2 | Recover Commits | Medium |
| 3 | Remote Issues | Medium |
| 4 | Large Files | Medium |
| 5 | Performance | Medium |
| 6 | Collab Mistakes | Medium |
| 7 | Complex Merges | Medium |
| 8 | CI/CD Debugging | Medium |
| 9 | Audit/Compliance | Medium |
| 10 | Prevention | Medium |
