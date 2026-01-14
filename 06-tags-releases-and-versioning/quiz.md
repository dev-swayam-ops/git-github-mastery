# Tags, Releases, and Versioning - Quiz

## Multiple Choice Questions (7 Questions)

**Question 1:** What is the main difference between a lightweight tag and an annotated tag?
- A) Lightweight tags are faster
- B) Annotated tags contain metadata (tagger, date, message), lightweight tags are just references
- C) Lightweight tags work locally, annotated tags are remote
- D) They are identical

**Correct Answer:** B

**Explanation:** Lightweight tags are simple references to commits. Annotated tags are full objects with tagger information, date, and message.

---

**Question 2:** What does MAJOR.MINOR.PATCH mean in semantic versioning?
- A) Three random numbers
- B) MAJOR=breaking changes, MINOR=features, PATCH=bug fixes
- C) Different naming for the same release
- D) Configuration levels

**Correct Answer:** B

**Explanation:** Semantic versioning uses MAJOR for incompatible changes, MINOR for backward-compatible features, PATCH for bug fixes.

---

**Question 3:** Which command creates an annotated tag with a message?
- A) `git tag v1.0.0`
- B) `git tag -a v1.0.0 -m "message"`
- C) `git tag --annotate v1.0.0`
- D) `git tag -t v1.0.0`

**Correct Answer:** B

**Explanation:** `-a` flag creates annotated tag, `-m` flag adds the message in one command.

---

**Question 4:** How do you delete a tag?
- A) `git delete tag v1.0.0`
- B) `git branch -d v1.0.0`
- C) `git tag -d v1.0.0`
- D) `git rm v1.0.0`

**Correct Answer:** C

**Explanation:** `git tag -d <tagname>` deletes the tag locally. Use `git push origin --delete v1.0.0` to delete remote.

---

**Question 5:** What is the purpose of pre-release versions like v1.0.0-alpha?
- A) To mark alpha versions before final release
- B) To test before main releases
- C) Both A and B
- D) They have no special meaning

**Correct Answer:** C

**Explanation:** Pre-releases mark stages before final: alpha → beta → rc (release candidate) → final release.

---

**Question 6:** How would you create a maintenance branch for an old released version?
- A) `git branch v1.0.0`
- B) `git switch -c release/1.0.x v1.0.0`
- C) `git tag -b release/1.0.x v1.0.0`
- D) Not possible with tags

**Correct Answer:** B

**Explanation:** Create a branch from a tag: `git switch -c <branch-name> <tag-name>`. Allows ongoing maintenance of old versions.

---

**Question 7:** What should you do with a tag before pushing it to a remote repository?
- A) Nothing, tags push automatically
- B) Make sure it's signed (recommended for official releases)
- C) Delete it first
- D) Convert it to a branch

**Correct Answer:** B

**Explanation:** While not required, signing tags with GPG is a security best practice for official releases before pushing.

---

## Short Answer Questions (3 Questions)

**Question 8:** Describe when you would use lightweight tags versus annotated tags, and give an example scenario for each.

**Suggested Answer:**

**Lightweight Tags:**
- Use for: Temporary markers, internal testing, quick references
- Example: `git tag checkpoint-before-refactor` to mark a point before major refactoring, then delete after

**Annotated Tags:**
- Use for: Official releases, important milestones, archival
- Example: `git tag -a v1.0.0 -m "Production release"` for official release with metadata

**In practice:** Use annotated tags for anything pushed to shared repositories, lightweight for personal temporary markers.

**Scoring:** Full points for explaining both types and providing realistic examples. Partial credit for understanding the distinction without good examples.

---

**Question 9:** You're implementing semantic versioning for your project. Currently at v1.2.3. Walk through what version numbers you would use for the next: a security patch, a new feature, and a major breaking change.

**Suggested Answer:**

Starting from v1.2.3:

1. **Security patch (most urgent):** v1.2.4
   - Increment PATCH only
   - Backward compatible bug fix
   - Released immediately on main

2. **New feature (after patch):** v1.3.0
   - Increment MINOR, reset PATCH to 0
   - Adds functionality but backward compatible
   - Can be used with v1.2.x versions

3. **Breaking change (major):** v2.0.0
   - Increment MAJOR, reset MINOR and PATCH to 0
   - API changes, removed features, incompatible changes
   - Requires migration guide for users

**Scoring:** Full points for correct version progression and explanations. Partial credit for correct numbers but incomplete reasoning.

---

**Question 10:** Explain how you would set up a comprehensive tagging strategy for a multi-component project with an app, API, and library. Include version tags, environment markers, and how they work together.

**Suggested Answer:**

**Version Tags (per component):**
```
app-v1.0.0      # Application at version 1.0.0
api-v2.0.0      # API at version 2.0.0
lib-v3.0.0      # Library at version 3.0.0
```

**Environment Tags (moveable, point to latest for each environment):**
```
app-stable      # Latest stable app release
api-stable      # Latest stable API release
lib-stable      # Latest stable lib release
app-testing     # Latest testing app version
```

**Release Date Tags (for historical reference):**
```
release-2026-01-15  # All releases on this date
release-2026-02-01
```

**How they work together:**
- Version tags identify specific releases: `git checkout app-v1.0.0`
- Environment tags identify current status: `git show app-stable` to see what's in production
- Date tags help track history: `git log release-2026-01-15..HEAD` to see changes since that release
- Each component can be versioned independently
- Deploy by version tag: `docker build -t app:$(git describe app-v*) .`

**Scoring:** Full points for comprehensive strategy with multiple tag types and explaining how they work together. Partial credit for good strategy with incomplete integration.

---

## Answer Key Summary

| Question | Answer | Type |
|----------|--------|------|
| 1 | B | Multiple Choice |
| 2 | B | Multiple Choice |
| 3 | B | Multiple Choice |
| 4 | C | Multiple Choice |
| 5 | C | Multiple Choice |
| 6 | B | Multiple Choice |
| 7 | B | Multiple Choice |
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
- 13-15 points: Excellent tagging strategy understanding
- 10-12 points: Good understanding, review semantic versioning
- 7-9 points: Basic understanding, practice more exercises
- Below 7: Review tag types and versioning concepts

