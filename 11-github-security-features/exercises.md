# 11-github-security-features: Exercises

## Exercise 1: Enable Dependabot Alerts
**Difficulty:** Easy

Set up automatic dependency vulnerability scanning.

**Instructions:**
1. Go to Settings > Code security and analysis
2. Enable "Dependabot alerts"
3. Check Security tab for alerts
4. Review any found vulnerabilities
5. Understand severity levels

**Expected Outcome:** Dependabot alerts enabled and visible

---

## Exercise 2: Configure Secret Scanning
**Difficulty:** Easy

Enable detection of exposed secrets.

**Instructions:**
1. Settings > Code security and analysis
2. Enable "Secret scanning"
3. View detected patterns
4. Understand what's detected (API keys, tokens, etc.)
5. Configure push protection (optional)

**Expected Outcome:** Secret scanning active, secrets detected

---

## Exercise 3: Set Up Security Policy
**Difficulty:** Medium

Create SECURITY.md for vulnerability reporting.

**Instructions:**
1. Create SECURITY.md file in root
2. Add vulnerability reporting guidelines
3. Include contact info for security reports
4. Add versioning and support info
5. Link from README

**Expected Outcome:** Security policy documented

---

## Exercise 4: Enable Code Scanning with CodeQL
**Difficulty:** Medium

Set up automated code analysis.

**Instructions:**
1. Go to Security > Code scanning alerts
2. Set up CodeQL analysis
3. Choose "Set up this workflow"
4. Commit workflow file
5. View scan results

**Expected Outcome:** CodeQL scanning running on pushes

---

## Exercise 5: Review Security Advisories
**Difficulty:** Medium

Create and manage security advisories.

**Instructions:**
1. Go to Security > Advisories
2. View any existing advisories
3. Create private security advisory
4. Add severity and CVSS score
5. Publish when ready

**Expected Outcome:** Security advisory created

---

## Exercise 6: Configure Dependabot Updates
**Difficulty:** Medium

Set up automatic dependency updates.

**Instructions:**
1. Create `dependabot.yml` in `.github/`
2. Configure version-update schedule
3. Set commit message format
4. Configure labels and reviewers
5. Test with a push update

**Expected Outcome:** Dependabot PRs created automatically

---

## Exercise 7: Set Up SAST with Custom Rules
**Difficulty:** Medium

Configure security testing in CI/CD.

**Instructions:**
1. Choose security tool (SonarQube, Snyk, etc.)
2. Add to GitHub Actions workflow
3. Configure rules and severity
4. Run scan on PR
5. Review results

**Expected Outcome:** Security scanning in pipeline

---

## Exercise 8: Configure Organization Security Settings
**Difficulty:** Medium

Set enterprise-level security requirements.

**Instructions:**
1. Go to Organization Settings (if owner)
2. Enable SAML/SSO (if applicable)
3. Set password policies
4. Enable 2FA requirement
5. Review audit logs

**Expected Outcome:** Organization security hardened

---

## Exercise 9: Create Security Workflow
**Difficulty:** Medium

Automate security checks in GitHub Actions.

**Instructions:**
1. Create workflow for security scanning
2. Add multiple security tools
3. Fail build on critical issues
4. Generate security report
5. Post to PR comments

**Expected Outcome:** Automated security pipeline

---

## Exercise 10: Review Audit Logs
**Difficulty:** Medium

Monitor security and compliance events.

**Instructions:**
1. Go to Security > Audit log
2. Filter by action type
3. Search for specific events
4. Export audit log
5. Understand logged events

**Expected Outcome:** Security events tracked and auditable

---

## Summary

| Exercise | Topic | Difficulty |
|----------|-------|-----------|
| 1 | Dependabot Alerts | Easy |
| 2 | Secret Scanning | Easy |
| 3 | Security Policy | Medium |
| 4 | Code Scanning | Medium |
| 5 | Advisories | Medium |
| 6 | Dependabot Updates | Medium |
| 7 | SAST | Medium |
| 8 | Org Security | Medium |
| 9 | Security Workflow | Medium |
| 10 | Audit Logs | Medium |
