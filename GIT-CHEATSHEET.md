# Git Cheat Sheet - Foundations

Quick reference for essential Git commands.

## ⚙️ Configuration

```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Set default editor
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"          # Vim

# View configuration
git config --list
git config user.name
git config user.email

# Configuration levels
git config --global   # User-level (~/.gitconfig)
git config --local    # Repository-level (.git/config)
git config --system   # System-level
```

## 📦 Creating Repositories

```bash
# Initialize new repository
git init

# Clone existing repository
git clone <url>
git clone <url> <folder-name>

# Clone specific branch
git clone -b <branch-name> <url>
```

## 📊 Status & Information

```bash
# Check repository status
git status
git status -s  # Short format

# View commit history
git log
git log --oneline
git log --oneline --graph --all
git log --stat                    # Show files changed
git log -p                        # Show actual changes
git log -n 5                      # Last 5 commits
git log --author="Name"
git log --grep="search term"
git log --since="2 weeks ago"
git log --until="yesterday"

# View specific commit
git show <commit-hash>
git show HEAD
git show HEAD~1  # Previous commit
git show HEAD~2  # 2 commits ago

# View file history
git log -- <file>
git log -p -- <file>

# Count commits
git rev-list --count HEAD
```

## ➕ Staging & Committing

```bash
# Stage files
git add <file>
git add <file1> <file2>
git add .              # All files in current directory
git add -A             # All files in repository
git add *.js           # All JS files
git add src/           # All files in directory

# View staged changes
git diff --staged
git diff --cached

# Unstage files
git restore --staged <file>
git reset HEAD <file>           # Old way

# Commit
git commit -m "Commit message"
git commit                      # Opens editor for message
git commit -am "Message"        # Stage all tracked files and commit

# Amend last commit
git commit --amend -m "New message"
git commit --amend --no-edit    # Keep same message
```

## 🔍 Viewing Changes

```bash
# View unstaged changes
git diff
git diff <file>

# View staged changes
git diff --staged
git diff --cached

# Compare commits
git diff <commit1> <commit2>
git diff HEAD~1 HEAD

# Compare branches
git diff <branch1>..<branch2>
git diff master..feature-branch

# Show changed files only
git diff --name-only
git diff --name-status
```

## ↩️ Undoing Changes

```bash
# Discard changes in working directory
git restore <file>
git checkout -- <file>          # Old way

# Unstage files
git restore --staged <file>
git reset HEAD <file>           # Old way

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert a commit (creates new commit)
git revert <commit-hash>

# Reset to specific commit
git reset --hard <commit-hash>  # DANGEROUS: loses changes
git reset --soft <commit-hash>  # Keep changes staged
git reset --mixed <commit-hash> # Keep changes unstaged
```

## 🌿 Branching

```bash
# List branches
git branch              # Local branches
git branch -r           # Remote branches
git branch -a           # All branches
git branch -v           # With last commit

# Create branch
git branch <branch-name>

# Switch branch
git switch <branch-name>
git checkout <branch-name>      # Old way

# Create and switch
git switch -c <branch-name>
git checkout -b <branch-name>   # Old way

# Rename branch
git branch -m <old-name> <new-name>
git branch -m <new-name>        # Rename current branch

# Delete branch
git branch -d <branch-name>     # Safe delete (must be merged)
git branch -D <branch-name>     # Force delete

# Show current branch
git branch --show-current
```

## 🔀 Merging

```bash
# Merge branch into current branch
git merge <branch-name>

# Merge with no fast-forward
git merge --no-ff <branch-name>

# Merge with commit message
git merge <branch-name> -m "Merge message"

# Abort merge
git merge --abort

# View merged branches
git branch --merged
git branch --no-merged
```

## 🌐 Remote Repositories

