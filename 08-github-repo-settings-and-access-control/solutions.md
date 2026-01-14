# 08-github-repo-settings-and-access-control: Solutions

## Solution 1: Configure Basic Repository Settings

**Steps:**
1. Navigate to your repository on GitHub
2. Click "Settings" tab
3. In "Repository name" field, update description
4. Click "Website" field to add project URL
5. Scroll to find "Features" section
6. Toggle Wiki, Projects, Discussions as needed
7. Click "Save changes" at bottom

**Configuration Best Practices:**
- Keep description under 160 characters (displays in search)
- Add website URL if project has documentation
- Disable unused features to reduce clutter
- Enable Discussions for community interaction

---

## Solution 2: Manage Repository Visibility

**Current Status Check:**
```
Settings > General > Danger Zone > Change repository visibility
```

**Visibility Types:**

| Type | Cost | Access | Use Case |
|------|------|--------|----------|
| Public | Free | Anyone on internet | Open source projects |
| Private | Free/Paid | Invited users only | Proprietary code |
| Internal | Enterprise | Organization members | Internal tools |

**When making Private:**
- Code is hidden from public
- Only invited collaborators access
- Useful for company/private projects

---

## Solution 3: Add Collaborators to Repository

**Steps via GitHub Web:**
```
Settings > Collaborators and teams > Add people
```

**Using GitHub CLI:**
```bash
gh repo add-access --user username --permission write
```

**Role Permission Levels:**

| Role | Can Pull | Can Push | Can Admin | Use For |
|------|----------|---------|----------|---------|
| Read | ✓ | ✗ | ✗ | View-only users |
| Triage | ✓ | ✗ | ✓ issues | Issue managers |
| Write | ✓ | ✓ | ✗ | Developers |
| Maintain | ✓ | ✓ | Limited | Team leads |
| Admin | ✓ | ✓ | ✓ | Repository owner |

---

## Solution 4: Understand Repository Roles

**Role Comparison Table:**

| Permission | Read | Triage | Write | Maintain | Admin |
|-----------|------|--------|-------|----------|-------|
| Pull branches | ✓ | ✓ | ✓ | ✓ | ✓ |
| Push branches | ✗ | ✗ | ✓ | ✓ | ✓ |
| Merge PRs | ✗ | ✗ | ✓ | ✓ | ✓ |
| Create releases | ✗ | ✗ | ✗ | ✓ | ✓ |
| Manage settings | ✗ | ✗ | ✗ | ✗ | ✓ |
| Delete repo | ✗ | ✗ | ✗ | ✗ | ✓ |

**Best Practices:**
- Developers: Write
- Team leads: Maintain
- Managers/Owners: Admin
- Auditors: Read
- Community: Triage

---

## Solution 5: Configure Default Branch

**Steps:**
```
Settings > Branches > Default branch > Change
```

**Impact of Changing Default:**
1. New clones use new default
2. GitHub web interface shows new default
3. PRs target new default by convention
4. Existing PRs unaffected

**Example Workflow:**
```
Before: main is default
After: develop is default
- git clone repo → clones develop
- New PRs default to develop target
- main still exists, not deleted
```

---

## Solution 6: Set Up Branch Protection Rules

**Steps:**
```
Settings > Branches > Add rule
```

**Configuration Options:**

```yaml
Branch pattern: main
Require pull request reviews: YES
Require code owner reviews: YES
Require status checks: YES
Require branches to be up to date: YES
Require commit signatures: NO
Allow force pushes: NO
Allow deletions: NO
```

**Example Protection for Production:**
- Require 2 PR reviews
- Require CI tests passing
- Require admin approval
- Prevent force pushes
- Prevent direct pushes (require PR)

---

## Solution 7: Manage Teams and Permissions

**Via GitHub Web:**
```
Settings > Teams > Select Team > Set Role
```

**Team vs Individual Permissions:**

| Aspect | Team | Individual |
|--------|------|-----------|
| Scalability | Add members to team | Add each person |
| Management | Manage once | Manage per person |
| Roles | Team-level roles | Individual roles |
| Use Case | Large teams | Few collaborators |

**Recommended Setup:**
- Use Teams for organizations
- Use Individuals for small projects
- Teams give consistency at scale

---

## Solution 8: Configure Webhook Settings

**Webhook Purpose:**
Send real-time event notifications to external systems (Slack, CI/CD, etc.)

**Common Events:**
- push - Code pushed
- pull_request - PR opened/closed
- issues - Issue created
- release - Release published
- deployment - Code deployed

**Webhook Configuration:**
```
Settings > Webhooks > Add webhook

Payload URL: https://your-server.com/webhook
Content type: application/json
Events: Let me select individual events
  - Push events
  - Pull request events
  - Issues
Active: Checked
```

---

## Solution 9: Review Deploy Keys

**Deploy Key Purpose:**
Machine-only access (read-only or read-write) for CI/CD pipelines

**Deploy Key vs Personal Token:**

| Aspect | Deploy Key | Personal Token |
|--------|-----------|----------------|
| Owner | Repository | User account |
| Scope | One repository | All repositories |
| Revoke | Per repo | Account-wide |
| Use | CI/CD machines | Scripts, CLI tools |
| Security | More isolated | Broader access |

**Setup in CI/CD:**
```bash
# In GitHub Actions
- name: Deploy
  uses: actions/deploy-key-action@v1
  with:
    deploy-key: ${{ secrets.DEPLOY_KEY }}
```

---

## Solution 10: Configure Repository Automation

**Auto-merge Configuration:**
```
Settings > General > Pull Requests
- Allow auto-merge: Enable
- Auto-merge method: Squash and merge (recommended)
```

**Branch Deletion:**
```
Settings > General > Pull Requests
- Automatically delete head branches: Enable
- Cleans up merged feature branches automatically
```

**Commit Squashing Default:**
```
- Allow squash merging: Enable
- Allow rebase merging: Enable
- Allow merge commits: Optional
```

**Complete Configuration Example:**
```yaml
Description: "My Project"
Default branch: main
Auto-merge: Enabled (Squash)
Delete branches: Enabled
Require PR reviews: Yes
Require status checks: Yes
Dismiss stale reviews: Yes
Require branches up to date: Yes
```

---

## Summary Workflow

1. **Create Repository** → Set visibility (Public/Private)
2. **Add Description** → Help people understand project
3. **Add Collaborators** → Grant appropriate roles
4. **Configure Default Branch** → Set to main/develop
5. **Add Branch Protection** → Protect main branch
6. **Setup Teams** → For larger projects
7. **Configure Webhooks** → For integrations
8. **Set Deploy Keys** → For CI/CD access
9. **Enable Automation** → Auto-merge, delete branches

---

## Security Best Practices

- **Minimal Permissions** - Give lowest permission needed
- **Rotate Access** - Remove unused collaborators
- **Use Teams** - Easier to manage at scale
- **Protect Main** - Prevent direct pushes
- **Enable 2FA** - For admin access
- **Audit Logs** - Review who did what
- **Deploy Keys** - Not personal tokens in CI/CD
