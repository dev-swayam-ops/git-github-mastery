# Git Workflows and Strategies - Quiz

## Multiple Choice Questions (7 Questions)

**Question 1:** In Git Flow, which branch is used for developing new features?
- A) main
- B) feature
- C) develop
- D) release

**Correct Answer:** C

**Explanation:** In Git Flow, develop is the main integration branch. Feature branches branch from develop and merge back to develop.

---

**Question 2:** What is the key principle of GitHub Flow?
- A) Multiple permanent branches with specific purposes
- B) Main is always deployable; features merge back quickly
- C) Hotfixes handled separately from regular releases
- D) Develop and main branches managed differently

**Correct Answer:** B

**Explanation:** GitHub Flow is simpler than Git Flow with one main branch that's always ready to deploy and short-lived feature branches.

---

**Question 3:** What is the primary benefit of trunk-based development?
- A) Better for large teams
- B) Easier to manage releases
- C) Reduced merge conflicts and more frequent integration
- D) Better for projects with infrequent releases

**Correct Answer:** C

**Explanation:** Trunk-based keeps all developers merged to main frequently (hours), minimizing conflicts and keeping code current.

---

**Question 4:** When should you create a hotfix branch in Git Flow?
- A) For any bug fix
- B) For critical production bugs that need immediate release
- C) For bugs found during development
- D) Hotfix branches are never used

**Correct Answer:** B

**Explanation:** Hotfixes branch from main to fix production issues immediately, then merge back to both main and develop.

---

**Question 5:** What is semantic versioning MAJOR.MINOR.PATCH incremented for?
- A) MAJOR for any change, MINOR for updates, PATCH for releases
- B) MAJOR for breaking changes, MINOR for features, PATCH for bug fixes
- C) MAJOR for releases, MINOR for updates, PATCH for anything
- D) They all mean the same thing

**Correct Answer:** B

**Explanation:** MAJOR = breaking changes (1.0.0→2.0.0), MINOR = features backward compatible (1.0.0→1.1.0), PATCH = bug fixes (1.0.0→1.0.1).

---

**Question 6:** What is the main purpose of feature flags?
- A) Mark which branches are features
- B) Enable/disable features without branching, for testing and gradual rollout
- C) Prevent merging branches
- D) Track feature status in pull requests

**Correct Answer:** B

**Explanation:** Feature flags let you merge incomplete features (disabled) and enable them later for testing or gradual rollout without needing long-lived branches.

---

**Question 7:** In Git Flow, after fixing a critical bug on a release branch, where should it be merged back?
- A) Only to main
- B) Only to develop
- C) To both main AND develop
- D) To feature branches

**Correct Answer:** C

**Explanation:** Bug fixes on release branches must go to both main (production) and develop (ongoing development) to keep them synchronized.

---

## Short Answer Questions (3 Questions)

**Question 8:** Compare GitHub Flow and Git Flow. What are the main differences and which would you choose for a startup?

**Suggested Answer:**

**GitHub Flow:**
- One main branch
- Simple feature branching
- Short-lived branches
- Continuous deployment
- No release or hotfix branches

**Git Flow:**
- Two permanent branches (main, develop)
- Release branches for preparation
- Hotfix branches for production bugs
- More complex but structured
- Better for versioned releases

**For a startup:** GitHub Flow is better because:
- Simpler process (less overhead)
- Supports continuous deployment
- Easier for small teams
- Quick iteration and feedback

**Scoring:** Full points for comparing both workflows and justifying choice. Partial credit for good comparison but weak justification.

---

**Question 9:** You're in a Git Flow workflow and discover a critical security bug in production. Walk through the exact steps you would take to fix it.

**Suggested Answer:**
1. Create hotfix branch from main: `git switch -c hotfix/security-patch main`
2. Fix the security bug with one or more commits
3. Test the fix thoroughly
4. Merge hotfix to main: `git switch main; git merge hotfix/security-patch`
5. Tag the release: `git tag v1.0.1`
6. Merge hotfix to develop: `git switch develop; git merge hotfix/security-patch` (critical!)
7. Delete the hotfix branch: `git branch -d hotfix/security-patch`
8. Deploy the tagged version to production

Why both merges: Main gets the fix for the next release, develop gets it so new features are based on secure code.

**Scoring:** Full points for correct sequence including both merges and tagging. Partial credit for correct overall approach but missing some details.

---

**Question 10:** Explain how feature flags enable trunk-based development and what the lifecycle of a feature flag looks like.

**Suggested Answer:**

**How feature flags enable trunk-based development:**
- Allows merging incomplete/untested features to main (disabled)
- Main stays deployable even with partial features
- Reduces time features spend in branches
- Enables testing without branching

**Feature flag lifecycle:**
1. **Development:** Implement feature behind flag (disabled by default)
2. **Integration:** Merge to main with flag disabled
3. **Testing:** Enable flag for QA/testing
4. **Gradual Rollout:** Enable for 10% → 50% → 100% of users
5. **Monitoring:** Monitor metrics with flag enabled
6. **Cleanup:** Remove flag once stable (code simplification)

**Example:**
```python
if os.getenv('USE_NEW_PAYMENT') == 'true':
    use_new_payment_system()
else:
    use_old_payment_system()
```

**Scoring:** Full points for explaining how flags enable trunk-based and showing complete lifecycle. Partial credit for one good answer with incomplete other.

---

## Answer Key Summary

| Question | Answer | Type |
|----------|--------|------|
| 1 | C | Multiple Choice |
| 2 | B | Multiple Choice |
| 3 | C | Multiple Choice |
| 4 | B | Multiple Choice |
| 5 | B | Multiple Choice |
| 6 | B | Multiple Choice |
| 7 | C | Multiple Choice |
| 8 | See above | Short Answer |
| 9 | See above | Short Answer |
| 10 | See above | Short Answer |

---

## Scoring Guide

- **Multiple Choice:** 1 point each (7 points total)
- **Short Answer Q8:** 2 points
- **Short Answer Q9:** 2 points
- **Short Answer Q10:** 2 points
- **Total:** 15 points

### Grading Scale
- 13-15 points: Excellent workflow understanding
- 10-12 points: Good understanding, review workflows
- 7-9 points: Basic understanding, practice exercises
- Below 7: Review Git Flow vs GitHub Flow concepts

