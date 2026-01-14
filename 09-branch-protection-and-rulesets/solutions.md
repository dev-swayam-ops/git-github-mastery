# 09-branch-protection-and-rulesets: Solutions

## Solution 1: Create Your First Branch Protection Rule

**Steps:**
```
Settings > Branches > Add rule
- Branch name pattern: main
- Check: "Require pull request reviews before merging"
- Number of reviewers: 1
- Click "Create"
```

**Result:**
- Direct pushes to main blocked
- All changes require PR
- Minimum 1 approval needed
- PR can be merged after review

---

## Solution 2: Require Status Checks

**Configuration:**
```
Edit Branch Protection Rule > Add these checks:
☑ Require status checks to pass before merging
  - Status checks:
    - CI/CD Pipeline (e.g., GitHub Actions)
    - Code quality checks
    - Test suite
☑ Require branches to be up to date before merging
```

**Effect:**
- PR cannot merge if tests fail
- Branch must be synced with main
- Ensures code quality before merge

---

## Solution 3: Enforce Commit Signatures

**Setup on Your Machine:**
```bash
# Generate GPG key (macOS/Linux)
gpg --gen-key

# Or for Windows
gpg --full-generate-key

# List keys
gpg --list-secret-keys

# Configure Git to sign commits
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true
```

**GitHub Configuration:**
```
Settings > SSH and GPG keys > New GPG key
- Paste your public key
- Save
```

**Branch Protection:**
```
Edit rule > Check: "Require signed commits"
```

**Making Signed Commits:**
```bash
git commit -S -m "Signed commit message"
# Verify with:
git log --show-signature
```

---

## Solution 4: Restrict Who Can Push

**Configuration:**
```
Edit Branch Protection Rule:
☑ Restrict who can push to matching branches
  - Select users/teams who can push
  - Or: Only admins can push
  - Or: Only code owners can push
```

**Example Setup:**
```
Allow push for:
- Code owners (team leads)
- Release managers
- Prevent: regular developers (must use PR)
```

---

## Solution 5: Dismiss Stale Reviews

**Configuration:**
```
Edit Branch Protection Rule:
☑ Dismiss stale pull request approvals when new commits are pushed
```

**Workflow:**
1. Alice approves PR
2. Developer pushes new changes
3. Alice's approval automatically dismissed
4. PR requires review again
5. Alice reviews new changes

**Why This Matters:**
- Ensures reviews are current
- Prevents outdated approvals
- Developers can't sneak changes after approval

---

## Solution 6: Require Code Owner Approval

**Create CODEOWNERS File:**
```
# In repository root, create file: CODEOWNERS

# Global owners
* @alice @bob

# JavaScript files
*.js @javascript-team

# Configuration
*.yml @devops-team

# Specific directory
/backend/ @backend-team
/frontend/ @frontend-team

# Specific files
package.json @alice
```

**Branch Protection:**
```
Edit rule:
☑ Require code owner review
☑ Require approval from code owners: YES
```

**Effect:**
- Changes to *.js require @javascript-team approval
- Changes to /backend/ require @backend-team approval
- Ensures domain experts review changes

---

## Solution 7: Require Conversation Resolution

**Configuration:**
```
Edit Branch Protection Rule:
☑ Require conversation resolution before merging
```

**Workflow:**
1. Reviewer leaves comment
2. Developer sees comment
3. Developer makes changes
4. Developer resolves conversation
5. Comment no longer blocks merge

**Via CLI:**
```bash
# List unresolved conversations
gh pr view PR_NUMBER

# Resolve conversation
# (Must be done on GitHub web)
```

---

## Solution 8: Create Multiple Branch Patterns

**Main Branch (Strict):**
```
Pattern: main
- Require 2 reviews
- Require status checks
- Require signed commits
- Require branches up to date
- Dismiss stale reviews
- Allow force pushes: NO
- Allow deletions: NO
```

**Develop Branch (Moderate):**
```
Pattern: develop
- Require 1 review
- Require status checks
- Require branches up to date
- Allow force pushes: NO
- Allow deletions: NO
```

**Release Branch (Release):**
```
Pattern: release/*
- Require 2 reviews
- Require signed commits
- Require status checks
- Lock to prevent changes
```

---

## Solution 9: Configure Ruleset

**Creating Rulesets:**
```
Settings > Rules > Rulesets > New ruleset
```

**Configuration:**
```yaml
Ruleset Name: Production Protection
Targets: 
  - Branch: main
  
Rules:
  - Require pull request reviews: 2
  - Require status checks: enabled
  - Require signed commits: enabled
  - Require conversation resolution: enabled
  - Block force push: enabled
  - Block deletions: enabled
  
Enforcement Level: Active
```

**Advantage over Branch Protection Rules:**
- Combine multiple rules
- Apply to branches and tags
- More flexible conditions
- Newer, more powerful

---

## Solution 10: Test and Validate All Rules

**Test Procedure:**
```bash
# 1. Try direct push (should fail)
echo "test" > file.txt
git add file.txt
git commit -m "Test commit"
git push origin main
# Output: rejected - cannot push

# 2. Create PR instead
git checkout -b feature/test
git push origin feature/test
# Create PR on GitHub

# 3. Check status
gh pr view --web

# 4. Get approval
gh pr review --approve

# 5. Merge
gh pr merge --squash

# 6. Verify success
git log --oneline
```

**Validation Checklist:**
- ✓ Cannot push directly to main
- ✓ PR requires review before merge
- ✓ Status checks must pass
- ✓ Branch must be up to date
- ✓ Signed commits enforced
- ✓ Code owners required
- ✓ Cannot delete main branch
- ✓ Cannot force push to main

---

## Common Patterns

### Production Safety
```
main branch:
- 2+ reviews required
- Status checks required
- Signed commits required
- Cannot delete
- Cannot force push
- Conversation resolution required
- Code owner approval
```

### Team Development
```
develop branch:
- 1 review required
- Status checks required
- Cannot delete
- Dismiss stale reviews
```

### Release Management
```
release/* pattern:
- 2 reviews required
- No force push allowed
- Signed commits required
- Status checks required
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Cannot push to main | This is expected - use PR instead |
| PR won't merge | Check status checks, review status |
| Status check failing | Fix code, re-run tests |
| Stale approval | Push new commit to refresh |
| Signature verification failed | Configure GPG signing, use `-S` flag |
