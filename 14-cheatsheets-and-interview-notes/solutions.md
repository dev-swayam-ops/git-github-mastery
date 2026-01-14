# 14-cheatsheets-and-interview-notes: Solutions

## Solution 1: Complete Git Command Reference

**Repository Setup**
```bash
git init                          # Initialize repo
git config user.name "Name"       # Set identity
git clone <url>                   # Clone repo
git remote add origin <url>       # Add remote
```

**Daily Workflow**
```bash
git status                        # Check status
git add <file>                    # Stage changes
git commit -m "message"           # Commit
git push origin <branch>          # Push to remote
git pull origin <branch>          # Pull from remote
```

**Branching**
```bash
git branch                        # List branches
git branch <name>                 # Create branch
git checkout <branch>             # Switch branch
git switch <branch>               # Switch (newer)
git merge <branch>                # Merge branch
git branch -d <branch>            # Delete branch
```

**History & Inspection**
```bash
git log                           # View history
git log --oneline                 # Compact history
git diff                          # Show changes
git show <commit>                 # Show commit details
git blame <file>                  # Show who changed what
```

**Undo & Recovery**
```bash
git restore <file>                # Discard changes
git reset HEAD~1                  # Undo commit
git revert <commit>               # Create undo commit
git reflog                        # View all actions
git cherry-pick <commit>          # Apply commit
```

---

## Solution 2: GitHub Features Recap

**Authentication & Access**
- Personal access tokens
- SSH keys
- OAuth applications
- SAML SSO

**Repository Management**
- Settings and configuration
- Visibility (public/private)
- Collaborators and teams
- Deploy keys

**Code Review**
- Pull requests
- Code reviews
- Comments and suggestions
- Merge strategies

**Protection & Security**
- Branch protection rules
- Status checks
- Secret scanning
- Dependabot alerts
- Security advisories

**Automation**
- GitHub Actions
- Workflows
- CI/CD pipelines
- Scheduled jobs

**Organization**
- Teams
- Project boards
- Discussions
- Wiki pages

---

## Solution 3: Basic Interview Questions & Answers

**Q1: What's the difference between Git and GitHub?**
A: Git is a version control system (software), GitHub is a cloud platform for hosting and collaborating on Git repositories.

**Q2: Explain git init**
A: git init initializes a new empty Git repository in the current directory, creating a .git folder to track changes.

**Q3: What's a commit?**
A: A commit is a snapshot of your project at a specific point, with changes, author info, timestamp, and message.

**Q4: What's the difference between git add and git commit?**
A: git add stages changes (prepares them), git commit saves staged changes to repository history.

**Q5: What's a branch?**
A: A branch is an independent line of development, allowing parallel work without affecting the main code.

**Q6: How do you merge branches?**
A: git merge combines changes from one branch into another, either fast-forward or creating a merge commit.

**Q7: What's a pull request?**
A: A PR requests to merge code changes, allowing review and discussion before integration.

**Q8: What's GitHub Actions?**
A: GitHub Actions automates tasks like testing and deployment when events occur (push, PR, schedule).

**Q9: What's branch protection?**
A: Rules that protect important branches by requiring reviews, status checks, and preventing force pushes.

**Q10: What's a merge conflict?**
A: When Git can't auto-merge because the same part of a file was edited differently in both branches.

---

## Solution 4: Intermediate Interview Questions

