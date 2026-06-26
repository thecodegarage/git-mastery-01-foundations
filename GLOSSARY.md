# Git Glossary - Essential Terminology

Beginner-friendly explanations of Git terms.

---

## A

### Add
**Verb**: Stage files for commit
```bash
git add <file>
```
**Simple explanation**: Tell Git "I want to include this change in my next commit"

### Amend
**Verb**: Modify the last commit
```bash
git commit --amend
```
**Simple explanation**: Fix or update your most recent commit (message or files)

---

## B

### Branch
**Noun**: Independent line of development
**Verb**: Create a new branch
```bash
git branch feature-name    # Create
git branch                 # List
```
**Simple explanation**: Like a parallel universe where you can make changes without affecting the main code. Think of it as a separate workspace.

**Visual**:
```
master:    C1 -- C2 -- C3
                \
feature:         C4 -- C5
```

### Blame
**Verb**: Show who last modified each line
```bash
git blame <file>
```
**Simple explanation**: See who wrote each line of code and when (not actually about blaming!)

---

## C

### Clone
**Verb**: Copy a remote repository to your computer
```bash
git clone <url>
```
**Simple explanation**: Download a complete copy of a project, including all its history

### Commit
**Noun**: Snapshot of your project at a point in time
**Verb**: Save staged changes to repository
```bash
git commit -m "Message"
```
**Simple explanation**: Take a permanent snapshot of your work. Like saving your game progress.

**Anatomy of a commit**:
- Hash (ID): `a1b2c3d4e5f6...`
- Author: Who made it
- Date: When it was made
- Message: What changed
- Parent: Previous commit(s)

### Checkout
**Verb**: Switch branches or restore files (older command)
```bash
git checkout <branch>      # Old way to switch
git checkout -- <file>     # Old way to restore
```
**Simple explanation**: Change what you're looking at. Replaced by `git switch` and `git restore`.

### Cherry-pick
**Verb**: Apply a commit from one branch to another
```bash
git cherry-pick <commit-hash>
```
**Simple explanation**: Copy a specific commit to your current branch (like copy-paste for commits)

---

## D

### Diff
**Noun/Verb**: Show changes between versions
```bash
git diff                   # Unstaged changes
git diff --staged          # Staged changes
```
**Simple explanation**: See what's different. Green (+) = additions, Red (-) = deletions.

### Detached HEAD
**State**: HEAD points to commit instead of branch
**Simple explanation**: Looking at history without being on a branch. Not dangerous, just confusing. Use `git switch <branch>` to get back.

---

## F

### Fetch
**Verb**: Download commits from remote without merging
```bash
git fetch origin
```
**Simple explanation**: Check what's new on the server without changing your local work

### Fast-forward
**Merge type**: Move branch pointer forward (no merge commit)
**Simple explanation**: When merging, if there's a straight line, Git just moves the pointer instead of creating a merge commit

**Visual**:
```
Before:
master:  C1 -- C2
feature:        \-- C3 -- C4

After fast-forward:
master:  C1 -- C2 -- C3 -- C4
```

---

## G

### .git/
**Directory**: Hidden folder containing all Git data
**Simple explanation**: Git's brain. Contains all commits, branches, configuration. Don't manually edit!

### .gitignore
**File**: List of files Git should ignore
```
node_modules/
*.log
.env
```
**Simple explanation**: Tell Git to ignore certain files (like temporary files, secrets, or build outputs)

---

## H

### HEAD
**Pointer**: Current commit/branch you're working on
**Simple explanation**: "You are here" marker. Points to your current location in Git history.

```bash
HEAD      → current commit
HEAD~1    → 1 commit ago (parent)
HEAD~2    → 2 commits ago (grandparent)
HEAD^     → same as HEAD~1
```

### Hash
**Noun**: Unique ID for commits
**Example**: `a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8s9t0`
**Simple explanation**: Commit's fingerprint. First 7 characters usually enough: `a1b2c3d`

### History
**Noun**: Record of all commits
```bash
git log
```
**Simple explanation**: Timeline of all changes made to project

---

## I

### Index
**Noun**: Another name for staging area
**Simple explanation**: Same as staging area (see Staging Area)

### Init
**Verb**: Create new Git repository
```bash
git init
```
**Simple explanation**: Start Git tracking in a folder. Creates `.git` directory.

---

## L

