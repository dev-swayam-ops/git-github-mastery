# 12-collaboration-labs-and-scenarios

## What You'll Learn

By the end of this module, you'll understand:
- Real-world team collaboration workflows
- Handling merge conflicts
- Code review communication
- Team coordination with Git
- Release coordination
- Simultaneous feature development
- Git Flow in practice

## Prerequisites

- Completion of Modules 01-11
- Understanding of all previous concepts
- Basic team collaboration experience

## Key Concepts

| Scenario | Challenge | Solution |
|----------|-----------|----------|
| **Parallel Features** | Teams working independently | Feature branches + develop |
| **Merge Conflict** | Same file modified twice | Resolve, test, merge |
| **Shared Release** | Coordinating version release | Release branch discipline |
| **Code Review** | Quality without blocking | PR discussions, suggestions |
| **Hotfix** | Production bug while developing | Hotfix branch from main |
| **Long-lived Branch** | Feature takes 2+ weeks | Keep up to date with develop |

## Hands-on Lab: Team Git Flow Workflow

### Scenario
You're part of a 3-person team working simultaneously. You need to handle features, reviews, and releases together.

### Step-by-Step Commands

```bash
# SETUP: Simulate 3 team members
# Dev 1: Alice (api-team)
# Dev 2: Bob (frontend-team)
# Dev 3: Carol (ops)

# Step 1: Initialize team repository structure
git clone <repo>
cd <repo>
git checkout develop
git pull origin develop

# Step 2: Alice creates feature branch
git checkout -b feature/user-api
echo "# User API endpoints" > api/users.py
echo "def get_users(): return []" >> api/users.py
git add api/users.py
git commit -m "Add user API endpoints"
git push origin feature/user-api
# Alice creates PR

# Step 3: Bob creates different feature branch
git fetch origin
git checkout develop
git checkout -b feature/dashboard
echo "# Dashboard UI" > ui/dashboard.js
echo "function Dashboard() { return <div></div>; }" >> ui/dashboard.js
git add ui/dashboard.js
git commit -m "Add dashboard component"
git push origin feature/dashboard
# Bob creates PR

# Step 4: Carol reviews Alice's PR
git fetch origin
git checkout feature/user-api
# View changes, add comments
# Approve PR

# Step 5: Alice addresses feedback
git checkout feature/user-api
echo "def get_user(id): return {id: id}" >> api/users.py
git add api/users.py
git commit -m "Add single user endpoint"
git push origin feature/user-api

# Step 6: Carol approves, Alice merges to develop
# GitHub: Merge PR to develop
git checkout develop
git pull origin develop

# Step 7: Bob updates branch (to avoid conflicts)
git checkout feature/dashboard
git pull origin develop
# Resolve any conflicts

# Step 8: Bob's PR gets review and merges
git checkout develop
git pull origin develop

# Step 9: Carol creates release
git checkout develop
git checkout -b release/1.0.0
echo "1.0.0" > VERSION
git add VERSION
git commit -m "Release 1.0.0"
git push origin release/1.0.0

# Step 10: Merge release to main
git checkout main
git pull origin main
git merge --no-ff release/1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin main
git push origin v1.0.0

# Step 11: Merge back to develop
git checkout develop
git pull origin develop
git merge --no-ff release/1.0.0
git push origin develop

# Step 12: Delete release branch
git branch -d release/1.0.0
git push origin --delete release/1.0.0
```

### Expected Output

```
[Alice] Feature branch created: feature/user-api
[Bob] Feature branch created: feature/dashboard
[Carol] Review: approved
[Alice] Addressed feedback
[Alice] Merged to develop
[Bob] Merged to develop
[Carol] Release branch created: release/1.0.0
[Carol] Released v1.0.0
```

## Validation

You've successfully completed this lab if:
- ✓ Created multiple feature branches
- ✓ Handled PR reviews and feedback
- ✓ Merged multiple features to develop
- ✓ Updated features with upstream changes
- ✓ Created release branch
- ✓ Tagged version
- ✓ Merged release to both main and develop

## Cleanup

```bash
git checkout main
rm -f VERSION
rm -rf api ui
git add .
git commit -m "Cleanup: Remove scenario files"
git push origin main
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Feature branch not synced | Conflicts multiply | git pull origin develop frequently |
| Merge develop into feature | History pollution | Merge feature → develop, not vice versa |
| Skipping code review | Low quality code | Always require review |
| Large PRs | Hard to review | Keep features small |
| Force push after review | Invalid review | Gentle push with new commits |

## Troubleshooting

**Q: How do we handle conflicts between features?**
- A: Merge feature to develop first (first one wins). Others pull and resolve

**Q: What if feature takes 2 weeks?**
- A: Sync with develop weekly, resolve conflicts early

**Q: Can multiple people work on same feature?**
- A: Yes, but use sub-branches: feature/user-api, feature/user-api/auth, feature/user-api/validation

**Q: What if we need hotfix during release?**
- A: Create hotfix from main, merge to both main and develop

**Q: How do we coordinate timing?**
- A: Standup meetings, GitHub project boards, clear PR descriptions

## Next Steps

Once comfortable with:
- Team collaboration
- Real workflows
- Conflict resolution
- Release coordination

Move to **Module 13: Troubleshooting and Best Practices** to handle problems.

---

**Time to Complete:** 60 minutes  
**Difficulty Level:** Advanced  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
