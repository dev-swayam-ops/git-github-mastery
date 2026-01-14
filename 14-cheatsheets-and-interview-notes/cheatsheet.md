# 14-cheatsheets-and-interview-notes: Cheatsheet

## Complete Git Command Reference

### Setup & Configuration
```bash
git config --global user.name "Name"
git config --global user.email "email@example.com"
git config --global core.editor "vim"
git config --list
```

### Repository Initialization
```bash
git init                          # Initialize new repo
git clone <url>                   # Clone existing repo
git clone <url> <directory>       # Clone to specific directory
git remote add <name> <url>       # Add remote
git remote -v                     # View remotes
```

### Daily Workflow
```bash
git status                        # Check status
git add <file>                    # Stage specific file
git add .                         # Stage all changes
git add -p                        # Interactive staging
git commit -m "message"           # Commit with message
git commit --amend                # Modify last commit
git push origin <branch>          # Push to remote
git pull origin <branch>          # Pull from remote
git fetch origin                  # Fetch without merging
```

### Branching
```bash
git branch                        # List local branches
git branch -a                     # List all branches
git branch <name>                 # Create branch
git checkout <branch>             # Switch branch
git checkout -b <branch>          # Create and switch
git switch <branch>               # Switch (newer syntax)
git merge <branch>                # Merge branch
git branch -d <branch>            # Delete branch
git branch -D <branch>            # Force delete
git branch -m <old> <new>         # Rename branch
```

### History & Inspection
```bash
git log                           # View history
git log --oneline                 # Compact history
git log --graph --oneline --all   # Visual graph
git log -p                        # Full patch
git log --stat                    # File statistics
git log --author="Name"           # Filter by author
git log --grep="text"             # Filter by message
git diff                          # Unstaged changes
git diff --cached                 # Staged changes
git diff <branch1> <branch2>      # Compare branches
git show <commit>                 # View commit details
git blame <file>                  # See who changed what
```

### Undo & Recovery
```bash
git restore <file>                # Discard changes (unstaged)
git restore --staged <file>       # Unstage file
git reset HEAD~1                  # Undo last commit (keep changes)
git reset --soft HEAD~1           # Soft reset
git reset --hard HEAD~1           # Hard reset (discard changes)
git revert <commit>               # Create undo commit
git reflog                        # View all actions
git reset --hard <ref>            # Go to specific ref
```

### Stashing
```bash
git stash                         # Save changes temporarily
git stash list                    # View stashed changes
git stash pop                     # Restore latest stash
git stash apply <id>              # Apply specific stash
git stash drop <id>               # Delete stash
```

### Merging & Rebasing
```bash
git merge <branch>                # Merge branch
git merge --no-ff <branch>        # Merge with commit
git merge --squash <branch>       # Squash commits
git rebase <branch>               # Rebase on branch
git rebase -i HEAD~N              # Interactive rebase
git rebase --continue             # Continue after conflict
git rebase --abort                # Cancel rebase
git cherry-pick <commit>          # Apply specific commit
```

### Tagging & Releases
```bash
git tag <name>                    # Create lightweight tag
git tag -a <name> -m "message"    # Create annotated tag
git tag -l                        # List tags
git show <tag>                    # View tag details
git push origin <tag>             # Push specific tag
git push origin --tags            # Push all tags
```

### Remote Operations
```bash
git remote add <name> <url>       # Add remote
git remote -v                     # View remotes
git remote remove <name>          # Remove remote
git remote rename <old> <new>     # Rename remote
git push origin <branch>          # Push branch
git push --all                    # Push all branches
git pull origin <branch>          # Pull and merge
git pull --rebase                 # Pull and rebase
git fetch                         # Fetch all
```

### Advanced
```bash
git bisect start                  # Start binary search for bug
git bisect bad                    # Mark as bad
git bisect good                   # Mark as good
git grep "text"                   # Search in repo
git log -S "text"                 # Find commits changing text
git filter-branch                 # Rewrite history (dangerous!)
git gc                            # Garbage collection
```

## GitHub Features Summary

### Authentication
- Personal access tokens
- SSH keys
- OAuth apps
- SAML SSO
- GitHub CLI

### Repository Management
- Settings (description, visibility)
- Collaborators (roles)
- Teams
- Deploy keys
- Webhooks

### Code Review
- Pull requests
- Code reviews
- Comments & suggestions
- Approve/request changes
- Merge strategies

### Branch Protection
- Require PR reviews
- Require status checks
- Require signed commits
- Require code owners
- Dismiss stale reviews

### Automation
- GitHub Actions
- Workflows
- Triggers
- CI/CD
- Scheduled jobs

