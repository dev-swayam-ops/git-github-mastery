# 02-git-branching-and-merging

## What You'll Learn

By the end of this module, you'll understand:
- How to create and switch between branches
- Different branching strategies (feature branches, Git Flow)
- How to merge branches cleanly
- How to resolve merge conflicts
- Best practices for branch naming and organization
- How branches enable parallel development

## Prerequisites

- Completion of Module 01 (Git Basics)
- Understanding of commits and repositories
- Comfortable with basic Git commands

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Branch** | Independent line of development |
| **Checkout** | Switch between branches |
| **Merge** | Combine changes from two branches |
| **Merge Conflict** | When Git can't auto-merge changes |
| **Fast-Forward Merge** | Linear merge without merge commit |
| **3-Way Merge** | Merge creating new merge commit |
| **Feature Branch** | Branch for single feature development |
| **Default Branch** | Main branch (usually main or master) |

## Hands-on Lab: Creating and Merging Branches

### Scenario
You're developing a user authentication feature. You'll create a feature branch, make changes, and merge back to main safely.

### Step-by-Step Commands

```bash
# Step 1: Check current branch
git branch

# Step 2: Create feature branch
git branch feature/auth

# Step 3: Switch to feature branch
git checkout feature/auth

# Step 4: Make changes
echo "def login(username, password):" > auth.py
echo "    return authenticate(username, password)" >> auth.py

# Step 5: Commit changes
git add auth.py
git commit -m "Add login function to authentication module"

# Step 6: Switch back to main
git checkout main

# Step 7: Verify main is clean
git status

# Step 8: Merge feature branch
git merge feature/auth

# Step 9: View merge result
git log --oneline

# Step 10: Delete feature branch
git branch -d feature/auth
```

### Expected Output

```
branch 'feature/auth' set up to track 'origin/feature/auth'.
Switched to a new branch 'feature/auth'

[feature/auth abc1234] Add login function
 1 file changed, 2 insertions(+)

Updating abc1234..def5678
Fast-forward
 auth.py | 2 ++
 1 file changed, 2 insertions(+)

Deleted branch feature/auth (was def5678)
```

## Validation

You've successfully completed this lab if:
- ✓ Created feature branch from main
- ✓ Made changes on feature branch
- ✓ Switched between branches without losing work
- ✓ Merged changes back to main
- ✓ Branch was deleted after merge
- ✓ Main branch now has the new changes

## Cleanup

```bash
# Delete test files
rm -f auth.py
git add .
git commit -m "Cleanup: Remove test files"
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Forgetting to switch branches | Changes go to wrong branch | Create branch from current state, switch, try again |
| Deleting active branch | Can't delete checked out branch | Switch to different branch first |
| Merging into wrong branch | Changes in unwanted location | Use git reset to undo |
| Not pulling before merge | Conflicts with remote changes | Always git pull before merge |
| Merge conflict panic | Not resolving properly | Take time, understand both changes, test after |

## Troubleshooting

**Q: I made changes on main but wanted feature branch**
- A: Create branch from current main, switch to it. Changes stay in working directory.

**Q: How do I see what's different between branches?**
- A: Use `git diff main feature/auth` to see differences

**Q: Merge failed with conflicts**
- A: Edit conflicted files, `git add .`, then `git commit` to complete merge

**Q: Can I rename a branch?**
- A: Yes! `git branch -m old-name new-name`

**Q: What if I delete a branch by mistake?**
- A: Use `git reflog` to find the commit and recreate the branch

## Next Steps

Once comfortable with:
- Creating and switching branches
- Merging successfully
- Resolving basic conflicts

Move to **Module 03: Rewriting History and Recovery** to learn advanced Git techniques for fixing mistakes.

---

**Time to Complete:** 45 minutes  
**Difficulty Level:** Beginner-Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
