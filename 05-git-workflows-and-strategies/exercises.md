# Git Workflows and Strategies - Exercises

## Exercise 1: Set Up Git Flow Workflow
**Difficulty:** Easy

Initialize a repository with the Git Flow structure.

**Instructions:**
1. Initialize a new repository
2. Create a `main` branch (for releases)
3. Create a `develop` branch (main development)
4. Create a feature branch `feature/user-registration` from develop
5. Make some commits on the feature branch
6. Switch back to develop
7. Create another feature branch `feature/profile-management`
8. Make commits on this branch
9. Verify you have the proper branch structure

**Expected Outcome:**
- Main branch exists for releases only
- Develop branch is the integration branch
- Multiple feature branches work independently from develop
- Clear separation of concerns

---

## Exercise 2: GitHub Flow Workflow
**Difficulty:** Easy

Practice the simpler GitHub Flow workflow.

**Instructions:**
1. Start from main branch
2. Create a feature branch: `feature/dark-mode`
3. Make 2-3 commits with meaningful messages
4. Switch to main
5. Create another feature branch: `feature/api-endpoint`
6. Make commits there
7. Compare branches to see differences
8. Merge the first feature into main
9. Delete the merged branch
10. Repeat for the second feature

**Expected Outcome:**
- Simple workflow with main and feature branches
- Features are self-contained in branches
- Easy to merge and delete branches
- Cleaner history than Git Flow for simple projects

---

## Exercise 3: Trunk-Based Development Workflow
**Difficulty:** Medium

Practice trunk-based development with short-lived branches.

**Instructions:**
1. Start with main as the trunk
2. Create short-lived branches for small changes:
   - `feature/bugfix-typo`
   - `feature/add-log`
   - `feature/update-readme`
3. Each branch should have only 1-2 commits
4. Merge each back to main quickly
5. Verify that all merges are completed
6. Notice how main stays up-to-date
7. Create 5 more small feature branches and merge them
8. View git log to see frequent merges to main

**Expected Outcome:**
- Very short-lived branches (hours, not days)
- Frequent integrations to main
- Reduced merge conflicts
- Continuous integration friendly

---

## Exercise 4: Release Branch Workflow
**Difficulty:** Medium

Create and work with release branches in Git Flow.

**Instructions:**
1. Develop several features on feature branches
2. Merge features into develop
3. Create a release branch: `release/1.0.0` from develop
4. Make bug-fix commits on release branch
5. Create a hotfix branch from release: `hotfix/1.0.0-critical-bug`
6. Fix the critical bug
7. Merge hotfix back to release
8. Merge release back to main
9. Tag main with `v1.0.0`
10. Merge release back to develop

**Expected Outcome:**
- Release branch isolates release preparation
- Bug fixes on release don't affect main develop
- Proper tagging for releases
- Both main and develop stay synchronized

---

## Exercise 5: Hotfix Workflow
**Difficulty:** Medium

Practice hotfixes for critical production bugs.

**Instructions:**
1. Start with main at v1.0.0
2. Create a `hotfix/critical-security-bug` from main
3. Fix the security bug with a commit
4. Create a tag `v1.0.1` on the hotfix
5. Merge hotfix into main
6. Also merge hotfix into develop (important!)
7. Delete the hotfix branch
8. Verify both main and develop have the fix
9. Verify tags exist for both versions

**Expected Outcome:**
- Hotfix solves production issues quickly
- Both main and develop receive the fix
- Proper versioning with tags
- Hotfix branch is temporary and cleaned up

---

## Exercise 6: Feature Branching Strategy
**Difficulty:** Medium

Implement a comprehensive feature branching strategy.

**Instructions:**
1. Create multiple feature branches with good naming:
   - `feature/auth-system`
   - `feature/user-dashboard`
   - `feature/notification-service`
2. Each branch should have 3-5 commits
3. Use nested feature branches: `feature/auth-system/login` and `feature/auth-system/logout`
4. Merge login feature into auth-system
5. Merge logout feature into auth-system
6. Merge complete auth-system into develop
7. Merge other features into develop
8. Delete all feature branches after merging

**Expected Outcome:**
- Good naming conventions for features
- Complex features can be broken into sub-features
- Organized branch structure
- Clean cleanup after merging

---

## Exercise 7: Parallel Development with Multiple Branches
**Difficulty:** Medium

Manage simultaneous development on multiple branches.

**Instructions:**
1. Create 3 simultaneous feature branches from develop:
   - `feature/cache-optimization`
   - `feature/logging-system`
   - `feature/error-handling`
2. Make commits on all 3 in parallel (simulate)
3. Merge one feature at a time into develop
4. After each merge, create a new feature branch from the updated develop
5. Practice keeping features isolated
6. Verify merges don't cause conflicts
7. Understand how commits from separate branches combine

**Expected Outcome:**
- Multiple developers can work on different features
- Each branch stays independent
- Merging one feature doesn't block others
- Features combine properly in develop

---

## Exercise 8: Merge Strategies and Rebase Workflow
**Difficulty:** Medium

Compare different approaches to integrating features.

**Instructions:**
1. Create a feature branch `feature/rebase-demo` with 3 commits
2. Meanwhile, make 2 commits on develop
3. Compare two integration methods:
   - Method A: Merge without rebase
   - Method B: Rebase then merge
4. For each method:
   - Check the commit history
   - Check for merge commits
   - Check commit order
5. Understand when to use each approach
6. Note the difference in history visualization

**Expected Outcome:**
- Merge creates merge commits (visible history)
- Rebase creates linear history (cleaner look)
- Both achieve the same end state
- Different workflows have trade-offs

---

## Exercise 9: Feature Toggle / Feature Flags Workflow
**Difficulty:** Medium

Practice shipping incomplete features using feature flags.

**Instructions:**
1. Create a feature branch `feature/new-payment-system`
2. Implement new payment system code
3. Add conditional code checks using environment variables/flags:
   - `if (process.env.USE_NEW_PAYMENT === 'true')`
4. Merge the incomplete feature into main (disabled)
5. Create configuration that enables the flag
6. Show how the feature can be toggled without branching
7. Demonstrate enabling for specific users/regions
8. Later, remove the flag when fully tested

**Expected Outcome:**
- Incomplete features can be merged safely
- Features controlled by flags, not branches
- Easy to enable/disable without deployment
- Reduces time features spend in branches

---

## Exercise 10: Versioning Strategy with Tags
**Difficulty:** Medium

Implement semantic versioning with tags across workflow.

**Instructions:**
1. Create releases with semantic versioning:
   - `v1.0.0` (major release)
   - `v1.0.1` (patch release)
   - `v1.1.0` (minor release)
   - `v2.0.0` (new major version)
2. Tag each release on main branch
3. Document which features are in each version
4. Create branches for older versions if needed
5. Show how to check what version is deployed
6. Practice creating release branches from tags
7. Demonstrate checking what changed between versions

**Expected Outcome:**
- Clear versioning scheme
- Tags mark release points
- Version history is trackable
- Can refer to specific versions
- Can create maintenance branches from old versions