### Security
- Secret scanning
- Dependabot alerts
- CodeQL analysis
- Vulnerability reports
- Audit logs

---

## Interview Quick Reference

### Git Basics (Answer in < 1 minute)
| Question | Answer |
|----------|--------|
| What is Git? | Distributed version control system |
| What is a commit? | Snapshot of project with message and metadata |
| What is a branch? | Independent line of development |
| What is a merge? | Combining changes from two branches |
| Difference between add and commit? | add stages, commit saves to history |

### Workflows
| Strategy | Best For |
|----------|----------|
| Git Flow | Large teams, multiple versions |
| GitHub Flow | Continuous deployment, simple projects |
| Trunk-Based | High velocity, feature flags |

### Commands to Know
```bash
# Daily work
git status, add, commit, push, pull

# Branching
git branch, checkout, merge

# Fixing mistakes
git restore, reset, revert

# Collaboration
git fetch, pull, push, merge

# Investigation
git log, diff, show, blame
```

### Common Scenarios
| Scenario | Command |
|----------|---------|
| Undo uncommitted changes | `git restore <file>` |
| Undo last commit | `git reset --soft HEAD~1` |
| Save work temporarily | `git stash` |
| Find lost commits | `git reflog` |
| Recover from mistake | `git reset --hard <ref>` |

### Best Practices
✓ Meaningful commit messages
✓ Small, focused commits
✓ Review before pushing
✓ Keep branches short-lived
✓ Merge frequently
✓ Test before committing
✓ Use branches for isolation
✓ Protect production code

---

## Quick Decision Trees

### Should I commit this?
```
Is it a logical change? → YES → Is it tested? → YES → COMMIT
                        → NO → Split into smaller changes
                                          → NO → Add tests first
```

### Which branching strategy?
```
Continuous deployment? → YES → GitHub Flow
Multiple versions? → YES → Git Flow
High velocity startup? → YES → Trunk-Based
Large enterprise? → YES → Git Flow
```

### How to undo?
```
Not staged? → git restore
Staged? → git restore --staged
Committed locally? → git reset --soft HEAD~1
Pushed to shared? → git revert
Lost commits? → git reflog
```

---

## Common Interview Answers

**Q: Explain your Git workflow**
A: I use Git Flow with feature branches. Create feature branches from develop, make commits with clear messages, create PR for review, address feedback, and merge. Keep commits small and logical.

**Q: What's your approach to merge conflicts?**
A: I prevent them by pulling regularly and keeping branches short-lived. When conflicts occur, I communicate with teammates, resolve manually while understanding both changes, test after resolution, and document the decision.

**Q: How do you ensure code quality?**
A: I use branch protection requiring PR reviews and status checks (tests, linting). CI/CD runs tests automatically. Code owners review critical changes. I also use pre-commit hooks to catch issues locally.

**Q: Describe your CI/CD setup**
A: I use GitHub Actions to run tests on every push and PR. If tests pass, build Docker image. If on main, deploy to staging. After manual approval, deploy to production. Full audit trail in Git history.

**Q: How do you handle production issues?**
A: Create hotfix branch from main (not develop) to fix issue immediately. Fast-track review (5 min). Deploy quickly. Then merge back to both main and develop to keep in sync. Tag release.

---

## Study Timeline

### Week 1: Basics
- Git fundamentals
- Basic commands
- First commits/branches
- Pushing/pulling

### Week 2: Workflows
- Branching strategies
- Merging vs rebasing
- Code review process
- PR workflow

### Week 3: Advanced
- Conflict resolution
- History rewriting
- Git internals
- Performance optimization

### Week 4: GitHub & DevOps
- GitHub features
- GitHub Actions
- Security features
- Real-world scenarios

### Week 5: Interview Prep
- Answer 100+ questions
- Solve scenarios
- Build portfolio
- Practice whiteboard

---

## Resources

### Documentation
- Git official: https://git-scm.com
- GitHub docs: https://docs.github.com
- Atlassian tutorials: https://www.atlassian.com/git

### Practice
- GitHub Learning Lab
- Interactive tutorials
- Create sample projects
- Contribute to open source

### Tools
- GitHub Desktop (GUI)
- GitKraken (visual)
- SourceTree (visual)
- VS Code Git extension

---

## Success Checklist

Before interviews, you should:
- [ ] Know all Git commands by heart
- [ ] Explain concepts clearly
- [ ] Solve scenarios quickly
- [ ] Understand workflows
- [ ] Know GitHub features
- [ ] Have GitHub portfolio
- [ ] Practice whiteboard explanations
- [ ] Understand DevOps integration
- [ ] Know security best practices
- [ ] Feel confident discussing git workflows
