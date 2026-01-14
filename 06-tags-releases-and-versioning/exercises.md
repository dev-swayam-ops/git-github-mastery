# Tags, Releases, and Versioning - Exercises

## Exercise 1: Create Lightweight Tags
**Difficulty:** Easy

Create simple tags that point to commits.

**Instructions:**
1. Make several commits on your repository
2. Create a lightweight tag `v1.0.0` on the current commit
3. Create another lightweight tag `v1.0.1` on a previous commit
4. List all tags
5. Switch to a tag to see what it points to
6. Create multiple tags in sequence on different commits
7. Verify tags are stored in `.git/refs/tags/`

**Expected Outcome:**
- Lightweight tags created successfully
- Tags can be listed and switched to
- Tags are simply references to commits
- Can reference any commit, not just HEAD

---

## Exercise 2: Create Annotated Tags
**Difficulty:** Easy

Create tags with metadata (tagger, date, message).

**Instructions:**
1. Make a commit
2. Create an annotated tag `v1.0.0` with a meaningful message
3. Create another annotated tag `v1.1.0`
4. List tags showing they exist
5. Use `git show` to view tag details
6. Compare annotated tag with lightweight tag
7. Notice the tagger information and timestamp
8. Create a tag with multiple lines of description

**Expected Outcome:**
- Annotated tags contain metadata
- `git show` displays tagger and date
- Tags can have detailed messages
- Annotated tags are Git objects

---

## Exercise 3: Delete and Rename Tags
**Difficulty:** Easy

Manage existing tags.

**Instructions:**
1. Create a tag `v1.0.0` (accidentally with wrong name)
2. Delete the tag
3. Create the correct tag `v1.0.0-beta`
4. Create another tag `wrong-tag-name`
5. Rename it to `correct-tag-name`
6. Verify old name is gone and new name exists
7. Try to delete a tag that doesn't exist (see error)

**Expected Outcome:**
- Tags can be deleted with `-d` flag
- Old tags are completely removed
- Tags can be effectively renamed (delete old, create new)
- Error handling for non-existent tags

---

## Exercise 4: Create Release Branches from Tags
**Difficulty:** Medium

Create maintenance branches based on old released versions.

**Instructions:**
1. Create multiple releases: v1.0.0, v1.1.0, v2.0.0
2. Tag each on main branch
3. Create a maintenance branch from v1.1.0: `release/1.1.x`
4. Make a patch commit on the maintenance branch
5. Tag it v1.1.1
6. Verify v1.1.1 is on the maintenance branch
7. Verify v1.1.1 is not on main (if main moved forward)
8. Merge the patch back to main if desired

**Expected Outcome:**
- Can create branches from old tags
- Maintenance releases possible
- Can support multiple versions simultaneously
- Old versions can receive security patches

---

## Exercise 5: Semantic Versioning Progression
**Difficulty:** Medium

Create a version progression following semantic versioning.

**Instructions:**
1. Start with v1.0.0 (initial release)
2. Add a new backward-compatible feature → tag v1.1.0
3. Add another feature → tag v1.2.0
4. Fix a bug → tag v1.2.1
5. Fix critical security bug → tag v1.2.2
6. Make breaking API changes → tag v2.0.0
7. Add feature to v2 → tag v2.1.0
8. Create a list showing the progression
9. Use git log to show what changed between versions

**Expected Outcome:**
- Understand MAJOR.MINOR.PATCH semantics
- Tags mark clear version boundaries
- Version progression tells the story
- Can view changes between versions

---

## Exercise 6: Tag Signed Releases
**Difficulty:** Medium

Create GPG-signed tags for security.

**Instructions:**
1. Set up GPG signing (if not already done)
2. Create a release with signed tag: `-s` flag
3. View the signed tag to see signature
4. Verify the signature
5. Create another signed tag with different key (if available)
6. List both tags and verify they're signed
7. Compare with an unsigned tag
8. Understand security implications of signed tags

**Expected Outcome:**
- Signed tags verify commit authenticity
- Signature verification possible
- Can use different keys for different releases
- Signed tags provide security guarantees

---

## Exercise 7: Create Releases with Descriptions
**Difficulty:** Medium

Create detailed releases with changelogs.

**Instructions:**
1. Create a tag v2.1.0 with annotated message including:
   - Release title
   - List of new features
   - Bug fixes
   - Known issues
2. Create tag v2.2.0 with similar detail
3. Use `git show` to view full release notes
4. Export release notes from a tag
5. Create a file with release notes
6. Link release notes to the tag

**Expected Outcome:**
- Tags can contain detailed information
- Release notes can be comprehensive
- All release history is in Git
- Easy to document versions

---

## Exercise 8: Working with Pre-Release and Build Metadata
**Difficulty:** Medium

Use pre-release versions and build metadata in semver.

**Instructions:**
1. Create alpha release: v1.0.0-alpha
2. Create beta release: v1.0.0-beta
3. Create release candidate: v1.0.0-rc.1
4. Create final release: v1.0.0
5. Create release with build metadata: v1.0.0+build.123
6. List all tags showing the progression
7. Understand version ordering with pre-releases
8. Use semantic versioning tool if available to verify

**Expected Outcome:**
- Pre-release versions clearly marked
- Build metadata provides additional info
- Version progression from alpha to final
- Proper semantic versioning practices

---

## Exercise 9: Compare Tags and View Changes
**Difficulty:** Medium

Use tags to find what changed between versions.

**Instructions:**
1. Create v1.0.0 tag on a commit
2. Make several commits adding features
3. Create v1.1.0 tag
4. Compare the two versions:
   - View commits between v1.0.0 and v1.1.0
   - View file changes between versions
   - Count lines added/removed
5. Create v2.0.0 with major changes
6. Compare v1.1.0 and v2.0.0
7. Generate a summary of changes

**Expected Outcome:**
- Can compare versions using tags
- Can see detailed changes between versions
- Useful for release notes
- Clear picture of what was added

---

## Exercise 10: Organize Tags with Naming Conventions
**Difficulty:** Medium

Create a comprehensive tagging strategy.

**Instructions:**
1. Use version tags: `v1.0.0`, `v1.1.0`, `v2.0.0`
2. Use release date tags: `release-2026-01-15`
3. Use milestone tags: `milestone/beta`, `milestone/production`
4. Use environment tags: `stable`, `testing`, `development`
5. Create prefixed tags: `app-v1.0`, `api-v2.0`, `lib-v3.0`
6. List all tags and understand the organization
7. Filter tags by pattern
8. Document the tagging strategy

**Expected Outcome:**
- Multiple tagging strategies can coexist
- Clear naming conventions
- Easy to understand tag purposes
- Flexible tagging system

