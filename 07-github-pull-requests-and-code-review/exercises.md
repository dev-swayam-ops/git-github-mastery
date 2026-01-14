# GitHub Pull Requests and Code Review - Exercises

## Exercise 1: Create Your First Pull Request
**Difficulty:** Easy

Create a basic pull request with a simple feature.

**Instructions:**
1. Create a feature branch from main
2. Make 2-3 commits with code changes
3. Push the branch to origin
4. Open a pull request on GitHub
5. Add a clear title and description
6. Link to relevant issues if any
7. Request a reviewer
8. Verify the PR appears on GitHub
9. Check the Checks/CI status

**Expected Outcome:**
- PR successfully created
- Visible on GitHub
- Clear description of changes
- Proper branch naming
- CI checks running

---

## Exercise 2: Review and Comment on Code
**Difficulty:** Medium

Practice code review by commenting on changes.

**Instructions:**
1. Have a peer create a PR or use an existing PR
2. Review the code changes
3. Add inline comments on specific lines
4. Ask clarifying questions
5. Suggest improvements
6. Approve or request changes
7. Use GitHub's code review features
8. Respond to comments

**Expected Outcome:**
- Constructive feedback provided
- Comments on relevant code
- Review recorded in PR
- Communication is clear

---

## Exercise 3: Request Changes and Re-review
**Difficulty:** Medium

Handle code review feedback and updates.

**Instructions:**
1. Create a PR with intentional improvements needed
2. Have reviewer request changes
3. Update the code based on feedback
4. Make new commits addressing issues
5. Push updated code
6. Mark conversation as resolved
7. Re-request review
8. Verify changes address feedback

**Expected Outcome:**
- Feedback implemented
- Follow-up commits clear
- Review process documented
- PR conversation history clear

---

## Exercise 4: Handle Merge Conflicts in PR
**Difficulty:** Medium

Resolve conflicts when merging is blocked.

**Instructions:**
1. Create a PR that conflicts with main
2. Verify GitHub shows conflict warning
3. Resolve conflicts locally:
   - Pull latest main
   - Merge or rebase
   - Resolve conflicts
   - Push solution
4. Verify conflict resolution on GitHub
5. Re-request review if needed
6. Merge after resolution

**Expected Outcome:**
- Conflicts identified early
- Resolved cleanly
- PR mergeable afterward
- Clear conflict resolution history

---

## Exercise 5: Squash and Merge
**Difficulty:** Medium

Use squash merge for cleaner history.

**Instructions:**
1. Create a PR with multiple small commits
2. Review shows all commits
3. Use "Squash and merge" option
4. Write a combined commit message
5. Merge the PR
6. Check main branch shows single commit
7. Compare with regular merge approach
8. Understand when to use squash vs merge

**Expected Outcome:**
- Multiple commits combined into one
- Clean main branch history
- Useful for feature branches
- Clear understanding of merge strategies

---

## Exercise 6: Use Code Review Templates
**Difficulty:** Easy

Implement PR and issue templates.

**Instructions:**
1. Create `.github/PULL_REQUEST_TEMPLATE.md`
2. Add structured PR description format
3. Create `.github/ISSUE_TEMPLATE/bug_report.md`
4. Create `.github/ISSUE_TEMPLATE/feature_request.md`
5. Test templates in new PR
6. Verify template appears as default
7. Include sections for checklist
8. Make templates reusable

**Expected Outcome:**
- Consistent PR descriptions
- Better issue tracking
- Structured feedback
- Helpful guidance for contributors

---

## Exercise 7: Draft Pull Requests
**Difficulty:** Easy

Create draft PRs for early feedback.

**Instructions:**
1. Create a PR and mark as Draft
2. Add preliminary work
3. Request feedback early
4. Make updates based on feedback
5. Mark as Ready for Review
6. Convert to regular PR
7. Request full review
8. Understand draft PR benefits

**Expected Outcome:**
- Early feedback possible
- Not accidentally merged
- Collaborative development
- Clear WIP status

---

## Exercise 8: Add Labels and Milestones
**Difficulty:** Easy

Organize PRs with metadata.

**Instructions:**
1. Create a PR
2. Add labels: `enhancement`, `bug`, `documentation`
3. Add to a milestone: `v1.0.0`
4. Use labels for categorization
5. Filter PRs by label
6. Track milestone progress
7. Set priority with labels
8. Automate with labels

**Expected Outcome:**
- PRs organized by type
- Easy filtering and search
- Milestone tracking
- Better project management

---

## Exercise 9: Dismiss Stale Reviews
**Difficulty:** Medium

Manage review state when code changes.

**Instructions:**
1. Create a PR
2. Get approval from reviewer
3. Make significant code changes
4. Review becomes stale
5. Dismiss the old approval
6. Re-request review
7. Update from reviewer
8. Understand review vs change tracking

**Expected Outcome:**
- Approvals not automatically carried forward
- Clear when code changed
- Re-review process clear
- Safety mechanism understood

---

## Exercise 10: Auto-Link Issues
**Difficulty:** Easy

Link PRs to issues automatically.

**Instructions:**
1. Create an issue with number (e.g., #123)
2. Create a PR referencing issue
3. Use keywords: "fixes #123", "closes #123"
4. GitHub auto-links PR to issue
5. Close issue when PR merges
6. Issue shows PR merged it
7. Track issue resolution
8. Use keywords consistently

**Expected Outcome:**
- Issues linked to PRs
- Issue auto-closes on merge
- Clear issue resolution tracking
- Better project workflow