**Q1: Explain Git Flow branching strategy**
A: Git Flow uses main (production), develop (integration), feature/*, release/*, and hotfix/* branches, separating development from releases.

**Q2: What's the difference between rebase and merge?**
A: Merge creates a merge commit preserving history. Rebase replays commits on new base for linear history (risky on shared branches).

**Q3: How do you handle merge conflicts?**
A: Edit conflicted files to keep desired changes, run git add, then git merge/rebase --continue or commit.

**Q4: What's git reflog and when do you use it?**
A: git reflog shows all Git movements and allows recovery from mistakes like accidental resets by finding and resetting to lost commits.

**Q5: Explain semantic commit messages**
A: Structured format: `type(scope): subject` (e.g., "fix(auth): prevent XSS in login"). Enables automation, readability, and changelog generation.

**Q6: What's the CI/CD pipeline role?**
A: Automates testing, building, and deployment. GitHub Actions runs tests on every PR, blocking merge if tests fail.

**Q7: How do you secure sensitive data in GitHub?**
A: Use GitHub Secrets for API keys, Dependabot for vulnerability scanning, secret scanning to detect leaks, and branch protection for production.

**Q8: What's code ownership (CODEOWNERS)?**
A: File mapping approval requirements to specific users/teams. Ensures domain experts review changes to critical code.

**Q9: How do you manage multiple versions?**
A: Use release branches (release/1.0) for patch releases, merge critical fixes back to develop, tag releases, document support timelines.

**Q10: Explain stashing in Git**
A: `git stash` temporarily saves uncommitted changes, letting you switch branches. `git stash pop` restores them. Useful when interrupted.

---

## Solution 5: Advanced Interview Questions

**Q1: Design a Git workflow for a 50-person team**
A: Use Git Flow with develop and main. Teams work in feature branches, integrate to develop, release/versioning branches, hotfixes from main. Require PR reviews, status checks, code owners for critical areas.

**Q2: How would you handle a very large monorepo with multiple teams?**
A: Use sparse checkout/clone, code ownership per folder, separate CI checks per team, parallel workflows, consider splitting into smaller repos.

**Q3: Explain shallow vs full clones and trade-offs**
A: Shallow (--depth 1) clones only recent history (fast, small), full clones all history (slow, large). Use shallow for CI/CD, full for development.

**Q4: How do you handle large binary files in Git?**
A: Don't. Use Git LFS (Large File Storage) which stores pointers instead of actual files, or use separate storage (S3, artifact repos). This prevents repo bloat.

**Q5: What's the ideal commit message structure and why?**
A: Subject (50 chars), blank line, body (72 chars). Enables parsing for automation, changelogs, and git bisect. Imperative mood ("Add" not "Added") for consistency.

**Q6: Explain squash vs rebase vs merge and when to use each**
A: Squash (clean feature history), Rebase (linear history, risky on shared), Merge (preserves history, merge commits). Context depends on team preference and branch safety.

**Q7: How do you implement GitOps?**
A: Git is source of truth. Changes to repo automatically deploy. Tools like ArgoCD watch Git and sync infrastructure. Enables reproducible, auditable deployments.

**Q8: Design authentication for a distributed team with 2FA requirement**
A: Use GitHub as source of truth. Enforce 2FA organization-wide. Use SAML/SSO if enterprise. Issue personal access tokens with short expiry. Regular access audits.

**Q9: How do you prevent security incidents in Git workflow?**
A: Branch protection (require reviews, status checks), secret scanning, code owners, signed commits, audit logs, regular security scanning (CodeQL, Snyk), remove compromised commits with filter-branch.

**Q10: Explain Trunk-Based Development vs Feature Branching**
A: Trunk-Based: Single main branch, frequent small commits, feature flags for unreleased work. Less conflicts, faster feedback.
Feature Branching: Long-lived branches, integration after complete feature. Better isolation but harder merges.

---

## Solution 6: Scenario-Based Problem Solving

**Scenario 1: Production Bug Found**
```
Approach:
1. Create hotfix branch from main
2. Fix immediately
3. Fast-track code review (5 min)
4. Deploy to production (10 min)
5. Merge back to develop (ensure sync)
6. Tag release version
Total time: ~30 minutes
```

**Scenario 2: Merge Conflict Between Teams**
```
Analysis:
- Both teams edited same file
- Can't auto-merge
- Affects critical feature

Solution:
- Schedule sync meeting
- Manual resolution with both teams
- Keep both changes if possible
- Or compromise solution
- Add comments documenting decision
```

**Scenario 3: Accidentally Deleted Important Branch**
```
Recovery:
1. Check git reflog
2. Find deleted branch commit
3. git checkout -b recovered-branch abc1234
4. Verify content
5. No data lost, always recoverable
```

**Scenario 4: PR with Unrelated Changes**
```
Feedback:
- Ask to split into two PRs
- One per concern/feature
- Keeps git history clean
- Easier to review
- Easier to revert if needed
```

---

## Solution 7: Whiteboard Interview Practice

**Explain Git Workflow:**
```
    feature/auth ─── ✓ review ─── merge ─┐
                                          │
main ──────── develop ─────────────────────── merge ──► production
                                          │
    feature/payment ─── ✓ review ─── merge ─┘
```

**Merge Conflict Diagram:**
```
main:     A ─── B ─── C ─── D
          └─ E ─── F (merge conflict on line 10)
          
After resolution:
          A ─── B ─── C ─── D ─── G(merged)
          └─ E ─── F ─┘
```

**Branch Protection Model:**
```
Developer → Create PR → Status Checks (✓)
                      ↓
                  Code Review (✓ 2 required)
                      ↓
              Conversation Resolution (✓)
                      ↓
                  Merge to main
```

---

## Solution 8: DevOps Integration

**GitHub Actions in DevOps:**
- Automated testing on every push
- Docker image builds and pushes
- Infrastructure-as-Code validation
- Deploy to cloud (AWS, Azure, GCP)
- Kubernetes rollouts
- Database migrations
- Monitoring and alerting

**GitOps Pattern:**
- Git repository = source of truth
- Automatic sync of cluster state
- Tools: ArgoCD, Flux, Helm
- Rollback by reverting commit
- Full audit trail of changes

**Infrastructure as Code:**
- Terraform/CloudFormation in Git
- Changes via PRs
- Automated validation
- Dry runs before deploy
- Version control for infrastructure

---

## Solution 9: Real-World Case Studies

**GitHub Flow (GitHub.com)**
- Single main branch (always deployable)
- Feature branches
- PR review mandatory
- Deploy to production immediately after merge
- Thousands of merges daily

**Git Flow (Traditional Companies)**
- Separate develop and main
- Release planning cycle
- Stable production releases
- Hotfix management
- Supports multiple versions

**Trunk-Based Development (Google, Facebook)**
- Single main branch
- All commits within hours
- Feature flags for incomplete work
- Continuous deployment
- Requires excellent testing

---

## Solution 10: Interview Portfolio

**GitHub Profile:**
- [ ] Professional bio and picture
- [ ] Pinned repositories (3-5 best projects)
- [ ] README on profile
- [ ] Consistent commit history
- [ ] Well-documented projects
- [ ] Contributions graph (active)
- [ ] Following relevant people
- [ ] Stars interesting projects

**Sample Projects to Showcase:**
- [ ] Project with good branching strategy
- [ ] Project with comprehensive CI/CD
- [ ] Project with detailed documentation
- [ ] Project with active community/PRs
- [ ] DevOps-related automation

**During Interview:**
- Explain your projects confidently
- Show good commit messages
- Discuss your branching strategy
- Explain your Git workflows
- Show security practices
- Discuss lessons learned

---

## Interview Tips

✓ **DO:**
- Know Git commands by heart
- Explain concepts clearly
- Use real examples
- Show your work
- Ask clarifying questions
- Discuss trade-offs
- Admit when unsure
- Learn from mistakes

✗ **DON'T:**
- Memorize answers
- Use jargon without explaining
- Rush explanations
- Claim expertise you don't have
- Criticize other approaches
- Forget fundamentals
- Ignore soft skills
- Be defensive

---

## Common Interview Question Categories

1. **Git Fundamentals** (Basic)
   - What is Git?
   - Commit, branch, merge basics
   - Push/pull operations

2. **Workflows & Strategies** (Intermediate)
   - Git Flow vs GitHub Flow
   - Branching strategies
   - Release management

3. **DevOps & Automation** (Advanced)
   - CI/CD integration
   - GitHub Actions
   - Infrastructure as Code

4. **Problem Solving** (Advanced)
   - Real-world scenarios
   - Conflict resolution
   - Team collaboration

5. **Soft Skills** (All levels)
   - Communication
   - Collaboration
   - Problem-solving approach
   - Learning mindset
