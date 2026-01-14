# 09-branch-protection-and-rulesets: Cheatsheet

## Branch Protection Rules

| Setting | Purpose | Recommended |
|---------|---------|-------------|
| Require pull request reviews | Need approval before merge | Always for main |
| Number of reviewers | How many must approve | 1 for dev, 2 for main |
| Require status checks | Tests must pass | Always for main |
| Require branches up to date | Sync with main before merge | Yes for main |
| Require signed commits | Verify commit author | Optional |
| Dismiss stale reviews | Invalidate old approvals | Yes for safety |
| Require code owner review | Domain experts approve | Yes for important files |
| Require conversation resolution | Comments must be resolved | Yes for quality |

## Creating Branch Protection Rule

```
Settings > Branches > Add rule

Branch pattern: main
☑ Require pull request reviews before merging
  - Required number of approvals: 2
  - Require review from code owners: ✓
  - Dismiss stale PR approvals: ✓
  - Require approval of last push: ✓
☑ Require status checks to pass before merging
  - Require branches to be up to date: ✓
☑ Require signed commits: ✓
☑ Require conversation resolution: ✓
☐ Allow force pushes: ✗
☐ Allow deletions: ✗
```

## Rulesets vs Branch Protection Rules

| Feature | Branch Rules | Rulesets |
|---------|--------------|----------|
| Branch patterns | Limited | Yes |
| Tag patterns | No | Yes |
| Multiple conditions | No | Yes |
| Push limitations | Basic | Advanced |
| Rule combinations | Separate | Combined |
| Newer feature | Older | Newer |

## Common Branch Patterns

| Pattern | Matches |
|---------|---------|
| `main` | Only main |
| `develop` | Only develop |
| `release/*` | release/1.0, release/2.0, etc. |
| `feature/*` | feature/auth, feature/payment, etc. |
| `hotfix/*` | hotfix/bug, hotfix/urgent, etc. |
| `*` | All branches |

## CODEOWNERS File Format

```
# Global code owners
* @alice @bob

# By file type
*.js @javascript-team
*.py @python-team
*.go @go-team

# By directory
/backend/ @backend-team
/frontend/ @frontend-team
/docs/ @documentation-team

# Specific files
package.json @alice
docker-compose.yml @devops-team

# Multiple owners
/critical/ @alice @bob @charlie
```

## Signed Commits Setup

```bash
# Generate GPG key (macOS/Linux)
gpg --gen-key

# List keys
gpg --list-secret-keys --keyid-format=long

# Configure Git globally
git config --global user.signingkey YOUR_KEY_ID
git config --global commit.gpgsign true

# Or sign specific commit
git commit -S -m "Signed message"

# Verify signatures in log
git log --show-signature
```

## Status Checks Common Tools

| Tool | Purpose | Examples |
|------|---------|----------|
| GitHub Actions | CI/CD | Tests, build, deploy |
| Jenkins | CI/CD | Pipeline automation |
| CircleCI | CI/CD | Continuous integration |
| Travis CI | CI/CD | Testing automation |
| CodeQL | Security | Code analysis |
| SonarQube | Quality | Code coverage |

## Enforcement Levels (Rulesets)

```
☑ Enforced
  - Rule applies to everyone (including admins)
  - Most restrictive
  - Good for compliance

○ Not enforced
  - Rule doesn't apply to anyone
  - Rule definition preview only
  - For testing
```

## Quick Setup Commands

```bash
# Create branch protection rule via CLI
gh rule create -b main \
  --require-code-review-count 2 \
  --require-status-checks \
  --dismiss-stale-reviews \
  --require-conversation-resolution

# List all rules
gh rule list

# Delete rule
gh rule delete RULE_ID
```

## Branch Protection Decision Tree

```
Is this main/production branch?
├─ YES:
│  ├─ Need signed commits? → Enable
│  ├─ Need strict review? → 2+ reviewers
│  ├─ Need code owners? → Enable CODEOWNERS
│  └─ Prevent mistakes? → Enable all safety checks
└─ NO:
   ├─ Development branch?
   │  ├─ Enable basic PR requirement
   │  ├─ 1 reviewer sufficient
   │  └─ Status checks optional
   └─ Feature branch?
      ├─ No protection needed
      └─ Developer can force push
```

## Troubleshooting Branch Protection

| Issue | Cause | Solution |
|-------|-------|----------|
| Can't push directly | Protected branch | Use PR instead |
| PR won't merge | Failed status check | Fix code, re-run tests |
| PR won't merge | Missing approval | Get required reviews |
| PR won't merge | Stale branch | Click "Update branch" |
| Signature check fails | Not signing commits | Configure GPG, use `-S` |
| Code owner not recognized | CODEOWNERS not found | Create CODEOWNERS file |

## Best Practices Summary

✓ **DO:**
- Protect main/production branches
- Require PR reviews
- Require status checks to pass
- Dismiss stale reviews
- Use code owners for critical code
- Document your protection rules
- Test rule configuration

✗ **DON'T:**
- Allow direct pushes to main
- Skip status checks
- Accept stale reviews
- Force push to protected branches
- Leave unresolved conversations
- Make rules too strict for development branches
- Forget to update CODEOWNERS when team changes

## Protection Rule Lifecycle

```
1. CREATE rule
   Settings > Branches > Add rule
   
2. CONFIGURE protection
   Set reviewers, checks, etc.
   
3. TEST rule
   Try to push/merge
   Verify it works
   
4. ENFORCE consistently
   Apply to all branches needing protection
   
5. MAINTAIN rules
   Update as team grows
   Adjust as process changes
   
6. DOCUMENT rules
   Share with team
   Explain reasoning
```
