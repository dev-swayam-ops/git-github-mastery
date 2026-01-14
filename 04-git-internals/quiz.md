# Git Internals - Quiz

## Multiple Choice Questions (7 Questions)

**Question 1:** What does a git blob object store?
- A) Directory structure and filenames
- B) Commit metadata and messages
- C) File content (data)
- D) Branch references

**Correct Answer:** C

**Explanation:** Blobs store file content. Trees store directory structure. Commits store metadata. Refs store branch pointers.

---

**Question 2:** What determines a commit's hash?
- A) Just the commit message
- B) Just the files changed
- C) Tree, parent, author, committer, and message
- D) The author's name only

**Correct Answer:** C

**Explanation:** Commit hash is SHA-1 of all commit metadata combined. Changing any part (author, date, message, etc.) changes the hash.

---

**Question 3:** What does `.git/HEAD` contain?
- A) Always a commit hash
- B) Always a branch reference like `ref: refs/heads/main`
- C) Either a branch reference or a commit hash
- D) A list of all commits

**Correct Answer:** C

**Explanation:** On a branch: `ref: refs/heads/main`. In detached HEAD state: direct commit hash. Both are valid.

---

**Question 4:** How are branch names stored in Git?
- A) As full commit objects in `.git/objects`
- B) As files in `.git/refs/heads/` containing a commit hash
- C) In the `.git/config` file only
- D) As tags in `.git/refs/tags/`

**Correct Answer:** B

**Explanation:** Each branch file in `.git/refs/heads/` contains the commit hash the branch points to. Simple and elegant.

---

**Question 5:** What is the difference between a lightweight tag and an annotated tag?
- A) Lightweight tags are local, annotated tags are remote
- B) Lightweight tags are just refs, annotated tags are full objects with metadata
- C) They are identical
- D) Annotated tags are only for releases

**Correct Answer:** B

**Explanation:** Lightweight tags = simple reference to a commit. Annotated tags = full object with tagger, date, and message.

---

**Question 6:** What does `git cat-file -p <hash>` do?
- A) Prints the file at that location
- B) Displays the content of a git object
- C) Checks if the object exists
- D) Compresses the object

**Correct Answer:** B

**Explanation:** `-p` flag = "pretty print" → shows object content in readable format. Works for any object type.

---

**Question 7:** When you're in detached HEAD state, what happens to commits you make?
- A) They're automatically pushed to origin
- B) They're added to all branches
- C) They become orphaned if you switch away without creating a branch
- D) They're impossible to make

**Correct Answer:** C

**Explanation:** Commits on detached HEAD are on no branch. Switching away abandons them, but they can be recovered with reflog.

---

## Short Answer Questions (3 Questions)

**Question 8:** Explain the relationship between commits, trees, and blobs. How do they connect together?

**Suggested Answer:**
A commit points to a tree, which represents the root directory snapshot. The tree contains references to:
- Blobs for regular files (stored as `100644 blob <hash> filename`)
- Other trees for subdirectories (stored as `040000 tree <hash> dirname`)

Example hierarchy:
```
commit a1b2c3d
└── tree 4a5c8d2e
    ├── blob 557db03 (file.txt)
    └── tree 5b6d9e3f (src/)
        ├── blob 3a1c5d8f (app.js)
        └── blob 7f2a4b1c (utils.js)
```

**Scoring:** Full points for explaining all three types and showing the hierarchy. Partial credit for understanding relationships but missing details.

---

**Question 9:** Describe what `.git/refs/heads/` contains and how it relates to branches. How does Git know which branch you're on?

**Suggested Answer:**
`.git/refs/heads/` contains one file per branch. Each file's name is the branch name (e.g., `main`, `feature/login`). Each file contains a single line: the commit hash that the branch points to.

Git knows which branch you're on by reading `.git/HEAD`:
- Normal: `ref: refs/heads/main` → you're on main branch
- Detached: direct commit hash → you're not on any branch

When you switch branches, Git:
1. Reads `.git/HEAD` to find the current branch
2. Updates `.git/HEAD` to point to the new branch
3. Updates working directory to match the new branch's commit

**Scoring:** Full points for explaining files in refs/heads/, their content, and how HEAD determines current branch. Partial credit for incomplete explanation.

---

**Question 10:** What is a pack file and why does Git create them? How does it affect normal Git operations?

**Suggested Answer:**
Pack files are optimizations created by `git gc` (garbage collection). They compress multiple loose objects into:
- `.pack` file: Contains compressed objects
- `.idx` file: Index for fast lookup

Benefits:
- Saves disk space (significant for large repos)
- Faster lookups (especially for many objects)
- Better network performance for pushes/pulls

Effects on normal operations:
- No difference to user - all Git commands work transparently
- `git log`, `git cat-file`, etc. work the same
- Objects are decompressed as needed automatically
- Completely transparent compression layer

**Scoring:** Full points for explaining purpose, benefits, and transparency. Partial credit for understanding purpose but missing other details.

---

## Answer Key Summary

| Question | Answer | Type |
|----------|--------|------|
| 1 | C | Multiple Choice |
| 2 | C | Multiple Choice |
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
- 13-15 points: Excellent understanding of Git internals
- 10-12 points: Good understanding, review object relationships
- 7-9 points: Basic understanding, practice more exercises
- Below 7: Review commit/tree/blob hierarchy and references

