# 13-troubleshooting-and-best-practices: Cheatsheet

## Common Problems & Solutions

| Problem | Cause | Solution |
|---------|-------|----------|
| Detached HEAD | Checked out commit instead of branch | `git checkout main` |
| Lost commits | Reset --hard | Use `git reflog` to recover |
| Merge conflict | Concurrent edits same file | Manually resolve, add, commit |
| "origin not found" | Wrong remote name | Check with `git remote -v` |
| Can't push | Branch protection or sync issue | Pull first, then push |
| Can't pull | Uncommitted changes | Commit or stash first |

## Recovery Commands

```bash
# View all recent changes
git reflog

# Recover to specific point
git reset --hard HEAD@{N}

# Recover deleted branch
git reflog
git checkout -b branch-name SHA

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Undo published commit (safe)
git revert HEAD
```

## Debugging Commands

```bash
# Check current state
git status
git log --oneline

# See what changed
git diff
git diff --cached
git show <commit>

# Check remotes
git remote -v
git branch -vv

# View reflog (history of movements)
git reflog
git log -g

# Find commits with keyword
git log --grep="bugfix"
git log -S "variable_name"
```

## Pre-commit Hooks Setup

```bash
# Create hook file
cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
npm test
npm run lint
EOF

# Make executable
chmod +x .git/hooks/pre-commit

# Modern: Use husky
npm install husky
npx husky install
npx husky add .husky/pre-commit "npm test"
```

## Large File Handling

```bash
# Check size
du -sh .git
git count-objects -v

# Find large files
git rev-list --all --objects | sort -k2 | tail -10

# Remove from history
git filter-branch --tree-filter 'rm -f large-file.bin'
bfg --delete-files large-file.bin

# Prevent in future
echo "*.iso" >> .gitignore
echo "node_modules/" >> .gitignore
```

## Performance Optimization

```bash
# Garbage collection
git gc
git gc --aggressive

# Prune old data
git reflog expire --expire=now --all
git gc --prune=now

# Shallow clone (faster)
git clone --depth 1 <url>

# Partial clone (sparse checkout)
git clone --sparse <url>
```

## Security Best Practices

| Practice | Command | Benefit |
|----------|---------|---------|
| Sign commits | `git commit -S` | Verify author |
| Prevent secrets | `git secrets` | Catch leaks |
| Rotate tokens | Periodic | Limit exposure |
| Review logs | `git log` | Audit activity |
| Branch protect | GitHub UI | Enforce process |

## Conflict Resolution Steps

```bash
# 1. Start merge/rebase
git merge/rebase branch

# 2. View conflicts
git status

# 3. Edit conflicted files
# Remove conflict markers:
# < < < < < < <  ours
# = = = = = = =
# > > > > > > >  theirs

# 4. Mark resolved
git add resolved-file

# 5. Complete
git merge --continue
# or
git rebase --continue

# 6. Push
git push origin branch
```

## Branch Protection Configuration

```yaml
# For main/production
✓ Require pull request reviews (2)
✓ Require status checks to pass
✓ Require branches to be up to date
✓ Require conversation resolution
✓ Require signed commits
✓ Restrict push access
✗ Allow force pushes
✗ Allow deletions
```

## CI/CD Debugging

```bash
# Check workflow status
gh workflow list
gh run list

# View specific run
gh run view <run-id>

# Re-run workflow
gh run rerun <run-id>

# View logs
gh run view <run-id> --log

# Cancel run
gh run cancel <run-id>
```

## Common Git Patterns

### Update local branch
```bash
git fetch origin
git rebase origin/main
# or
git pull --rebase
```

### Undo recent changes
```bash
git reset --soft HEAD~N    # Keep changes
git reset --hard HEAD~N    # Discard changes
git revert HEAD            # Create undo commit
```

### Move commits between branches
```bash
git cherry-pick <commit>
git rebase --onto new-base old-base
```

### Fix commit mistakes
```bash
git commit --amend                          # Change last commit
git commit --amend --no-edit                # Add files to last commit
git rebase -i HEAD~N                        # Reorder/fix multiple
```

## Audit & Compliance

```bash
# View audit log
git log --format="%h %an %ae %ad %s" --date=short

# Export audit log
gh api repos/owner/repo/events > audit.json

# Check who changed what
git blame <file>

# View commits by author
git log --author="Name"
```

## Performance Monitoring

| Metric | Command | Target |
|--------|---------|--------|
| Repo size | `du -sh .git` | <100MB |
| Objects count | `git count-objects` | <1M |
| Large files | `git rev-list...` | None >50MB |
| Branch count | `git branch` | <50 |
| Stale branches | `git branch -vv` | <10 |

## Emergency Response

```
CRITICAL ISSUE:
1. Hotfix branch from main (1 min)
2. Fix code (varies)
3. Force merge (2 min)
4. Deploy (5 min)
5. Backport to develop (2 min)

Total: ~10-15 minutes
```

## Maintenance Schedule

| Task | Frequency |
|------|-----------|
| Garbage collection | Weekly |
| Delete stale branches | Weekly |
| Review collaborators | Monthly |
| Audit permissions | Monthly |
| Update dependencies | Ongoing |
| Review security alerts | Daily |

## Warning Signs

🚨 Repository health issues:
- Slow clone/pull times
- Push failures
- Merge conflicts increasing
- CI/CD timeouts
- Stale branches accumulating
- Large .git directory
- Security alerts

💡 Solutions:
- Run `git gc`
- Delete old branches
- Archive old releases
- Split large repository
- Review and fix security issues
