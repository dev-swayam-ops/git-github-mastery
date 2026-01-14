# 14-cheatsheets-and-interview-notes

## What You'll Learn

By the end of this module, you'll understand:
- Quick reference command guides
- Interview preparation
- Common interview questions
- GitHub/Git concepts for interviews
- Best answers to technical questions
- Problem-solving strategies
- Explaining Git concepts clearly

## Prerequisites

- Completion of Modules 01-13
- Job search preparation
- Interview practice

## Key Concepts

| Area | Topics | Purpose |
|------|--------|----------|
| **Fundamentals** | What is Git, commits, branches | Baseline knowledge |
| **Advanced** | Rebase vs merge, workflows | Problem-solving |
| **Teamwork** | Collaboration, review | Real-world scenarios |
| **Troubleshooting** | Recovery, conflicts | Handling issues |
| **GitHub Features** | Actions, security, PRs | Platform knowledge |

## Hands-on Lab: Interview Preparation

### Scenario
You're preparing for technical interviews involving Git and GitHub knowledge.

### Common Interview Questions & Answers

```bash
# Q1: What's the difference between Git and GitHub?
# A: Git is version control (local), GitHub is hosting (remote/social)

# Q2: What's in a commit?
# A: Hash, author, date, message, parent commit(s), changes (diff)

# Q3: Merge vs Rebase?
# A: Merge preserves history, rebase cleans history
#    Merge: safe for shared branches
#    Rebase: clean history for local/feature branches

# Q4: What's a detached HEAD?
# A: HEAD pointing directly to commit instead of branch
#    Solution: git checkout branch or git branch recovery-branch

# Q5: How do you revert a commit that's been pushed?
# A: git revert <commit> creates new commit that undoes changes

# Q6: What's the difference between reset, revert, restore?
# A: reset (move HEAD), revert (undo via new commit), restore (checkout file)

# Q7: How do you handle merge conflicts?
# A: 1. Identify conflicts (<<<< ==== >>>>)
#    2. Resolve manually (keep/discard)
#    3. git add
#    4. git commit
#    5. Test

# Q8: What's Git Flow?
# A: Workflow with main, develop, feature/*, release/*, hotfix/*
#    Best for versioned releases

# Q9: What's a good commit message?
# A: - Imperative mood ("Add", not "Added")
#    - Under 50 chars for title
#    - Blank line before body
#    - Explain what and why, not how

# Q10: How do you optimize a large repository?
# A: git gc --aggressive, git sparse-checkout, git clone --depth 1

# PRACTICE: Explain your workflow
echo "I use:
1. Fork → Feature branch → PR → Code review → Merge
2. Git Flow for releases
3. Branch protection rules
4. CI/CD for automated testing
5. Semantic versioning for releases
6. Squash commits for clean history
" > my-workflow.txt

# PRACTICE: Describe handling a production bug
echo "1. Create hotfix branch from main
2. Make minimal fix
3. Test thoroughly
4. Create PR (with urgency label)
5. Merge to main (fast-forward)
6. Tag version
7. Merge hotfix back to develop
8. Deploy to production
" > hotfix-process.txt

# PRACTICE: Explain a complex scenario
echo "Scenario: Multiple teams, parallel development
Solution:
1. Each feature gets own branch from develop
2. PRs with code review
3. Merge to develop when approved
4. Keep feature branches updated with develop
5. Resolve conflicts early
6. Release when features complete
" > scenario-answer.txt
```

### Expected Output

```
Interview preparation completed
Common questions answered
Scenarios explained
Workflow documented
```

## Quick Reference Commands

### Setup
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init
git clone <url>
```

### Basic Workflow
```bash
git status
git add <file>
git commit -m "message"
git push origin <branch>
git pull origin <branch>
```

### Branching
```bash
git branch
git branch <new-branch>
git checkout <branch>
git checkout -b <new-branch>
git merge <branch>
```

### Advanced
```bash
git rebase <branch>
git rebase -i HEAD~3
git cherry-pick <commit>
git reset --hard <commit>
git reflog
```

## Validation

You've successfully completed this lab if:
- ✓ Understood core Git concepts
- ✓ Can explain workflows clearly
- ✓ Prepared answers to common questions
- ✓ Practiced explaining scenarios
- ✓ Know command reference

## Cleanup

```bash
rm -f my-workflow.txt hotfix-process.txt scenario-answer.txt
```

## Interview Tips

1. **Understand the "why"** not just the "how"
   - Why merge vs rebase?
   - Why branch protection?
   - Why code review?

2. **Use real examples**
   - "In my last project..."
   - "Our team faced..."
   - "I solved this by..."

3. **Show problem-solving**
   - Ask clarifying questions
   - Explain your approach
   - Discuss trade-offs

4. **Be honest about gaps**
   - "I haven't used that, but..."
   - "I'd need to look that up..."
   - "Here's how I'd approach..."

5. **Practice the commands**
   - Muscle memory matters
   - Don't hesitate on basics
   - Know what each flag does

## Common Interview Mistakes

| Mistake | Impact | Fix |
|---------|--------|-----|
| Confusing Git/GitHub | Looks uninformed | Understand the distinction |
| Can't explain workflows | Unclear thinking | Practice explaining |
| Doesn't know why | Shallow understanding | Learn the philosophy |
| Nervous about mistakes | Hesitation | Accept mistakes happen |
| Only theory, no practice | Unconvincing | Do hands-on practice |

## Sample Interview Scenario

**Question**: "Our main branch got corrupted. Only 2 developers have pushed. How would you recover?"

**Good Answer**:
1. Use git fsck to identify corrupted objects
2. Check if refs are intact
3. Use git reflog to find good commit
4. Reset to last good state
5. Have team re-push if needed
6. Set up better protections (no direct push to main)
7. Regular backups

## Next Steps

Once comfortable with:
- Git fundamentals
- All advanced concepts
- Interview preparation
- Quick references

You're ready for:
- Job interviews
- Team leadership
- Complex Git workflows
- Teaching Git to others

---

**Time to Complete:** 60 minutes  
**Difficulty Level:** All Levels  
**Hands-on Practice:** Yes  
**Files Generated:** exercises.md, solutions.md, cheatsheet.md
