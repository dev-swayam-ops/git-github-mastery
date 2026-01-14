# 08-github-repo-settings-and-access-control

## What You'll Learn

By the end of this module, you'll understand:
- Repository settings and configuration
- Team and user permissions
- Role-based access control
- Organization management
- Repository visibility (public/private)
- Access tokens and personal authentication
- Security best practices for access

## Prerequisites

- Completion of Modules 01-07
- GitHub account with admin permissions
- Basic understanding of teams

## Key Concepts

| Role | Permissions | Best For |
|------|-------------|----------|
| **Owner** | Full admin | Repository founder |
| **Maintainer** | Most admin, not delete | Core team leads |
| **Write** | Push, merge, not delete | Regular developers |
| **Triage** | Manage issues/PRs, read | Community moderators |
| **Read** | Read-only access | External stakeholders |

## Hands-on Lab: Configuring Repository Access

### Scenario
You're setting up access control for a team project with different roles.

### Step-by-Step Commands

```bash
# Step 1: Create organization (if not exists)
# GitHub > Profile > Settings > Organizations > New

# Step 2: Create team
# Organization > Teams > New Team
# Name: development
# Privacy: Private

# Step 3: Add team members
# Team > Members > Add member
# Select users from organization

# Step 4: Assign repository to team
# Team > Repositories > Add repository
# Select repository and role

# Step 5: Configure branch protection
git clone <repo>
cd <repo>

# Go to GitHub > Settings > Branches > Add rule
# Pattern: main
# Check: Require PR reviews
# Check: Dismiss stale reviews
# Check: Require status checks

# Step 6: Set team role
# Repository > Settings > Collaborators and teams
# Add team with appropriate role

# Step 7: View team permissions
# Repository > Insights > People > Teams

# Step 8: Create PAT for automation
# Settings > Developer settings > Personal access tokens
# Generate new token with scope

# Step 9: Test access
git config user.name "Developer"
git config user.email "dev@example.com"
echo "test" >> file.txt
git add file.txt
git commit -m "Test access"
# git push (should succeed with correct permissions)
```

### Expected Output

```
Team created: development
Repository added to team
Branch protection rule created
Personal access token generated
Access verified
```

## Validation

You've successfully completed this lab if:
- ✓ Created organization
- ✓ Created team
- ✓ Added team members
- ✓ Assigned repository to team
- ✓ Configured branch protection
- ✓ Understood role permissions

## Cleanup

```bash
cd ..
rm -rf test-repo
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Everyone is owner | No governance | Use roles: owner, maintainer, write |
| PAT with full permissions | Security risk | Use minimal scopes |
| Direct main branch access | Bypasses review | Always require PR and review |
| No team structure | Confusion about access | Create teams by function |
| Forgotten access tokens | Account compromise | Regularly rotate and revoke |

## Troubleshooting

**Q: What's the best role for developers?**
- A: "Write" for developers, "Maintain" for leads, "Admin" only for owners

**Q: How do I restrict direct commits to main?**
- A: Branch protection > Require PR, require reviews, require status checks

**Q: Can users have different permissions per branch?**
- A: No, permissions are repository-wide. Use branch protection rules to restrict specific branches

**Q: What's a personal access token?**
- A: Password replacement for API/CLI access. More secure than password. Can be revoked

**Q: How do I audit who accessed what?**
- A: Settings > Audit log. View who did what and when

## Next Steps

Once comfortable with:
- Repository access control
- Team management
- Role-based permissions
- Branch protection

Move to **Module 09: Branch Protection and Rulesets** to master advanced protection rules.

---

**Time to Complete:** 50 minutes  
**Difficulty Level:** Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
