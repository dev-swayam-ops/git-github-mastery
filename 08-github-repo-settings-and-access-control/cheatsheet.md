# 08-github-repo-settings-and-access-control: Cheatsheet

## Repository Settings Quick Access

| Setting | Location | Purpose |
|---------|----------|---------|
| Repository name/description | Settings > General | Display in search results |
| Visibility | Settings > General | Public, Private, Internal |
| Default branch | Settings > Branches | Branch for PRs and clones |
| Wiki | Settings > General | Enable/disable wiki pages |
| Projects | Settings > General | Enable/disable project boards |
| Discussions | Settings > General | Enable community discussions |

## Managing Collaborators

| Task | Command/Path | Purpose |
|------|--------------|---------|
| Add person | Settings > Collaborators > Add people | Grant individual access |
| Change role | Settings > Collaborators > Edit | Adjust permissions |
| Remove access | Settings > Collaborators > Remove | Revoke access |
| View invitations | Settings > Collaborators > Pending | See pending invites |
| Add team | Settings > Teams > Add team | Grant team access |

## Repository Roles & Permissions

| Role | Pull | Push | Admin | Best For |
|------|------|------|-------|----------|
| Read | ✓ | ✗ | ✗ | Viewers, auditors |
| Triage | ✓ | ✗ | Issues | Issue managers |
| Write | ✓ | ✓ | ✗ | Developers |
| Maintain | ✓ | ✓ | Limited | Team leads |
| Admin | ✓ | ✓ | ✓ | Owner/manager |

## Branch Settings

| Setting | Path | Use Case |
|---------|------|----------|
| Default branch | Settings > Branches | Controls initial branch |
| Branch protection | Settings > Branches > Add rule | Protect important branches |
| Require reviews | Settings > Branches > Rule details | Code review enforcement |
| Require status checks | Settings > Branches > Rule details | CI/CD validation |
| Require signatures | Settings > Branches > Rule details | Commit verification |
| Allow force pushes | Settings > Branches > Rule details | Prevent history rewrites |

## Branch Protection Rule Configuration

```yaml
Pattern: main
☑ Require pull request reviews before merging
  - Number of reviewers: 2
  - Dismiss stale PR approvals: ✓
  - Require review from owners: ✓
☑ Require status checks to pass before merging
  - Require branches to be up to date: ✓
☑ Require conversation resolution: ✓
☑ Require signed commits: ✓
☑ Dismiss stale reviews: ✓
☑ Require code owner review: ✓
☐ Allow force pushes
☐ Allow deletions
```

## Access Control Strategy

| Team Size | Recommended Setup |
|-----------|-----------------|
| Solo | Admin on main |
| 2-5 people | Individuals with Write role |
| 5-20 people | Teams with Write, Maintain roles |
| 20+ people | Teams with strict roles + branch protection |

## Common Webhook Events

| Event | Triggers | Use |
|-------|----------|-----|
| push | Code pushed | Deploy, notify |
| pull_request | PR actions | CI/CD, notifications |
| issues | Issue created/modified | Tracking, automation |
| release | Release published | Deploy, announcements |
| deployment | Deployment status | Notifications |

## GitHub CLI Commands

| Command | Purpose |
|---------|---------|
| `gh repo set-default` | Set default repository |
| `gh repo view` | View repository details |
| `gh repo edit` | Edit repository settings |
| `gh repo add-collaborator` | Add collaborator |
| `gh repo delete-collaborator` | Remove collaborator |
| `gh rule list` | List branch protection rules |
| `gh rule create` | Create protection rule |

## Security Checklist

- [ ] Visibility set correctly (Public/Private)
- [ ] Default branch protected
- [ ] Require PR reviews enabled
- [ ] Require status checks enabled
- [ ] Unnecessary collaborators removed
- [ ] Teams used for consistency
- [ ] Deploy keys for CI/CD (not personal tokens)
- [ ] Webhooks configured for integrations
- [ ] Audit logs reviewed periodically

## Permission Escalation Path

```
Read (Viewer)
   ↓
Triage (Issue Manager)
   ↓
Write (Developer)
   ↓
Maintain (Team Lead)
   ↓
Admin (Repository Owner)
```

## Quick Setup for New Repository

```bash
# Set description and visibility
gh repo edit --description "Project description" --visibility private

# Add team
gh repo add-team --team teamname --role write

# Add collaborator
gh repo add-collaborator --user username --permission write

# Create branch protection
gh rule create -b main --require-code-review-count 2 --require-status-checks
```

## Common Patterns

### Production Repository
- Private repository
- Strict branch protection on main
- Require 2 reviews
- Require status checks
- Admin-only merge
- Signed commits required

### Open Source Repository
- Public repository
- Basic PR requirement
- Allow community contributions
- Clear contributor guidelines
- Auto-merge for maintainers

### Team Project
- Private repository
- Teams for permissions
- Write access for developers
- Maintain for leads
- Require code owner approval

## Troubleshooting Access Issues

| Problem | Solution |
|---------|----------|
| User can't push | Check role (must be Write+), check branch protection |
| PR won't merge | Check status checks, reviews, branch protection |
| Can't delete branch | Branch protection enabled, use admin override |
| Webhook not firing | Check active status, verify payload URL, check logs |
| Deploy key not working | Ensure read/write scope set, key added to GitHub |

## Useful Settings for Teams

```
General:
- Description: Clear project purpose
- Website: Link to docs
- Default branch: main or develop
- Auto-delete head branches: ✓

Pull Requests:
- Auto-merge: Enabled
- Squash and merge: Preferred

Branch Protection:
- Require 2 reviews
- Require status checks
- Dismiss stale reviews
- Require branches up to date
```
