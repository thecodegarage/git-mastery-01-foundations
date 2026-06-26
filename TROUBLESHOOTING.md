# Troubleshooting - Git Foundations

Common issues beginners face and how to fix them.

---

## 🚨 Installation & Configuration Issues

### "git: command not found"

**Symptom**: Terminal doesn't recognize `git` command

**Causes**:
1. Git not installed
2. Git not in PATH
3. Terminal not restarted after installation

**Solutions**:
```bash
# Check if Git is installed (Mac/Linux)
which git

# Check on Windows
where git

# Install Git
# Mac: brew install git
# Ubuntu: sudo apt-get install git
# Windows: Download from https://git-scm.com/

# After installation, restart terminal
```

---

### "Please tell me who you are"

**Symptom**: Can't commit, Git asks for identity

**Full Error**:
```
*** Please tell me who you are.

Run
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```

**Solution**:
```bash
# Set your identity
git config --global user.name "Jane Doe"
git config --global user.email "jane@example.com"

# Verify
git config user.name
git config user.email
```

---

### "warning: LF will be replaced by CRLF"

**Symptom**: Warning about line endings (Windows)

**Explanation**: Windows uses CRLF, Unix uses LF for line endings

**Solution**:
```bash
# Windows: automatically convert on checkout
git config --global core.autocrlf true

# Mac/Linux: don't convert
git config --global core.autocrlf input

# To suppress warning (not recommended)
git config --global core.autocrlf false
```

---

## 📁 Repository Issues

### "fatal: not a git repository"

**Symptom**: Git commands don't work

**Causes**:
1. Not in a Git repository
2. In wrong directory
3. .git folder missing

**Solutions**:
```bash
# Check current directory
pwd

# Look for .git folder
ls -la .git

# Navigate to repository
cd /path/to/repository

# Or initialize new repository
git init
```

---

### "Nothing to commit, working tree clean"

**Symptom**: No changes detected when you made changes

**Causes**:
1. Changes not saved in editor
2. Wrong file modified
3. File is ignored (.gitignore)
4. Already committed

**Solutions**:
```bash
# Check status
git status

# List all files
ls -la

# Check if file is ignored
git check-ignore -v <filename>

# View ignored files
git status --ignored

# Check last commit
git show HEAD
```

---

## ➕ Staging Issues

### "Changes not staged for commit"

**Symptom**: Modified files but `git commit` says nothing to commit

**Explanation**: Files need to be staged before committing

**Solution**:
```bash
# Check what's modified
git status

# Stage the files
git add <filename>
# or stage all
git add .

# Now commit
git commit -m "Message"
```

---

### "Can't git add - file is ignored"

**Symptom**: `git add` says file will be ignored

**Cause**: File matches pattern in .gitignore

**Solutions**:
```bash
# Check why file is ignored
git check-ignore -v <filename>

# Option 1: Remove from .gitignore
# Edit .gitignore, remove the matching pattern

# Option 2: Force add (override ignore)
git add -f <filename>

# Option 3: Add exception to .gitignore
!<filename>  # In .gitignore
```

---

### "I added the wrong files!"

**Symptom**: Staged files you didn't mean to

**Solutions**:
```bash
# Unstage one file
git restore --staged <filename>

# Unstage all files
git restore --staged .

# Or using reset (older way)
git reset HEAD <filename>
git reset HEAD .

# Verify
git status
```

---

## 💬 Commit Issues

### "Aborting commit due to empty commit message"

**Symptom**: Commit failed because no message provided

**Solutions**:
```bash
# Use -m flag for message
git commit -m "Your commit message"

# Or let editor open (then type message and save)
git commit

# If editor opened and you cancelled
# Just run git commit again
```

---

### "I committed the wrong files!"

**Symptom**: Committed files you didn't mean to include

**Solutions**:
```bash
# Option 1: Undo commit, keep changes
git reset --soft HEAD~1
# Now unstage unwanted files
git restore --staged <unwanted-file>
# Commit again with correct files
git commit -m "Correct message"

# Option 2: Amend the commit (if it's the last one)
git reset --soft HEAD~1
git restore --staged <unwanted-file>
git commit -m "Corrected commit"

# Option 3: Remove file from last commit
git rm --cached <unwanted-file>
git commit --amend --no-edit
```

---