### Log
**Verb**: View commit history
```bash
git log
git log --oneline
git log --graph
```
**Simple explanation**: See the list of all commits made to project

---

## M

### Master / Main
**Branch**: Default main branch name
**Simple explanation**: Primary branch of your project. `master` is traditional name, `main` is newer standard.

### Merge
**Verb**: Combine branches together
```bash
git merge <branch-name>
```
**Simple explanation**: Bring changes from one branch into another. Integrates work.

**Visual**:
```
master:  C1 -- C2 ---------- M
                \           /
feature:         C3 -- C4 --
```

### Merge Conflict
**State**: Same line edited differently in two branches
**Simple explanation**: Git can't automatically merge because two changes conflict. You must manually decide which to keep.

**Conflict markers**:
```
<<<<<<< HEAD
Your version
=======
Their version
>>>>>>> branch-name
```

---

## O

### Origin
**Remote**: Default name for cloned repository
```bash
git remote -v
# origin  https://github.com/user/repo.git
```
**Simple explanation**: Nickname for the server you cloned from (usually GitHub, GitLab, etc.)

---

## P

### Pull
**Verb**: Fetch and merge in one command
```bash
git pull origin master
```
**Simple explanation**: Download changes from server AND merge them. `git fetch` + `git merge`

### Push
**Verb**: Upload commits to remote
```bash
git push origin master
```
**Simple explanation**: Send your commits to the server so others can see them

### Pull Request (PR)
**Noun**: Request to merge your changes (GitHub/GitLab feature)
**Simple explanation**: "Hey, I made changes. Can you review and merge them?" Not a Git command, but a GitHub/GitLab feature.

---

## R

### Repository (Repo)
**Noun**: Project tracked by Git
**Simple explanation**: Folder with `.git` directory. Contains all files and their history.

### Remote
**Noun**: Server hosting repository
**Simple explanation**: The server (like GitHub) where repository is stored online

### Rebase
**Verb**: Reapply commits on top of another branch
```bash
git rebase master
```
**Simple explanation**: Move your commits to start from a different point. Rewrites history.

**Visual**:
```
Before:
master:  C1 -- C2 -- C3
feature:      \-- C4 -- C5

After rebase:
master:  C1 -- C2 -- C3
feature:                \-- C4' -- C5'
```

### Reset
**Verb**: Undo commits
```bash
git reset --soft HEAD~1    # Keep changes
git reset --hard HEAD~1    # Discard changes
```
**Simple explanation**: Move back in time. Can keep or discard changes.

### Restore
**Verb**: Discard changes or unstage files (newer command)
```bash
git restore <file>              # Discard changes
git restore --staged <file>     # Unstage
```
**Simple explanation**: Undo changes in working directory or staging area

