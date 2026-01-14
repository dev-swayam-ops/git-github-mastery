# 07-github-pull-requests-and-code-review: Cheatsheet

## Creating Pull Requests

| Command | Purpose | Example |
|---------|---------|---------|
| `gh pr create` | Create a new PR | `gh pr create --title "Add feature" --body "Description"` |
| `gh pr create --draft` | Create draft PR | `gh pr create --draft` |
| `gh pr create --reviewer` | Add reviewers | `gh pr create --reviewer user1,user2` |
| `gh pr create --assignee` | Assign to user | `gh pr create --assignee @me` |
| `gh pr create --label` | Add labels | `gh pr create --label "bug,urgent"` |

## Reviewing Pull Requests

| Command | Purpose | Example |
|---------|---------|---------|
| `gh pr list` | List open PRs | `gh pr list --state open` |
| `gh pr view PR#` | View PR details | `gh pr view 42` |
| `gh pr view PR# --web` | Open PR in browser | `gh pr view 42 --web` |
| `gh pr diff PR#` | Show PR changes | `gh pr diff 42` |
| `gh pr review PR#` | Start review | `gh pr review 42` |

## Reviewing Code

| Command | Purpose | Example |
|---------|---------|---------|
| `gh pr review PR# --approve` | Approve PR | `gh pr review 42 --approve` |
| `gh pr review PR# --request-changes` | Request changes | `gh pr review 42 --request-changes` |
| `gh pr review PR# --comment` | Add comment | `gh pr review 42 --comment --body "Looks good"` |
| `gh pr comment PR#` | Comment on PR | `gh pr comment 42 --body "Nice work"` |

## Merging Pull Requests

| Command | Purpose | Example |
|---------|---------|---------|
| `gh pr merge PR#` | Merge PR | `gh pr merge 42` |
| `gh pr merge PR# --merge` | Create merge commit | `gh pr merge 42 --merge` |
| `gh pr merge PR# --squash` | Squash commits | `gh pr merge 42 --squash` |
| `gh pr merge PR# --rebase` | Rebase and merge | `gh pr merge 42 --rebase` |
| `gh pr merge PR# --delete-branch` | Delete branch after merge | `gh pr merge 42 --delete-branch` |

## Common Git Workflows for PRs

| Task | Command | Purpose |
|------|---------|---------|
| Create feature branch | `git checkout -b feature/name` | Start new work |
| Push to fork | `git push origin feature/name` | Make PR-ready |
| Keep branch updated | `git fetch origin main && git rebase origin/main` | Avoid conflicts |
| Resolve conflicts | `git rebase origin/main` (fix conflicts) `git rebase --continue` | Clean merge |
| Delete local branch | `git branch -d feature/name` | Clean up |

## PR Status & Checks

| Status | Meaning | Action |
|--------|---------|--------|
| Open | PR awaiting review | Request review, wait for feedback |
| Draft | Work in progress | Convert to ready when done |
| Approved | Reviewer approved | Safe to merge |
| Changes Requested | Needs work | Address feedback, push updates |
| Merged | Successfully merged | Complete |
| Closed | PR rejected/abandoned | Close if no longer needed |

## Code Review Checklist

- [ ] Code follows project style guide
- [ ] No obvious bugs or logic errors
- [ ] Functions have clear purpose
- [ ] Tests are included or updated
- [ ] Documentation updated if needed
- [ ] Performance impact considered
- [ ] Security implications reviewed
- [ ] No hardcoded values or secrets

## PR Description Template

```markdown
## Description
Brief explanation of what this PR does

## Changes
- Change 1
- Change 2
- Change 3

## Testing
How was this tested? What scenarios?

## Related Issues
Closes #issue-number

## Checklist
- [ ] Tests pass
- [ ] Code documented
- [ ] No breaking changes
```

## Merge Strategies Comparison

| Strategy | Use When | Pros | Cons |
|----------|----------|------|------|
| Create Merge Commit | Keeping full history important | Preserves all commits | Clutters history |
| Squash | Feature is one logical unit | Clean history | Loses intermediate commits |
| Rebase | Want linear history | Linear, clean commits | Rewrites history (avoid on shared branches) |

## Helpful GitHub Web Features

### Files Changed Tab
- View all files modified
- See line-by-line changes
- Add comments to specific lines
- View file history

### Conversation Tab
- Overall PR discussion
- Review summaries
- Status checks

### Checks Tab
- CI/CD pipeline results
- Test results
- Code quality scores
- Deploy previews

## Shortcuts & Tips

1. **Quick comment on line** - Hover over line number in "Files changed" tab, click +
2. **Suggest changes** - Click suggestion button when commenting
3. **Resolve conversation** - Mark thread as resolved after fix
4. **Request more reviewers** - Use "Request reviewers" if initial reviewers unavailable
5. **Auto-link issues** - Type "Closes #123" in description
6. **Draft PR** - Mark as draft if still working on changes
7. **WIP prefix** - Use "WIP:" in title if not ready to merge

## Performance Tips

- **Keep PRs small** - Easier to review
- **Limit scope** - One feature per PR
- **Test locally first** - Catch obvious errors before PR
- **Respond to reviews promptly** - Don't leave PRs hanging
- **Review others' PRs** - Build team knowledge sharing
