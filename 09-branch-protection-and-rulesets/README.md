# 09-branch-protection-and-rulesets

## What You'll Learn

By the end of this module, you'll understand:
- Creating branch protection rules
- Configuring status checks
- Code review requirements
- Merging strategies and protections
- CODEOWNERS and review delegation
- Rulesets (GitHub's new protection system)
- Enforcing quality standards

## Prerequisites

- Completion of Modules 01-08
- Understanding of branch workflows
- GitHub repository with admin access

## Key Concepts

| Protection | Purpose | Impact |
|------------|---------|--------|
| **Require PR** | Force code review | No direct commits to protected branch |
| **Require Reviews** | Approval needed | Minimum reviewers must approve |
| **Status Checks** | Automated tests pass | CI/CD must succeed before merge |
| **Dismiss Stale** | Refresh old reviews | New commits require new reviews |
| **CODEOWNERS** | Automatic reviewers | Files with owners require their approval |
| **Rulesets** | Modern protection | More granular control |
| **Require Branches** | Base branch must exist | Can't merge to missing branch |

## Hands-on Lab: Setting Up Branch Protection

### Scenario
You're implementing strict protection rules for main branch to ensure quality and prevent accidents.

### Step-by-Step Commands

```bash
# Step 1: Clone repository
git clone <repo>
cd <repo>

# Step 2: Create CODEOWNERS file
echo "# Repository Code Owners" > CODEOWNERS
echo "*       @team-lead" >> CODEOWNERS
echo "src/api/ @api-team" >> CODEOWNERS
echo "src/ui/ @frontend-team" >> CODEOWNERS
git add CODEOWNERS
git commit -m "Add CODEOWNERS file"
git push origin main

# Step 3: Go to GitHub Settings > Branches
# Click "Add rule"
# Pattern name: main

# Step 4: Configure protections
# ✓ Require a pull request before merging
# ✓ Require approvals (2)
# ✓ Dismiss stale pull request approvals
# ✓ Require status checks to pass
# ✓ Require branches to be up to date
# ✓ Require code to be analyzed before merging

# Step 5: Add status check requirement
# GitHub > Settings > Branches > main rule
# Add status check: "build", "tests", "lint"

# Step 6: Enforce status checks
# ✓ Require status checks to pass before merging
# ✓ Require branches to be up to date before merging

# Step 7: Create ruleset (new way)
# GitHub > Settings > Rulesets > New ruleset
# Name: Main Branch Protection
# Target: main
# Rules: Require PR, require reviews, require status checks

# Step 8: Test protection (expected to fail)
git checkout main
echo "dangerous" >> dangerous.txt
git add dangerous.txt
git commit -m "Direct commit to main"
# git push origin main (should be rejected)

# Step 9: Proper workflow
git checkout -b fix/critical
echo "fix" > fix.txt
git add fix.txt
git commit -m "Critical fix"
git push origin fix/critical
# Create PR, get reviews, merge through GitHub
```

### Expected Output

```
CODEOWNERS file created
Branch protection rule added
[blocked] Direct push to main
[success] PR created and merged after reviews
```

## Validation

You've successfully completed this lab if:
- ✓ Created CODEOWNERS file
- ✓ Set branch protection rule
- ✓ Configured PR requirement
- ✓ Configured review requirement
- ✓ Set up status checks
- ✓ Tested protection (confirm it blocks unauthorized changes)

## Cleanup

```bash
git checkout main
git pull origin main
rm -f dangerous.txt fix.txt
git add .
git commit -m "Cleanup: Remove test files"
git push origin main
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| No branch protection | Anyone can force push | Always protect main/release branches |
| Too many reviewers | Slow development | Balance review quality with velocity |
| Forgetting CODEOWNERS | Wrong people review | Create CODEOWNERS for each team area |
| Status checks too lenient | Bad code merges | Include linting, testing, security scans |
| Bypassing protection often | Rules become useless | Enforce rules strictly |

## Troubleshooting

**Q: Can admins bypass branch protection?**
- A: Yes, but you can enable "Restrict who can push to matching branches"

**Q: How many reviewers should I require?**
- A: Minimum 1-2. More than 2 slows development. Depends on team size

**Q: What status checks should I require?**
- A: Build, unit tests, linting, security scan. Keep fast (< 10 minutes)

**Q: Can I have different rules per branch?**
- A: Yes! Create multiple branch protection rules with different patterns

**Q: What if a status check is broken?**
- A: Fix the check, or temporarily disable for unblocking PRs (with documentation)

## Next Steps

Once comfortable with:
- Branch protection rules
- Code review requirements
- CODEOWNERS
- Rulesets

Move to **Module 10: GitHub Actions CI/CD Basics** to automate your workflows.

---

**Time to Complete:** 50 minutes  
**Difficulty Level:** Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
