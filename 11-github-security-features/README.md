# 11-github-security-features

## What You'll Learn

By the end of this module, you'll understand:
- Secret scanning
- Dependabot for vulnerability management
- Code scanning and SAST
- Security advisories
- Token management and rotation
- Audit logging
- Security best practices

## Prerequisites

- Completion of Modules 01-10
- Understanding of GitHub features
- Some security awareness

## Key Concepts

| Feature | Purpose | Detection |
|---------|---------|----------|
| **Secret Scanning** | Prevent exposed credentials | Keys, tokens, passwords |
| **Dependabot** | Vulnerable dependencies | Library vulnerabilities |
| **Code Scanning** | Find code vulnerabilities | SAST analysis |
| **Security Advisory** | CVE reporting | Public vulnerabilities |
| **SAML/SSO** | Enterprise authentication | Identity management |
| **Audit Log** | Track user actions | Who did what when |
| **Token Management** | PAT security | Expiration, rotation |

## Hands-on Lab: Implementing Security Scanning

### Scenario
You're implementing automated security scanning to catch vulnerabilities before they're exploited.

### Step-by-Step Commands

```bash
# Step 1: Enable secret scanning
# GitHub > Settings > Security & analysis > Secret scanning
# Toggle ON for secret scanning
# Toggle ON for push protection

# Step 2: Create test file with secret (for learning)
git clone <repo>
cd <repo>
echo "aws_secret_access_key = AKIAIOSFODNN7EXAMPLE" > credentials.txt
git add credentials.txt
# Try to commit (should be blocked by push protection)

# Step 3: Remove exposed credential
rm credentials.txt

# Step 4: Enable code scanning
# GitHub > Settings > Security & analysis > Code scanning
# Click "Set up" > Choose CodeQL
# Let GitHub generate workflow

# Step 5: Review CodeQL workflow
cat .github/workflows/codeql.yml

# Step 6: Verify Dependabot
# GitHub > Settings > Security & analysis > Dependabot
# Enable: Version updates
# Enable: Security updates

# Step 7: Create dependabot config
mkdir -p .github
cat > .github/dependabot.yml << 'EOF'
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "monday"
      time: "04:00"
    open-pull-requests-limit: 10
    reviewers:
      - "dependency-reviewer"
EOF

# Step 8: Check security advisories
# GitHub > Security > Advisories
# View any reported vulnerabilities

# Step 9: Review audit log
# Organization > Audit log (if owner)
# View all user actions

# Step 10: Rotate personal tokens
# Settings > Developer settings > Personal access tokens
# Delete old tokens, create new ones

git add .github/dependabot.yml
git commit -m "Add Dependabot configuration"
git push origin main
```

### Expected Output

```
Secret scanning enabled
CodeQL scanning workflow created
Dependabot configured
Security dashboard updated
```

## Validation

You've successfully completed this lab if:
- ✓ Enabled secret scanning
- ✓ Enabled code scanning
- ✓ Configured Dependabot
- ✓ Reviewed security settings
- ✓ Understood vulnerability reports

## Cleanup

```bash
git checkout main
rm -f credentials.txt
rm -f .github/dependabot.yml
git add .
git commit -m "Cleanup: Remove security test files"
git push origin main
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Secret already exposed | Compromised credential | 1. Rotate secret 2. Enable scanning |
| Ignoring Dependabot | Vulnerable dependencies | Review and merge PRs promptly |
| No code scanning | Unknown code vulnerabilities | Enable CodeQL or equivalent |
| Weak secrets | Easy to brute force | Use long, complex secrets |
| Never rotating tokens | Exposed tokens stay valid | Rotate quarterly minimum |

## Troubleshooting

**Q: What's the difference between scanning and monitoring?**
- A: Scanning: active search for issues. Monitoring: watch for new vulnerabilities

**Q: How do I handle false positives in code scanning?**
- A: Mark as "Not needed", add comment explaining why

**Q: What's secret rotation?**
- A: Periodically replace credentials with new ones. Best practice: quarterly

**Q: Can I scan without CodeQL?**
- A: Yes! Use other tools: Snyk, SonarQube, OWASP, etc.

**Q: How do I prioritize security alerts?**
- A: Focus on high severity + public exploits first

## Next Steps

Once comfortable with:
- Secret scanning
- Dependabot
- Code scanning
- Security monitoring

Move to **Module 12: Collaboration Labs and Scenarios** to practice team workflows.

---

**Time to Complete:** 50 minutes  
**Difficulty Level:** Intermediate  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
