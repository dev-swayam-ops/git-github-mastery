# Git Internals - Cheatsheet

## Git Objects & Storage

| Command | Purpose | Example |
|---------|---------|---------|
| `git hash-object <file>` | Calculate SHA-1 hash of file | `git hash-object myfile.txt` |
| `git cat-file -p <hash>` | Display object content | `git cat-file -p a1b2c3d` |
| `git cat-file -t <hash>` | Show object type | `git cat-file -t a1b2c3d` |
| `git cat-file -s <hash>` | Show object size | `git cat-file -s a1b2c3d` |
| `git rev-parse <ref>` | Get commit hash for ref | `git rev-parse HEAD` |
| `git gc` | Garbage collection & pack files | `git gc` |
| `git verify-pack <packfile>` | Inspect pack file contents | `git verify-pack -v pack-*.idx` |

---

## .git Directory Structure

### Core Directories
```
.git/
├── HEAD              # Points to current branch
├── config            # Repository configuration
├── index             # Staging area (binary)
├── objects/          # All git objects (blobs, trees, commits, tags)
│   ├── <2-char>/     # Directory based on first 2 chars of hash
│   │   └── <38-char> # Filename from remaining hash chars
│   └── pack/         # Compressed object files
├── refs/             # Branch and tag references
│   ├── heads/        # Branch references
│   ├── tags/         # Tag references
│   └── remotes/      # Remote tracking branches
├── hooks/            # Git hook scripts
├── info/             # Additional info directory
└── description       # Repository description
```

---

## Git Objects (4 Types)

### Blob (Binary Large Object)
- Stores file content
- Identified by SHA-1 hash of content
- `git cat-file -t <hash>` returns: `blob`
- **Example:** `git cat-file -p a1b2c3d` → file content

### Tree
- Maps filenames to object hashes
- Represents directory structure
- `git cat-file -t <hash>` returns: `tree`
- **Format:** `mode type hash filename`
- **Example:** `100644 blob a1b2c3d file.txt`

### Commit
- Represents a snapshot in time
- Contains: tree, parent, author, committer, message
- `git cat-file -t <hash>` returns: `commit`
- **Example:** First commit has no parent

### Tag
- Annotated tags are objects (with metadata)
- Lightweight tags are refs (just a pointer)
- `git cat-file -t <hash>` returns: `tag`
- Contains: object hash, type, tagger, message

---

## Understanding Object Relationships

```
commit a1b2c3d
├── tree: 4a5c8d2e (root directory)
│   ├── blob: 557db03d (file1.txt)
│   ├── blob: 7f2a4b1c (file2.js)
│   └── tree: 5b6d9e3f (src/ directory)
│       ├── blob: 3a1c5d8f (app.js)
│       └── blob: 7f2a4b1c (utils.js)
├── parent: d3e4f5g6 (previous commit)
├── author: Name <email@domain.com>
└── message: Commit description
```

---

## References (Refs)

### Branch References
- Location: `.git/refs/heads/<branch-name>`
- Content: Commit hash the branch points to
- **Example:** `.git/refs/heads/main` contains `a1b2c3d...`

### Tag References
- Location: `.git/refs/tags/<tag-name>`
- Lightweight: Just a commit hash
- Annotated: Reference to tag object

### Remote Tracking References
- Location: `.git/refs/remotes/<remote>/<branch>`
- Example: `.git/refs/remotes/origin/main`

### Special References
- `HEAD`: Points to current branch or commit
- Format: `ref: refs/heads/main` or direct commit hash
- Detached HEAD: HEAD contains commit hash directly

---

## HEAD States

### Normal State (On a Branch)
```
$ cat .git/HEAD
ref: refs/heads/main
```

### Detached HEAD State
```
$ cat .git/HEAD
a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6
```

### Understanding Detached HEAD
- HEAD points to a commit, not a branch
- Commits made are on no branch
- Switching away abandons the commits (can be recovered)
- Create a branch to save commits: `git branch new-branch <commit-hash>`

---

## Commit References

| Syntax | Meaning |
|--------|---------|
| `HEAD` | Current commit |
| `HEAD~1` | Parent commit |
| `HEAD~2` | Grandparent commit |
| `HEAD~n` | n commits back |
| `HEAD@{0}` | Current HEAD (reflog) |
| `HEAD@{n}` | n positions back in reflog |
| `<branch>~1` | Parent of branch tip |
| `<hash>` | Specific commit by hash |

---

## Git Configuration Locations

### Priority (lowest to highest)
1. System: `/etc/gitconfig`
2. Global: `~/.gitconfig` or `~/.config/git/config`
3. Local: `.git/config`

### Viewing Configuration
```bash
git config --system -l    # System level
git config --global -l    # Global level
git config --local -l     # Local level (repo)
git config -l             # All levels combined
```

### Common Configuration
```
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
[user]
    name = Your Name
    email = your@email.com
[remote "origin"]
    url = https://github.com/user/repo.git
```

---

## Pack Files (Optimization)

### When Created
- `git gc` (garbage collection) creates pack files
- Automatically during push/fetch operations
- Periodically by Git background processes

### Pack File Components
- `.pack` file: Compressed objects
- `.idx` file: Index for fast lookup
- `.keep` file: Prevents repacking

### Inspection
```bash
git gc                           # Create pack files
git verify-pack -v *.idx        # View pack contents
git rev-list --objects --all    # List all objects
```

---

## Git Internals Debugging

### Explore Objects
```bash
git hash-object <file>              # Get blob hash
git cat-file -t <hash>              # Check object type
git cat-file -p <hash>              # View object content
git cat-file -s <hash>              # Check object size
```

### Explore References
```bash
cat .git/HEAD                       # Check current HEAD
cat .git/refs/heads/<branch>        # Check branch pointer
ls -la .git/refs/heads/             # List all branches
```

### Explore History
```bash
git log --all --graph --oneline     # Complete history
git log --reflog                    # Reflog history
git fsck --lost-found               # Find lost objects
```

---

## Tips & Best Practices

1. **Understanding Immutability**
   - Content hash = SHA-1 of object
   - Same content = same hash
   - Different content = different hash
   - Ensures integrity

2. **Referencing Commits**
   - Use symbolic names: `HEAD`, branch names, tags
   - Use relative references: `HEAD~1`, `HEAD~2`
   - Use commit hashes when needed

3. **Optimization**
   - Git automatically manages objects
   - Pack files save space
   - Loose objects fine for small repos
   - `git gc` for maintenance

4. **Recovery**
   - Objects never deleted unless reflog expires
   - Use `git reflog` to find lost commits
   - Use `git fsck --lost-found` for orphaned objects