### "I made a typo in my commit message!"

**Symptom**: Committed with wrong message

**Solution (if it's the last commit)**:
```bash
# Change message of last commit
git commit --amend -m "Corrected message"

# Or open editor to edit
git commit --amend
```

**Warning**: Don't amend commits that are already pushed to shared repositories!

---

### "I forgot to add a file to my commit!"

**Symptom**: Committed but missed a file

**Solution (if it's the last commit)**:
```bash
# Add the missing file
git add <forgotten-file>

# Amend the last commit
git commit --amend --no-edit
# Or with new message:
git commit --amend -m "Updated message"
```

---

## 🌿 Branch Issues

### "fatal: A branch named 'X' already exists"

**Symptom**: Can't create branch with existing name

**Solutions**:
```bash
# List existing branches
git branch

# Use different name
git branch feature/new-name

# Or delete old branch first (if safe)
git branch -d feature/old-name
git branch feature/old-name
```

---

### "You are in 'detached HEAD' state"

**Symptom**: Scary message after checking out a commit

**Explanation**: HEAD points directly to commit, not a branch

**What it means**:
- You can look around
- You can make commits (but they'll be orphaned)
- Not dangerous, just confusing

**Solutions**:
```bash
# Option 1: Just looking around? Go back to branch
git switch master

# Option 2: Want to make commits? Create branch
git switch -c new-branch-name

# Option 3: Already made commits? Create branch
git branch temp-branch
git switch master
git merge temp-branch
```

---

### "Cannot delete branch - not fully merged"

**Symptom**: Can't delete branch with unmerged changes

**Solutions**:
```bash
# View unmerged changes
git diff master..feature-branch

# Option 1: Merge the branch first
git switch master
git merge feature-branch
git branch -d feature-branch

# Option 2: Force delete (LOSE CHANGES)
git branch -D feature-branch
```

---

## 🔀 Merge Issues

### "Already up to date"

**Symptom**: `git merge` says already up to date

**Causes**:
1. Branch already merged
2. No new commits on branch being merged
3. Merging in wrong direction

**Solutions**:
```bash
# Check branches
git log --oneline --graph --all

# Make sure you're on the right branch
git branch --show-current

# Merge in correct direction
# Switch to target branch (e.g., master)
git switch master
# Merge FROM feature
git merge feature-branch
```

---

### "Please commit or stash before merging"

**Symptom**: Can't merge because of uncommitted changes

**Solutions**:
```bash
# Option 1: Commit changes
git add .
git commit -m "WIP: in progress"
git merge <branch>

# Option 2: Stash changes
git stash
git merge <branch>
git stash pop

# Option 3: Discard changes (careful!)
git restore .
git merge <branch>
```

---

## ↩️ Undo Issues

### "I deleted a file by accident!"

**Symptom**: Deleted important file in working directory

**Solutions**:
```bash
# If not staged, restore from last commit
git restore <deleted-file>

# If staged, unstage then restore
git restore --staged <deleted-file>
git restore <deleted-file>

# If committed, checkout from commit
git show HEAD:<file> > <file>
```

---

### "I reset too far back!"

**Symptom**: Used `git reset --hard` and lost commits

**Solution**:
```bash
# View reflog (history of HEAD movements)
git reflog

# Find the commit before reset
# Looks like: abc1234 HEAD@{1}: reset: moving to HEAD~3

# Reset back to that commit
git reset --hard HEAD@{1}
# Or use the commit hash
git reset --hard abc1234
```

**Key Point**: Git keeps commits for ~30 days in reflog, even after reset!

---

### "I can't undo - already pushed!"

**Symptom**: Pushed wrong commits to remote

**Solution (DON'T force push on shared branches)**:
```bash
# Create new commit that undoes the bad one
git revert <commit-hash>
git push

# If multiple commits
git revert <commit1>
git revert <commit2>
git push

# Or revert a range
git revert HEAD~3..HEAD
```

---

## 🌐 Remote Issues

### "fatal: 'origin' does not appear to be a git repository"

**Symptom**: Can't push/pull/fetch

**Causes**:
1. Remote not set up
2. Typo in remote name
3. Remote URL incorrect

**Solutions**:
```bash
# List remotes
git remote -v

# Add remote
git remote add origin <url>

# Fix remote URL
git remote set-url origin <correct-url>

# Verify
git remote -v
```

---

### "Permission denied (publickey)"

**Symptom**: Can't push to GitHub/GitLab

**Causes**:
1. No SSH key set up
2. Using SSH URL without SSH key
3. Wrong credentials

**Solutions**:
```bash
# Option 1: Use HTTPS instead
git remote set-url origin https://github.com/user/repo.git

# Option 2: Set up SSH key
# Generate key
ssh-keygen -t ed25519 -C "your@email.com"
# Add to ssh-agent
ssh-add ~/.ssh/id_ed25519
# Add public key to GitHub: Settings → SSH Keys

# Test connection
ssh -T git@github.com
```

---

### "Updates were rejected because the remote contains work..."

**Symptom**: Can't push because remote has new commits

**Full Error**:
```
Updates were rejected because the remote contains work that you do
not have locally. This is usually caused by another repository pushing
to the same ref.
```

**Solutions**:
```bash
# Pull changes first
git pull origin master

# If conflicts, resolve them
# Then push
git push origin master

# Or pull with rebase (keeps linear history)
git pull --rebase origin master
git push origin master
```

---

### "fatal: refusing to merge unrelated histories"

**Symptom**: Can't pull from remote with different history

**Solutions**:
```bash
# Allow merge of unrelated histories
git pull origin master --allow-unrelated-histories

# Resolve any conflicts
# Then commit
```

---

## 🙈 .gitignore Issues

### "File still tracked even though in .gitignore"

**Symptom**: Changes to ignored file still show in `git status`

**Cause**: File was tracked before being added to .gitignore

**Solution**:
```bash
# Remove from Git tracking (keeps file locally)
git rm --cached <filename>

# For directory
git rm -r --cached <directory>

# Commit the removal
git commit -m "Stop tracking file now in gitignore"

# Now file will be ignored
```

---

## 🔧 Editor Issues

### "Git commit opens wrong editor"

**Symptom**: `git commit` (without -m) opens vim/nano/wrong editor

**Solutions**:
```bash
# Set VS Code as editor
git config --global core.editor "code --wait"

# Set nano
git config --global core.editor "nano"

# Set vim
git config --global core.editor "vim"

# Set emacs
git config --global core.editor "emacs"

# Verify
git config core.editor
```

---

### "Stuck in vim!"

**Symptom**: Commit message editor opened vim, don't know how to exit

**Solutions**:
```
# Save and exit vim:
Press ESC
Type: :wq
Press ENTER

# Exit without saving:
Press ESC
Type: :q!
Press ENTER
```

---

## 🆘 General Help

### "I don't know what I did!"

**Solutions**:
```bash
# View recent actions
git reflog

# View current status
git status

# View recent commits
git log --oneline -n 10

# See what changed
git diff

# Start fresh (WARNING: loses uncommitted changes)
git reset --hard HEAD
git clean -fd
```

---

### "How do I ask for help?"

**Resources**:
1. **Built-in help**: `git help <command>`
2. **Quick help**: `git <command> -h`
3. **This guide**: TROUBLESHOOTING.md
4. **Cheatsheet**: GIT-CHEATSHEET.md
5. **Stack Overflow**: Search "git [your problem]"
6. **Pro Git Book**: https://git-scm.com/book (free!)

**When asking for help, include**:
```bash
# Git version
git --version

# Command you ran
git <command>

# Error message (full output)

# Current status
git status

# Recent history
git log --oneline -n 5
```

---

## 💡 Prevention Tips

### Before Making Changes
```bash
# Always check status first
git status

# Make sure you're on the right branch
git branch --show-current

# Pull latest changes
git pull
```

### Before Committing
```bash
# Review what you're committing
git diff --staged

# Make sure you staged the right files
git status
```

### Before Pushing
```bash
# Make sure you're pushing to the right branch
git branch --show-current

# Check what you're pushing
git log origin/master..master --oneline
```

---

## 🚀 Quick Recovery Commands

```bash
# Undo uncommitted changes
git restore <file>

# Undo staged changes
git restore --staged <file>

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Find lost commits
git reflog

# Abort merge
git merge --abort

# Get help
git help <command>
```

---

**Remember**: Git is forgiving! Almost everything can be undone. When in doubt, check `git status` and `git reflog`.
