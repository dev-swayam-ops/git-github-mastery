# 05-git-workflows-and-strategies

## What You'll Learn

By the end of this module, you'll understand:
- Different branching strategies (Git Flow, GitHub Flow, Trunk-Based)
- When to use each strategy
- Release management strategies
- Hotfix procedures
- Integration strategies
- Pros and cons of each approach
- How to implement in your team

## Prerequisites

- Completion of Modules 01-04
- Understanding of branches and merging
- Familiarity with team workflows
- Basic DevOps concepts helpful

## Key Concepts

| Strategy | Best For | Key Branches |
|----------|----------|---------------|
| **Git Flow** | Large teams, versioned releases | main, develop, feature/*, release/*, hotfix/* |
| **GitHub Flow** | Continuous deployment | main, feature/* |
| **Trunk-Based** | High velocity, DevOps | main (single branch) |
| **Release Flow** | Software releases | main, release branches |

## Hands-on Lab: Implementing Git Flow Workflow

### Scenario
You're implementing Git Flow for a team working on multiple features with planned releases.

### Step-by-Step Commands

```bash
# Step 1: Create main and develop branches
git branch main
git branch develop
git push origin develop

# Step 2: Create feature branch
git checkout develop
git checkout -b feature/user-auth

# Step 3: Work on feature (multiple commits)
echo "auth code" > auth.py
git add auth.py
git commit -m "Add authentication module"

echo "# More auth logic" >> auth.py
git add auth.py
git commit -m "Add login validation"

# Step 4: Create PR and merge to develop
git push origin feature/user-auth
# Create PR on GitHub, get review, merge

# Step 5: Create release branch
git checkout develop
git checkout -b release/1.0.0

# Step 6: Only bug fixes on release
echo "1.0.0" > VERSION
git add VERSION
git commit -m "Bump version to 1.0.0"

# Step 7: Merge to main
git checkout main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Release 1.0.0"

# Step 8: Merge back to develop
git checkout develop
git merge --no-ff release/1.0.0

# Step 9: Delete release branch
git branch -d release/1.0.0
```

### Expected Output

```
Branch develop created
Branch release/1.0.0 created
Merge made by 'recursive' strategy
Tag v1.0.0 created
```

## Validation

You've successfully completed this lab if:
- ✓ Created main and develop branches
- ✓ Created feature branch from develop
- ✓ Merged feature back to develop
- ✓ Created release branch
- ✓ Merged release to main
- ✓ Created version tag
- ✓ Synced release back to develop

## Cleanup

```bash
rm -f auth.py VERSION
git add .
git commit -m "Cleanup: Remove test files"
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Merging feature directly to main | Skips review cycle | Merge to develop first always |
| Forgetting to sync release back | Develop gets out of sync | Merge release branch to both main and develop |
| Hotfixing from develop | Fix only in one branch | Always hotfix from main |
| Too many long-lived branches | Integration chaos | Keep feature branches short (<1 week) |
| No clear version tagging | Can't track releases | Tag every release version |

## Troubleshooting

**Q: Which workflow should my team use?**
- A: Git Flow for larger teams with versioning; GitHub Flow for continuous deployment; Trunk-Based for high velocity

**Q: How long should feature branches exist?**
- A: Ideally < 1 week. Long branches = merge conflicts

**Q: What if we need production hotfix during development?**
- A: Git Flow handles this: create hotfix/* from main, merge to both main and develop

**Q: Do we need a develop branch?**
- A: Not for GitHub Flow or Trunk-Based. Optional for Git Flow. Choose based on release cycle

**Q: How do we coordinate multiple releases?**
- A: Multiple release/* branches simultaneously, or one at a time with discipline

## Next Steps

Once comfortable with:
- Different workflow strategies
- Branch organization
- Release management
- Merging patterns

Move to **Module 06: Tags, Releases and Versioning** to master version management.

---

**Time to Complete:** 50 minutes  
**Difficulty Level:** Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
