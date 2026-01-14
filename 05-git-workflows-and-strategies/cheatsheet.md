# Git Workflows and Strategies - Cheatsheet

## Git Flow Workflow

### Permanent Branches
- **main** - Production releases only
- **develop** - Integration branch for features

### Temporary Branches
- **feature/** - New features, branch from develop
- **release/** - Release preparation, branch from develop
- **hotfix/** - Production fixes, branch from main

### Git Flow Commands
```bash
# Feature
git switch -c feature/<name>
git switch develop
git merge feature/<name>

# Release
git switch -c release/<version>
# Fix bugs...
git switch main
git merge release/<version>
git tag v<version>
git switch develop
git merge release/<version>

# Hotfix
git switch -c hotfix/<issue>
git switch main
git merge hotfix/<issue>
git tag v<version>
git switch develop
git merge hotfix/<issue>
```

---

## GitHub Flow Workflow

### Simple, Continuous Deployment Friendly
1. Create feature branch from main
2. Make commits and push
3. Create Pull Request (covered in module 07)
4. Merge to main
5. Deploy from main

### Key Characteristics
- Main is always deployable
- Short-lived feature branches (hours to days)
- No release or hotfix branches
- Frequent releases from main

---

## Trunk-Based Development

### Strategy
- Single main branch (the trunk)
- Very short-lived branches (hours)
- Frequent small merges
- Continuous integration/deployment

### Benefits
- Reduced merge conflicts
- Easy to track changes
- Supports continuous deployment
- Developers stay current

### Challenges
- Requires feature flags for incomplete work
- Needs strong testing discipline
- All developers merge frequently

---

## Semantic Versioning

| Version | Meaning | When to Increment |
|---------|---------|-------------------|
| MAJOR.MINOR.PATCH | X.Y.Z | |
| 1.0.0 | Initial release | Breaking changes |
| 1.1.0 | New features | New features, backward compatible |
| 1.1.1 | Bug fixes | Bug fixes only |
| 2.0.0 | Major update | Breaking API changes |

### Tagging
```bash
git tag v1.0.0           # Lightweight tag
git tag -a v1.0.0 -m "Release 1.0.0"  # Annotated tag
git tag -l              # List tags
git show v1.0.0         # Show tag details
git push origin v1.0.0  # Push tag to remote
```

---

## Common Workflow Patterns

### Branch Naming Conventions
```
feature/<description>
feature/<ticket>-description
bugfix/<issue>
hotfix/<issue>
release/v<version>
docs/<topic>
refactor/<area>
```

### Commit Message Conventions
```
feat: Add user authentication
fix: Resolve payment validation bug
docs: Update API documentation
refactor: Simplify auth logic
test: Add unit tests for payment
chore: Update dependencies
```

---

## Workflow Decision Matrix

| Workflow | Team Size | Release Frequency | Complexity | Recommendation |
|----------|-----------|-------------------|------------|-----------------|
| GitHub Flow | Small | Frequent | Low | Startups, Simple Projects |
| Git Flow | Medium | Monthly | High | Enterprise, Complex Apps |
| Trunk-Based | Any | Continuous | Medium | CI/CD, Microservices |

---

## Integration Strategies

### Merge (Preserves History)
```bash
git merge feature/name
# Creates merge commit
# Shows branch structure
# Safe for shared branches
```

### Rebase (Linear History)
```bash
git rebase main
git merge --ff feature/name
# Rewrites history
# Cleaner log
# Only for private branches
```

### Squash (Combine Commits)
```bash
git merge --squash feature/name
git commit -m "Merge feature/name"
# Combines all commits
# Single commit on main
# Useful for cleanup
```

---

## Feature Toggles / Feature Flags

### Implementation Pattern
```python
if os.getenv('ENABLE_NEW_FEATURE') == 'true':
    use_new_implementation()
else:
    use_old_implementation()
```

### Benefits
- Deploy without releasing
- A/B testing
- Gradual rollouts
- Quick rollback
- Reduce time in branches

### Cleanup
- Remove feature flags when stable
- Keep flags for monitoring
- Document active flags

---

## Tips for Choosing Workflow

1. **Team Size & Distribution**
   - Small local team → simpler workflow
   - Large distributed → more structure needed

2. **Release Frequency**
   - Continuous → trunk-based, GitHub flow
   - Monthly/quarterly → Git flow with releases

3. **Complexity**
   - Monolith → more structure (Git flow)
   - Microservices → simpler (trunk-based)

4. **Development Culture**
   - Code review focused → pull requests
   - Integration focused → trunk-based
   - Release focused → Git flow

5. **Deployment Process**
   - Automated deployment → trunk-based, GitHub flow
   - Manual deployment → Git flow

---

## Common Anti-Patterns to Avoid

1. **Long-lived branches** - Hard to merge, outdated
2. **Merging to wrong branch** - Hotfixes only to main and develop
3. **Skipping release branches** - Use them for preparation
4. **No tagging** - Always tag releases
5. **Merging without testing** - Review before merge
6. **No branch protection** - Protect main and develop
7. **Complex branch names** - Keep them simple and consistent

