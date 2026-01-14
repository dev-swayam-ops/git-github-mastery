# 12-collaboration-labs-and-scenarios: Cheatsheet

## Team Workflow Checklist

### Daily
- [ ] Pull latest develop/main
- [ ] Review open PRs
- [ ] Respond to code review comments
- [ ] Push changes regularly

### Per Feature
- [ ] Create feature branch
- [ ] Keep branch updated
- [ ] Write PR description
- [ ] Request specific reviewers
- [ ] Address feedback

### Per Merge
- [ ] All tests passing
- [ ] Code review approved
- [ ] Conflicts resolved
- [ ] Documentation updated

## Git Flow Branches

| Branch | From | Purpose | Into |
|--------|------|---------|------|
| feature/* | develop | New features | develop |
| develop | main | Integration | main for release |
| release/* | develop | Prepare release | main + develop |
| hotfix/* | main | Production fixes | main + develop |

## Collaboration Commands

| Command | Purpose |
|---------|---------|
| `git fetch origin` | Get latest remote changes |
| `git rebase origin/develop` | Update your branch |
| `git merge --no-ff origin/develop` | Merge with history |
| `git cherry-pick <commit>` | Copy specific commit |
| `git log --graph --oneline` | Visualize branches |

## PR Review Checklist

- [ ] Code is understandable
- [ ] No obvious bugs
- [ ] Tests included
- [ ] Documentation updated
- [ ] Follows style guide
- [ ] Performance acceptable
- [ ] Security reviewed
- [ ] No hardcoded values

## Conflict Resolution Pattern

```bash
# 1. Start update
git fetch origin
git rebase origin/develop

# 2. View conflicts
git status

# 3. Edit files with <<<<<<

# 4. Resolve (keep both, choose one, etc.)

# 5. Add resolved
git add resolved-file.js

# 6. Continue
git rebase --continue

# 7. Push
git push origin branch --force-with-lease
```

## Multiple Release Support

| Version | Status | Support | Fixes |
|---------|--------|---------|-------|
| 2.0 | Current | Yes | All |
| 1.9 | Maintenance | Critical | Security only |
| 1.8 | EOL | No | None |

## Team Size Recommendations

| Size | Setup |
|------|-------|
| 1-2 | One branch per feature |
| 3-5 | Feature + develop branch |
| 5-20 | Git Flow recommended |
| 20+ | Multiple teams + Git Flow |

## Communication Best Practices

| Channel | Use |
|---------|-----|
| PR Comments | Code-specific feedback |
| Slack/Teams | General discussion |
| Issues | Bug tracking |
| Discussions | Architecture decisions |
| Email | Formal decisions |

## Code Review Standards

```
Positive tone:
✓ "Consider adding error handling here"
✓ "What about performance at scale?"
✓ "Nice implementation!"

✗ "This is wrong"
✗ "You should know this"

Response time:
- Same day for urgent
- Within 24 hours typical
- Within 48 hours maximum
```

## Common Collaboration Patterns

### Quick Fix
```bash
git checkout -b fix/typo develop
# Fix typo
git push && create PR
# Merge when approved
```

### Feature Development
```bash
git checkout -b feature/auth develop
# Multiple commits over days
# Keep updated with rebase
# Final PR when complete
```

### Release Cycle
```bash
git checkout -b release/2.0 develop
# Only bug fixes on release branch
# Merge to main when ready
# Tag and deploy
```

### Hotfix
```bash
git checkout -b hotfix/critical main
# Fix immediately
# Fast-track approval
# Merge to main + develop
```

## Metrics to Track

```
PR Statistics:
- Average review time: <24 hours
- Average merge time: <2 days
- % PRs with comments: 80%+
- % PRs blocked on tests: <10%

Team Velocity:
- Features completed per sprint
- Bug fixes completed per sprint
- Failed builds per day: <1
```

## Documentation Files

```
README.md
├─ Project overview
├─ Quick start
└─ Link to other docs

CONTRIBUTING.md
├─ How to contribute
├─ Development setup
└─ Code review process

DEVELOPMENT.md
├─ Architecture
├─ Design decisions
└─ Debugging tips

SECURITY.md
├─ Reporting vulnerabilities
├─ Security policy
└─ Supported versions
```

## Conflict Resolution Guide

| Conflict Type | Solution |
|---------------|----------|
| Same file edited differently | Manual merge, test thoroughly |
| File deleted vs edited | Decide if file needed |
| Rebased commits | Merge conflict markers appear |
| Directory conflicts | Rare, usually from rename |

## Retrospective Template

```markdown
## ✓ What Went Well
- Fast PR reviews
- Good test coverage
- Clear communication

## ✗ Pain Points
- Long build times
- Merge conflicts in shared files
- Unclear priorities

## 💡 Improvements
- Parallelize tests
- Weekly syncs on shared files
- Use labels for priority
```

## Emergency Response

```
CRITICAL BUG FOUND:
1. Create hotfix branch from main (2 min)
2. Fix issue (varies)
3. Fast-track review (10 min)
4. Deploy immediately (10 min)
5. Backport to develop (10 min)
Total: ~30 min from discovery to deployed + synced
```

## Tools Integration

```
GitHub ←→ Slack
      ←→ JIRA
      ←→ Analytics
      ←→ CI/CD (GitHub Actions)
      ←→ Deployment (various)
```

## Handoff Checklist

When team member leaves or takes time off:

- [ ] Document their work in progress
- [ ] Assign PRs to others
- [ ] Update project board
- [ ] Brief replacement
- [ ] Ensure continuity
