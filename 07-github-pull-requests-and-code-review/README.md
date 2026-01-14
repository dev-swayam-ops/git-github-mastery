# 07-github-pull-requests-and-code-review

## What You'll Learn

By the end of this module, you'll understand:
- Creating and managing pull requests
- Code review best practices
- Reviewing code effectively
- Asking for reviews
- Handling review feedback
- Merging strategies
- PR templates and workflows

## Prerequisites

- Completion of Modules 01-06
- Understanding of branches
- Basic GitHub knowledge
- Team collaboration experience

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Pull Request** | Proposal to merge branch changes |
| **Review** | Code inspection before merging |
| **Approval** | Formal sign-off on changes |
| **Reviewer** | Person who reviews code |
| **Draft PR** | Work-in-progress PR not ready for review |
| **Commit History** | Clean history improves review |
| **Review Comments** | Feedback on specific lines |
| **Merge Commit** | Preserves PR history |

## Hands-on Lab: Creating and Reviewing a Pull Request

### Scenario
You've completed a feature and need to create a PR, address review feedback, and merge.

### Step-by-Step Commands

```bash
# Step 1: Create feature branch
git checkout develop
git pull origin develop
git checkout -b feature/add-logging

# Step 2: Make changes
echo "import logging" > logger.py
echo "logger = logging.getLogger()" >> logger.py
git add logger.py
git commit -m "Add logging module"

echo "logger.info('app started')" >> app.py
git add app.py
git commit -m "Add startup log"

# Step 3: Push feature branch
git push origin feature/add-logging

# Step 4: Create PR on GitHub
# Go to GitHub, click "New Pull Request"
# Base: develop, Compare: feature/add-logging
# Add description with:
#   - What changed
#   - Why it changed
#   - How to test

# Step 5: View PR status
git log --oneline origin/develop..HEAD

# Step 6: Address review feedback (simulated)
git checkout feature/add-logging
echo "logger.setLevel(logging.INFO)" >> logger.py
git add logger.py
git commit -m "Set logging level"
git push origin feature/add-logging

# Step 7: Merge PR
# GitHub: Click "Merge Pull Request"
# Choose merge strategy: Squash, Rebase, or Create Merge Commit

# Step 8: Update local
git checkout develop
git pull origin develop

# Step 9: Delete branch
git branch -d feature/add-logging
git push origin --delete feature/add-logging
```

### Expected Output

```
Pull request created: #42
Review requested from @reviewer
[New commit] Set logging level
Pull request merged!
Branch deleted
```

## Validation

You've successfully completed this lab if:
- ✓ Created feature branch
- ✓ Pushed branch to remote
- ✓ Opened pull request
- ✓ Addressed feedback
- ✓ Merged pull request
- ✓ Cleaned up branch

## Cleanup

```bash
git checkout develop
rm -f logger.py
git add .
git commit -m "Cleanup: Remove test files"
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Too many commits in PR | Hard to review | Squash commits before merging |
| Huge PRs with many files | Reviewer overwhelmed | Keep PRs small (<400 lines) |
| No description | Reviewer confused | Always add detailed description |
| Requesting yourself as reviewer | No actual review | Get reviews from teammates |
| Force pushing after review | Review becomes invalid | Use gentle push or create new PR |

## Troubleshooting

**Q: How do I create a pull request?**
- A: Push branch, go to GitHub, click "Compare & pull request", add description

**Q: What should be in a PR description?**
- A: What changed, why it changed, how to test, related issues/PRs

**Q: How long should review take?**
- A: Aim for < 24 hours. Don't let PRs sit for days

**Q: Can I make changes during review?**
- A: Yes! Push new commits. Keep conversation in PR

**Q: What merge strategy should I use?**
- A: Squash for features, merge commit for releases, rebase for clean history

## Next Steps

Once comfortable with:
- Creating PRs
- Code review process
- Addressing feedback
- Merging

Move to **Module 08: GitHub Repository Settings and Access Control** to manage team permissions.

---

**Time to Complete:** 45 minutes  
**Difficulty Level:** Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
