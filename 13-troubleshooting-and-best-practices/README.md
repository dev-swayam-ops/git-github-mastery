# 13-troubleshooting-and-best-practices

## What You'll Learn

By the end of this module, you'll understand:
- Common Git errors and solutions
- Data recovery techniques
- Performance optimization
- Best practices for teams
- Commit message standards
- Workflow discipline
- Prevention strategies

## Prerequisites

- Completion of Modules 01-12
- Experience with Git problems
- Desire to prevent future issues

## Key Concepts

| Problem | Cause | Solution |
|---------|-------|----------|
| **Lost Commits** | Reset/rebase mistake | Use git reflog to recover |
| **Wrong Branch Merge** | Operator error | git revert or cherry-pick |
| **Detached HEAD** | Checking out commit | git switch - to return |
| **Merge Conflicts** | Overlapping changes | Resolve and test |
| **Large Files** | Binary/media commits | Use Git LFS |
| **Slow Clones** | Large history | git clone --depth 1 |
| **Accidental Commits** | Committed wrong files | git reset --soft HEAD~1 |

## Hands-on Lab: Recovering from Common Mistakes

### Scenario
You've made various Git mistakes and need to recover from them.

### Step-by-Step Commands

```bash
# SCENARIO 1: Lost commits
git clone <repo>
cd <repo>

# Make commits
echo "commit 1" > file1.txt
git add file1.txt
git commit -m "Commit 1"

echo "commit 2" > file2.txt
git add file2.txt
git commit -m "Commit 2"

# Accidentally reset
git reset --hard HEAD~2

# Recover using reflog
git reflog
# Find the commit hash
git reset --hard <commit-hash>

# SCENARIO 2: Wrong branch merge
git checkout develop
git merge feature-wrong  # Oops, wrong branch!

# Revert the merge
git revert -m 1 HEAD

# Or reset if not pushed
git reset --hard HEAD~1

# SCENARIO 3: Committed wrong files
echo "secret" > secrets.txt
git add secrets.txt
git add config.txt
git commit -m "Add configs"

# Undo commit, keep changes
git reset --soft HEAD~1

# Remove secrets
git reset secrets.txt
rm secrets.txt

# Recommit
git commit -m "Add configs"

# SCENARIO 4: Detached HEAD
git checkout <commit-hash>
# Now in detached HEAD state

# Create branch before losing changes
git branch recovery-branch

# Return to main branch
git checkout main

# Merge recovery branch if needed
git merge recovery-branch

# SCENARIO 5: Large file committed
echo "large binary data" > huge.bin
git add huge.bin
git commit -m "Add large file"

# Remove from history
git rm --cached huge.bin
git commit --amend

# Or use filter-branch for already-pushed
git filter-branch --tree-filter 'rm -f huge.bin' HEAD

# SCENARIO 6: Merge conflict
git checkout feature/api
echo "version 2" > api.py
git add api.py
git commit -m "Update API"

git checkout develop
echo "version 1" > api.py
git add api.py
git commit -m "Add API"

# Try to merge
git merge feature/api
# CONFLICT!

# Resolve conflict
# Edit api.py, keep desired version
git add api.py
git commit -m "Resolve conflict"

# SCENARIO 7: Slow performance
# Check repository size
git gc --aggressive

# Shallow clone
git clone --depth 1 <repo>

# Sparse checkout
git sparse-checkout init
git sparse-checkout set src/
```

### Expected Output

```
[Scenario 1] Commits recovered
[Scenario 2] Merge reverted
[Scenario 3] File removed from commit
[Scenario 4] Branch created from detached HEAD
[Scenario 5] Large file removed from history
[Scenario 6] Conflict resolved
[Scenario 7] Repository optimized
```

## Validation

You've successfully completed this lab if:
- ✓ Recovered lost commits using reflog
- ✓ Reverted incorrect merge
- ✓ Fixed wrong committed files
- ✓ Escaped detached HEAD
- ✓ Handled merge conflicts
- ✓ Recovered from force push
- ✓ Optimized repository

## Cleanup

```bash
rm -f file1.txt file2.txt secrets.txt huge.bin
rm -rf .git
git init
```

## Common Mistakes

| Mistake | Prevention | Recovery |
|---------|-----------|----------|
| Force push without backup | Don't use -f, use --force-with-lease | Use reflog |
| Delete branch with unpushed commits | Check branch status before delete | reflog works for ~30 days |
| Wrong rebase | Use --onto carefully | Reset and try again |
| Accidental amend | Check what you're amending | reflog |
| Private key in commit | Pre-commit hooks, scanning | Rotate key, remove from history |

## Best Practices

1. **Commit Messages**: Clear, concise, imperative mood
   - Bad: "fixed stuff"
   - Good: "Fix user authentication error on login"

2. **Branch Naming**: Consistent convention
   - feature/description
   - bugfix/description
   - hotfix/description
   - release/version

3. **Commit Frequency**: Small, logical changes
   - Easier to review
   - Easier to revert if needed
   - Better history

4. **Team Standards**:
   - Agree on workflow (Git Flow, GitHub Flow, etc.)
   - Enforce via branch protection
   - Require PR reviews
   - Document in CONTRIBUTING.md

5. **Testing**:
   - Test before committing
   - Test before pushing
   - Test before merging
   - Automate with CI/CD

## Troubleshooting

**Q: How long can I recover commits with reflog?**
- A: Default 90 days. Check: git config gc.reflogexpire

**Q: Can I recover after git push origin --force?**
- A: If others pulled, they have it. Otherwise, ask server admin

**Q: What's the difference between reset, revert, restore?**
- A: reset changes HEAD, revert creates new commit, restore changes files

**Q: How do I prevent large files?**
- A: Pre-commit hooks, .gitignore, or use Git LFS

**Q: What if repository is corrupted?**
- A: Use git fsck to find issues. Restore from backup if needed

## Next Steps

Once comfortable with:
- Troubleshooting
- Recovery techniques
- Prevention strategies
- Best practices

Move to **Module 14: Cheatsheets and Interview Notes** for quick reference.

---

**Time to Complete:** 60 minutes  
**Difficulty Level:** Advanced  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
