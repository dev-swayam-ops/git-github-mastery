# 04-git-internals

## What You'll Learn

By the end of this module, you'll understand:
- How Git stores objects internally
- The .git folder structure
- How commits, trees, and blobs work
- How Git references (branches, tags) work
- How HEAD works and what it points to
- How Git creates hashes
- The difference between Git objects

## Prerequisites

- Completion of Modules 01-03
- Understanding of commits and branches
- Comfort with terminal/command line
- Some basic knowledge of data structures helpful

## Key Concepts

| Concept | Description |
|---------|-------------|
| **Object** | Core storage unit (commit, tree, blob, tag) |
| **Blob** | Stores file content |
| **Tree** | Stores directory structure |
| **Commit** | Links tree, parent commit, metadata |
| **Hash** | SHA-1 identifier for object |
| **Ref** | Pointer to commit (branch, tag) |
| **HEAD** | Current position in Git history |
| **.git folder** | Complete Git repository database |

## Hands-on Lab: Exploring Git's Internal Structure

### Scenario
You'll look inside Git's .git folder to understand how it stores your project.

### Step-by-Step Commands

```bash
# Step 1: Initialize repo and make commit
git init
echo "Hello" > file.txt
git add file.txt
git commit -m "Initial commit"

# Step 2: View .git structure
ls -la .git

# Step 3: Look at objects
ls -la .git/objects

# Step 4: Find your commit hash
git log --oneline

# Step 5: View commit object
git cat-file -t <hash>        # Show type
git cat-file -p <hash>        # Show content

# Step 6: View tree object
git cat-file -p <tree-hash>

# Step 7: View blob (file content)
git cat-file -p <blob-hash>

# Step 8: Check what HEAD points to
cat .git/HEAD

# Step 9: Check branch reference
cat .git/refs/heads/main

# Step 10: Count Git objects
git count-objects -v
```

### Expected Output

```
objects/
refs/
  heads/
    main        (contains commit hash)
  tags/
HEAD           (ref to current branch)

commit abc1234567...
Author: Name <email>
Date: ...
  Initial commit

100644 blob def5678... file.txt

Hello
```

## Validation

You've successfully completed this lab if:
- ✓ Explored .git folder structure
- ✓ Used git cat-file to view objects
- ✓ Understood commit/tree/blob relationships
- ✓ Verified HEAD and branch references
- ✓ Counted Git objects

## Cleanup

```bash
cd ..
rm -rf test-repo
```

## Common Mistakes

| Mistake | What Happens | How to Fix |
|---------|--------------|----------|
| Modifying .git directly | Repository corruption | Don't! Always use git commands |
| Deleting .git folder | Lose entire history | Restore from backup or use git reflog if available |
| Not understanding object types | Can't troubleshoot issues | Learn the 4 object types |
| Assuming objects can be deleted | Garbage collection confusion | Use `git gc` for proper cleanup |

## Troubleshooting

**Q: What's inside the objects folder?**
- A: Compressed objects (commits, trees, blobs) with hash-based filenames

**Q: How does Git calculate commit hash?**
- A: SHA-1 hash of commit content. Same content = same hash = powerful for detecting changes

**Q: Can I manually create commits?**
- A: Yes, with `git hash-object` and `git mktree`, but use git commands instead

**Q: How much does my .git folder grow?**
- A: Use `git count-objects -v` to check. Run `git gc` to compress

**Q: What's in the refs folder?**
- A: Files containing commit hashes that branches and tags point to

## Next Steps

Once you understand:
- Git's internal object model
- How storage works
- How references work
- Git internals depth

Move to **Module 05: Git Workflows and Strategies** to learn how to structure your team's development process.

---

**Time to Complete:** 40 minutes  
**Difficulty Level:** Intermediate-Advanced  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