```bash
# View remotes
git remote
git remote -v
git remote show origin

# Add remote
git remote add <name> <url>
git remote add origin https://github.com/user/repo.git

# Remove remote
git remote remove <name>
git remote rm <name>

# Rename remote
git remote rename <old> <new>

# Fetch from remote
git fetch <remote>
git fetch origin
git fetch --all

# Pull (fetch + merge)
git pull <remote> <branch>
git pull origin master
git pull                        # From tracking branch

# Push to remote
git push <remote> <branch>
git push origin master
git push -u origin master       # Set upstream tracking
git push                        # To tracking branch

# Push all branches
git push --all origin

# Push tags
git push --tags

# View remote branches
git branch -r
git ls-remote
```

## 🏷️ Tags

```bash
# List tags
git tag
git tag -l "v1.*"

# Create lightweight tag
git tag <tag-name>
git tag v1.0.0

# Create annotated tag
git tag -a <tag-name> -m "Message"
git tag -a v1.0.0 -m "Release version 1.0.0"

# Tag specific commit
git tag <tag-name> <commit-hash>

# View tag details
git show <tag-name>

# Delete tag
git tag -d <tag-name>

# Push tag to remote
git push origin <tag-name>
git push origin --tags
```

## 🙈 Ignoring Files

```bash
# Create .gitignore
touch .gitignore

# Common patterns
node_modules/     # Ignore directory
*.log             # Ignore all .log files
!important.log    # Exception (don't ignore this)
build/            # Build artifacts
.env              # Environment files
*.tmp             # Temporary files

# Check if file is ignored
git check-ignore <file>
git check-ignore -v <file>  # Show which rule

# List ignored files
git status --ignored

# Remove tracked file now in .gitignore
git rm --cached <file>
git rm -r --cached <directory>
```

## 🔧 Stashing (Preview for Later)

```bash
# Save work in progress
git stash
git stash save "Message"

# List stashes
git stash list

# Apply most recent stash
git stash apply
git stash pop  # Apply and remove

# Apply specific stash
git stash apply stash@{1}

# Delete stash
git stash drop stash@{0}
git stash clear  # Delete all
```

## 🔍 Searching & Debugging

```bash
# Search for text in files
git grep "search term"
git grep -n "search term"  # Show line numbers

# Find who changed a line
git blame <file>
git blame -L 10,20 <file>  # Lines 10-20

# Find commit that introduced a bug (advanced)
git bisect start
git bisect bad           # Current commit is bad
git bisect good <commit> # Known good commit
# Git checks out commits to test
git bisect reset         # When done
```

## 📚 Help & Documentation

```bash
# Get help
git help <command>
git <command> --help
git <command> -h       # Quick help

# Examples
git help commit
git help merge
git log --help
```

## 🎯 Common Workflows

### Starting Work
```bash
git status              # Check current state
git pull                # Get latest changes
git switch -c feature   # Create feature branch
# ... make changes ...
git add .
git commit -m "Add feature"
git push -u origin feature
```

### Daily Workflow
```bash
git status              # What's changed?
git diff                # Review changes
git add <files>         # Stage changes
git commit -m "Message" # Commit
git push                # Share with team
```

### Before Switching Branches
```bash
git status              # Any uncommitted changes?
git stash               # Save work in progress
git switch <branch>     # Switch branch
git stash pop           # Restore work
```

## ⚠️ Dangerous Commands

These commands can lose work - use carefully!

```bash
# Resets and discards work
git reset --hard
git clean -fd
git checkout -- <file>

# Rewrites history (bad for shared branches)
git commit --amend
git rebase
git reset
git filter-branch

# Force push (overwrites remote)
git push --force
```

## 💡 Pro Tips

```bash
# Create aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --all'

# Now use shortcuts
git st      # Instead of git status
git co      # Instead of git checkout
git visual  # Pretty log
```

## 🚀 Quick Reference

| Command | Purpose |
|---------|---------|
| `git status` | Check what's changed |
| `git add <file>` | Stage file |
| `git commit -m "msg"` | Commit changes |
| `git push` | Upload to remote |
| `git pull` | Download from remote |
| `git log` | View history |
| `git diff` | See changes |
| `git branch` | List branches |
| `git switch <branch>` | Change branch |
| `git merge <branch>` | Merge branch |
| `git restore <file>` | Discard changes |

---

**Remember:** `git status` and `git log` are your friends. Use them often!