### Revert
**Verb**: Create new commit that undoes previous commit
```bash
git revert <commit-hash>
```
**Simple explanation**: Safe undo - creates NEW commit that reverses changes (doesn't delete history)

### Reflog
**Noun**: Log of all HEAD movements
```bash
git reflog
```
**Simple explanation**: Safety net! Shows everywhere HEAD has been. Can recover "lost" commits.

---

## S

### SHA / SHA-1
**Noun**: Commit hash algorithm
**Simple explanation**: The long hexadecimal ID for commits (hash)

### Stage / Staging Area
**Noun**: Place where changes wait before committing
**Verb**: Add files to staging area
```bash
git add <file>    # Stage files
```
**Simple explanation**: Preparation area for your next commit. Like packing a box before shipping.

**Flow**:
```
Working Directory → (git add) → Staging Area → (git commit) → Repository
```

### Stash
**Verb/Noun**: Temporarily save uncommitted changes
```bash
git stash           # Save changes
git stash pop       # Restore changes
```
**Simple explanation**: Set aside your work temporarily without committing. Like putting papers in a drawer.

### Status
**Verb**: Show current state of working directory
```bash
git status
```
**Simple explanation**: See what's changed, staged, or untracked. Most used Git command!

### Switch
**Verb**: Change branches (newer command)
```bash
git switch <branch-name>
git switch -c <new-branch>
```
**Simple explanation**: Move to different branch. Replaces `git checkout` for switching.

---

## T

### Tag
**Noun**: Named reference to specific commit
```bash
git tag v1.0.0
git tag -a v1.0.0 -m "Release 1.0"
```
**Simple explanation**: Bookmark for important commits (like releases)

### Tracked / Untracked
**State**: Whether Git is watching a file
- **Tracked**: Git knows about file
- **Untracked**: New file Git hasn't seen
```bash
git status  # Shows tracked/untracked
```

### Tree
**Noun**: Git's internal structure for files/folders
**Simple explanation**: How Git organizes files internally. Usually don't need to worry about this.

---

## U

### Unstage
**Verb**: Remove files from staging area
```bash
git restore --staged <file>
```
**Simple explanation**: Undo `git add` - move changes back to working directory

### Upstream
**Noun**: Remote branch your branch tracks
```bash
git push -u origin master    # Set upstream
```
**Simple explanation**: The remote branch your local branch is linked to

### Untracked
**State**: Files Git doesn't know about yet
**Simple explanation**: New files that haven't been added (`git add`) yet. Show up in red in `git status`

---

## W

### Working Directory / Working Tree
**Noun**: Your actual files (what you see)
**Simple explanation**: The regular files and folders you edit. Changes here are "uncommitted"

**Three areas**:
1. **Working Directory**: Files you're editing
2. **Staging Area**: Changes prepared for commit
3. **Repository**: Committed history

---

## Common Terms Explained

### "Clean working directory"
**Meaning**: No uncommitted changes
```bash
git status
# Output: nothing to commit, working tree clean
```

### "Fast-forward merge"
**Meaning**: Branch merged by moving pointer (no merge commit)

### "Detached HEAD state"
**Meaning**: Looking at commit directly, not through a branch

### "Upstream branch"
**Meaning**: Remote branch your local branch tracks

### "Tracking branch"
**Meaning**: Local branch linked to remote branch

### "Origin/master" vs "master"
- `master`: Your local branch
- `origin/master`: Your local copy of remote's master branch
- `origin`: The remote itself

---

## Command Translations

### Old → New
Git updated some commands for clarity:

| Old Command | New Command | Purpose |
|------------|-------------|---------|
| `git checkout <branch>` | `git switch <branch>` | Change branches |
| `git checkout -b <branch>` | `git switch -c <branch>` | Create & switch |
| `git checkout -- <file>` | `git restore <file>` | Discard changes |
| `git reset HEAD <file>` | `git restore --staged <file>` | Unstage file |

**Both work!** New commands are clearer, but old commands still supported.

---

## Visual Git Workflow

```
┌─────────────────┐
│ Working         │
│ Directory       │  git add
│ (Your files)    │ ────────► ┌──────────────┐
└─────────────────┘           │ Staging      │
       ▲                      │ Area         │  git commit
       │                      │ (Index)      │ ────────► ┌─────────────┐
       │ git restore          └──────────────┘           │ Repository  │
       │                             ▲                   │ (.git)      │
       │                             │                   └─────────────┘
       │                             │ git restore              │
       └─────────────────────────────┘  --staged               │
                                                                │
                                    git push │          │ git pull
                                             ▼          ▼
                                         ┌──────────────────┐
                                         │ Remote           │
                                         │ (GitHub, etc.)   │
                                         └──────────────────┘
```

---

## 🎓 Study Tips

### Essential Terms to Know
1. **Repository**: Your project
2. **Commit**: Snapshot of changes
3. **Branch**: Independent line of work
4. **Stage**: Prepare changes
5. **Remote**: Server with your code
6. **Push**: Send changes to server
7. **Pull**: Get changes from server
8. **Merge**: Combine branches
9. **HEAD**: Where you are now
10. **Origin**: Default remote name

### When You See...
- **Red text in git status**: Unstaged or untracked
- **Green text in git status**: Staged, ready to commit
- **Plus signs (+)**: Additions in diff
- **Minus signs (-)**: Deletions in diff
- **<<<<<<< HEAD**: Start of conflict
- **=======**: Separator in conflict
- **>>>>>>> branch**: End of conflict

---

## 🔗 Related Resources

- **README.md**: Project overview and objectives
- **EXERCISES.md**: Hands-on practice
- **SOLUTIONS.md**: Exercise answers
- **TROUBLESHOOTING.md**: Fix common problems
- **GIT-CHEATSHEET.md**: Command reference

---

**Pro Tip**: Don't try to memorize everything! Refer back to this glossary when you encounter unfamiliar terms. Understanding comes with practice.
