# 09-branch-protection-and-rulesets: Exercises

## Exercise 1: Create Your First Branch Protection Rule
**Difficulty:** Easy

Set up basic protection on the main branch.

**Instructions:**
1. Go to Settings > Branches > Add rule
2. Enter "main" as branch pattern
3. Enable "Require pull request reviews"
4. Set to 1 reviewer
5. Save rule
6. Verify rule appears in list

**Expected Outcome:** Branch protection rule created for main

---

## Exercise 2: Require Status Checks
**Difficulty:** Easy

Add CI/CD validation requirement.

**Instructions:**
1. Edit branch protection rule
2. Check "Require status checks to pass before merging"
3. Check "Require branches to be up to date before merging"
4. Save changes
5. Try to merge without passing checks (should fail)

**Expected Outcome:** Cannot merge without passing status checks

---

## Exercise 3: Enforce Commit Signatures
**Difficulty:** Medium

Require cryptographic commit signatures.

**Instructions:**
1. Edit branch protection rule
2. Enable "Require signed commits"
3. Save changes
4. Try to commit without signing (should be rejected)
5. Configure GPG signing on your machine

**Expected Outcome:** Only signed commits allowed

---

## Exercise 4: Restrict Who Can Push
**Difficulty:** Medium

Control who has bypass permissions.

**Instructions:**
1. Edit branch protection rule
2. Find "Who has access to push to matching branches"
3. Configure restrictions
4. Test that only specified users/teams can merge
5. Verify others cannot bypass

**Expected Outcome:** Push access properly restricted

---

## Exercise 5: Dismiss Stale Reviews
**Difficulty:** Medium

Automatically invalidate approvals when new commits arrive.

**Instructions:**
1. Edit branch protection rule
2. Enable "Dismiss stale pull request approvals when new commits are pushed"
3. Make a PR, get approval
4. Push new commits
5. Verify approval is dismissed (PR needs re-review)

**Expected Outcome:** Reviews dismissed on new changes

---

## Exercise 6: Require Code Owner Approval
**Difficulty:** Medium

Set up CODEOWNERS file and require their approval.

**Instructions:**
1. Create CODEOWNERS file in repository
2. Add entries like: `*.js @username`
3. Edit branch protection rule
4. Enable "Require code owner review"
5. Make PR modifying protected files
6. Verify code owner must approve

**Expected Outcome:** Code owners must review changes

---

## Exercise 7: Require Conversation Resolution
**Difficulty:** Medium

Prevent merge until review comments are resolved.

**Instructions:**
1. Edit branch protection rule
2. Enable "Require conversation resolution before merging"
3. Create PR with review comments
4. Try to merge (should fail)
5. Resolve conversations
6. Now merge succeeds

**Expected Outcome:** All comments must be resolved before merge

---

## Exercise 8: Create Multiple Branch Patterns
**Difficulty:** Medium

Protect multiple branches with different rules.

**Instructions:**
1. Create rule for "main" (strict: 2 reviews, status checks, signed commits)
2. Create rule for "develop" (moderate: 1 review, status checks)
3. Create rule for "release/*" (requires approval)
4. Verify each branch has appropriate protection
5. Understand how patterns work (wildcards, etc.)

**Expected Outcome:** Multiple rules with appropriate strictness

---

## Exercise 9: Configure Ruleset (GitHub Advanced)
**Difficulty:** Medium

Use the newer Rulesets feature for complex scenarios.

**Instructions:**
1. Go to Settings > Rules > Rulesets
2. Create new ruleset
3. Add multiple rules together
4. Set conditions (branch, tag)
5. Test that rules apply correctly
6. Understand ruleset advantages over old rules

**Expected Outcome:** Ruleset configured with multiple enforcement rules

---

## Exercise 10: Test and Validate All Rules
**Difficulty:** Medium

Verify your protection rules work as intended.

**Instructions:**
1. Create test branch from protected branch
2. Try to commit directly (should fail)
3. Create PR instead
4. Verify status checks required
5. Verify review required
6. Get approval and merge (should succeed)
7. Verify all protections worked correctly

**Expected Outcome:** All branch protection rules validated

---

## Summary

| Exercise | Topic | Difficulty |
|----------|-------|-----------|
| 1 | Basic Protection | Easy |
| 2 | Status Checks | Easy |
| 3 | Signed Commits | Medium |
| 4 | Push Restrictions | Medium |
| 5 | Stale Reviews | Medium |
| 6 | Code Owners | Medium |
| 7 | Conversations | Medium |
| 8 | Multiple Rules | Medium |
| 9 | Rulesets | Medium |
| 10 | Validation | Medium |
