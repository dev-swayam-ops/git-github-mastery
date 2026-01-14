# 11-github-security-features: Cheatsheet

## Security Features Comparison

| Feature | Purpose | Free | Pro | Enterprise |
|---------|---------|------|-----|-----------|
| Dependabot Alerts | Vulnerability scanning | ✓ | ✓ | ✓ |
| Secret Scanning | Find exposed secrets | ✗ | ✓ | ✓ |
| CodeQL Analysis | Code scanning | ✓ | ✓ | ✓ |
| SAST | Static analysis | Via Actions | Via Actions | ✓ |
| Audit Logs | Activity tracking | Basic | ✓ | ✓ |

## Enabling Security Features

| Feature | Location |
|---------|----------|
| Dependabot | Settings > Code security |
| Secret Scanning | Settings > Code security |
| CodeQL | Security > Code scanning |
| Branch Protection | Settings > Branches |
| 2FA | Personal Settings > Security |
| Audit Log | Organization Settings > Audit log |

## Common Security Tools

| Tool | Type | Language Support |
|------|------|-----------------|
| CodeQL | SAST | Multiple |
| Snyk | SCA/SAST | Multiple |
| SonarQube | SAST | Multiple |
| OWASP ZAP | DAST | Web apps |
| npm audit | SCA | JavaScript |
| Dependabot | Dependency | All |

## Vulnerability Severity Levels

| Level | CVSS | Action |
|-------|------|--------|
| Critical | 9.0-10.0 | Fix immediately |
| High | 7.0-8.9 | Fix within days |
| Moderate | 4.0-6.9 | Fix within weeks |
| Low | 0.1-3.9 | Monitor, fix when possible |

## Creating SECURITY.md

```markdown
# Security Policy

## Reporting
Email: security@example.com
Not: Public issues

## Supported Versions
- 2.0.x: Supported
- 1.9.x: Supported
- 1.8.x: EOL

## Timeline
- Critical: Immediate
- High: 24 hours
- Moderate: 1 week
```

## Dependabot Configuration

```yaml
updates:
  - package-ecosystem: npm
    directory: "/"
    schedule:
      interval: weekly
    labels: [dependencies]
    reviewers: [alice]
```

## CodeQL Setup

```bash
# Initialize database
codeql database create mydb --language=python

# Run analysis
codeql database analyze mydb codeql/python-queries

# Generate SARIF
codeql database interpret-results mydb
```

## Secret Types Detected

```
GitHub Tokens
AWS Credentials
NPM Tokens
PyPI Tokens
SSH Private Keys
Database Credentials
Private Keys
API Keys
Mailchimp Keys
Slack Webhooks
```

## Audit Log Actions

| Action | Description |
|--------|-------------|
| `repo.push` | Code pushed |
| `repo.create` | Repo created |
| `repo.delete` | Repo deleted |
| `member.invite` | User invited |
| `member.remove` | User removed |
| `team.create` | Team created |
| `settings.update` | Settings changed |

## CLI Commands

```bash
# Check for vulnerabilities
gh repo view --json 'dependabotAlerts'

# Enable alerts
gh repo edit --enable-vulnerability-alerts

# Export audit log
gh api repos/OWNER/REPO/audit-logs

# Set secret
gh secret set SECRET_NAME --body value
```

## Security Workflow Template

```yaml
on: [push, pull_request]
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: CodeQL Analysis
        uses: github/codeql-action/init@v2
      
      - name: Dependency Check
        run: npm audit --audit-level=high
      
      - name: Secret Scan
        run: git log -p | grep -E "password|api_key|token"
      
      - name: Upload Results
        uses: github/codeql-action/upload-sarif@v2
```

## Access Control Security

```
Branch Protection Rules:
- Require PR review
- Require status checks
- Require signed commits
- Require code owners
- Dismiss stale reviews
- Restrict push access
```

## 2FA Setup Steps

```
1. User Settings > Security
2. Enable 2FA
3. Scan QR code with authenticator app
4. Generate backup codes
5. Verify with OTP
```

## Dependabot Best Practices

✓ Enable for all package managers
✓ Set review schedule
✓ Assign to team members
✓ Use allow/ignore lists
✓ Require PR reviews
✓ Test dependency updates
✓ Keep dependencies updated
✓ Monitor security advisories

## Security Compliance

```
For Production:
□ All security features enabled
□ Branch protection active
□ Code review required
□ Signed commits enforced
□ Audit logs enabled
□ 2FA required for users
□ Secrets properly stored
□ Dependencies scanned
□ SAST running
□ Incident response plan
```

## Quick Security Audit

```bash
# Check vulnerabilities
npm audit

# Check for secrets in code
git log -p | grep -i "password\|secret"

# Review branch protection
gh repo view --json 'branchProtectionRules'

# List collaborators
gh repo view --json 'collaborators'

# Check 2FA status
gh api /user
```

## Response Times SLA

| Severity | Response | Fix |
|----------|----------|-----|
| Critical | 1 hour | 24 hours |
| High | 4 hours | 1 week |
| Moderate | 1 day | 1 month |
| Low | 3 days | As planned |

## Tools Integration

```
GitHub ←→ Snyk
      ←→ SonarQube
      ←→ CodeQL
      ←→ Dependabot
      ←→ Custom tools via API
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Alerts not showing | Enable Dependabot alerts in settings |
| Secret blocked | Use GitHub secrets instead |
| Scan too slow | Exclude node_modules, vendor |
| False positives | Configure rules, adjust thresholds |
