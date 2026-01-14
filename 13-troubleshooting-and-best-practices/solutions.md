# 13-troubleshooting-and-best-practices: Solutions

## Solution 1: Detached HEAD State

**Situation:**
```bash
git checkout abc1234  # Checkout specific commit
# HEAD is now at abc1234...
# You are in detached state
```

**Recovery:**
```bash
# Option 1: Create branch to save work
git branch recovery-branch
git checkout recovery-branch

# Option 2: Go back to main
git checkout main

# Option 3: Discard changes
git checkout main
```

**Prevention:**
- Always work on branches, not commits
- Use git switch for clarity
- Check `git status` before committing

---

## Solution 2: Recover Lost Commits

**Scenario:**
```bash
# Accidentally reset hard
git reset --hard HEAD~10
# Last 10 commits seem lost!
```

**Recovery:**
```bash
# View all recent actions
git reflog

# Output shows:
# abc1234 HEAD@{0}: reset: moving to HEAD~10
# def5678 HEAD@{1}: commit: feature work
# ghi9012 HEAD@{2}: commit: bugfix

# Recover to before reset
git reset --hard HEAD@{1}

# Or reset to specific commit found
git checkout -b recovered def5678
```

**Lesson:**
- Reflog stores all movements (even deletions)
- Commits rarely truly deleted
- Always use `--force-with-lease` not `--force`

---

## Solution 3: Fix Upstream Issues

**Problem:**
```bash
git push origin main
# error: failed to push

git pull origin main
# error: your current branch is behind
```

**Diagnosis & Fix:**
```bash
# Check remote status
git remote -v
git branch -vv

# Check if remote was reset
git fetch origin
git log --oneline origin/main

# Safe force push (only overwrites if no one else pushed)
git push origin main --force-with-lease

# Team communication
# Message: "Remote was reset. Please pull latest."
```

**Best Practices:**
- Communicate force pushes
- Use `--force-with-lease` always
- Document why force push was needed

---

## Solution 4: Handle Large Files

**Accidentally Committed:**
```bash
# Discovered after push:
# File is 500MB (should be ignored)

# Option 1: Remove from history (if not shared)
git filter-branch --tree-filter 'rm -f large-file.bin' HEAD

# Option 2: Using BFG (faster)
bfg --delete-files large-file.bin

# Step 1: Add to .gitignore
echo "large-file.bin" >> .gitignore

# Step 2: Force push
git push origin main --force-with-lease

# Step 3: Prevent future occurrences
# Create .gitignore entry for pattern
```

**Prevention:**
```
.gitignore examples:
*.iso
*.zip
node_modules/
.DS_Store
*.log
```

---

## Solution 5: Performance Optimization

**Check Size:**
```bash
# Repository size
du -sh .git

# Largest objects
git rev-list --all --objects | sort -k2 | tail -20

# Find large blobs
git gc
git count-objects -v
```

**Optimization:**
```bash
# Garbage collection
git gc --aggressive

# Prune unreachable objects
git reflog expire --expire=now --all
git gc --prune=now

# Clone shallow (fewer history)
git clone --depth 1 repo-url
```

**Maintenance:**
- Run gc regularly
- Keep .gitignore current
- Review large files
- Monitor .git size

---

## Solution 6: Fixing Collaborator Mistakes

**Scenario: Pushed to wrong branch**

**Step 1: Identify problem**
```bash
# Commits went to main instead of feature branch
git log --oneline main -5
# Shows: "feature work" commits that shouldn't be there
```

**Step 2: Fix (if not shared)**
```bash
# Revert the commits
git revert abc1234 def5678

# Or reset if very recent
git reset --soft HEAD~2
# Changes still in working directory
```

**Step 3: Create correct branch**
```bash
# From current state
git checkout -b feature/correct-branch
git commit -m "Move feature to correct branch"
git push origin feature/correct-branch
```

**Step 4: Communication**
```
Message to team:
"Accidentally pushed feature work to main.
Moved to feature/correct-branch.
Please review before merging."
```

---

## Solution 7: Complex Merge Scenarios

**Scenario: Multiple branches, selective merge**

```bash
# You need only specific commits from another branch
git cherry-pick abc1234  # Apply specific commit

# Or entire branch with conflict resolution
git merge feature/other --no-ff

# If you need different strategy
git merge -s recursive feature/other  # Default
git merge -s resolve feature/other    # Simpler
git merge -s ours feature/other       # Keep ours
git merge -s theirs feature/other     # Take theirs

# View merge without committing
git merge --no-commit --no-ff feature/other
# Review, then decide
git merge --continue  # or --abort
```

---

## Solution 8: Debugging CI/CD Failures

**Check Workflow Logs:**
```
GitHub > Actions > Select failed workflow > View logs
```

**Common Issues:**

1. **Test failure:**
```bash
# Reproduce locally first
npm test

# Fix locally
git add .
git commit -m "Fix failing test"
git push
# CI re-runs
```

2. **Build failure:**
```bash
# Check build logs for errors
# Usually missing dependencies or config

# Fix:
npm install  # Or equivalent
git add package-lock.json
git commit -m "Update dependencies"
```

3. **Deployment failure:**
```bash
# Check deployment credentials/secrets
# Verify environment variables set

gh secret set SECRET_NAME --body value
```

---

## Solution 9: Audit and Compliance

**Checklist:**
```bash
# 1. Branch protection
gh repo view --json 'branchProtectionRules'

# 2. Collaborators
gh repo view --json 'collaborators'

# 3. Recent commits
git log --oneline main -10

# 4. Security issues
gh repo view --json 'securityAlerts'

# 5. Large files
git rev-list --all --objects | sort -k2 | tail -5
```

**Documentation:**
```
Repository Audit Report:
- Protection: main branch protected ✓
- Reviews: 2 required ✓
- Status checks: Enabled ✓
- Collaborators: 5 approved ✓
- Security: No alerts ✓
- Large files: None found ✓
Date: 2024-01-15
Auditor: Alice
```

---

## Solution 10: Preventing Common Mistakes

**Pre-commit hooks: .git/hooks/pre-commit**
```bash
#!/bin/bash

# Prevent commit of unfinished code
if grep -r "TODO\|FIXME" --include="*.js" .; then
    echo "Found unresolved TODOs"
    exit 1
fi

# Run tests before commit
npm test
if [ $? -ne 0 ]; then
    echo "Tests failed, cannot commit"
    exit 1
fi

# Check for secrets
if grep -r "password\|api_key" --include="*.js" .; then
    echo "Found hardcoded secrets"
    exit 1
fi

# Lint code
npm run lint
```

**Using husky (modern approach):**
```bash
npm install husky
npx husky install

# Add hook
npx husky add .husky/pre-commit "npm test && npm run lint"
```

**Using commitlint:**
```bash
npm install @commitlint/cli

# Enforce commit message format
# Only "feat:", "fix:", "docs:" etc. allowed
```

---

## Best Practices Summary

✓ Use meaningful commit messages
✓ Commit frequently (small changes)
✓ Keep branches short-lived
✓ Review PRs thoroughly
✓ Test before pushing
✓ Use branches for features
✓ Protect main/production
✓ Document decisions
✓ Communicate with team
✓ Monitor repository health

✗ Don't force push to shared branches
✗ Don't commit secrets or large files
✗ Don't use vague commit messages
✗ Don't skip code reviews
✗ Don't let branches go stale
✗ Don't ignore CI/CD failures
✗ Don't delete branches after merge
✗ Don't commit commented code
✗ Don't work directly on main
✗ Don't ignore security warnings
