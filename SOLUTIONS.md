# Exercise Solutions - Foundations

Detailed solutions for all exercises. **Try exercises yourself first!**

---

## 🟢 Getting Started Solutions

### Exercise 1: Your First Repository

**Solution:**
```bash
# Check Git version
git --version

# Configure (if needed)
git config --global user.name "Jane Doe"
git config --global user.email "jane@example.com"

# Navigate to repository
cd git-mastery-01-foundations

# Check status
git status
# Output: On branch master (or main)

# Explore .git folder
ls -la .git/
# Shows: objects, refs, config, HEAD, etc.
```

**Key Points:**
- `.git` folder contains all repository data
- Never manually edit `.git` files
- Configuration can be global or local

---

### Exercise 2: Your First Commit

**Solution:**
```bash
# Check untracked files
git status

# Stage and commit HTML
git add index.html
git commit -m "Add portfolio homepage"

# Stage and commit CSS
git add style.css
git commit -m "Add stylesheet for portfolio"

# Stage and commit JavaScript
git add script.js
git commit -m "Add interactive functionality"

# Verify
git log --oneline
# Should show 3 commits
```

**Alternative Approach:**
```bash
# Commit all at once
git add index.html style.css script.js
git commit -m "Initial portfolio website setup

- Add homepage structure
- Add styling
- Add interactive features"
```

**Key Points:**
- Can commit files individually or together
- Individual commits = more granular history
- Group commit = simpler when changes are related

---

### Exercise 3: Understanding Staging Area

**Solution:**
```bash
# Modify both files
# (edit index.html and style.css)

# Check status
git status
# Both show as modified (red)

# Stage only HTML
git add index.html
git status
# HTML green, CSS red

# Commit HTML
git commit -m "Personalize portfolio title"

# Stage and commit CSS
git add style.css
git commit -m "Update background color"

# Verify
git log --oneline -n 2
```

**Why Stage Separately?**
- Keeps commits focused and logical
- Easier to review history
- Can revert one change without affecting the other

**Key Points:**
- Staging area = "proposed next commit"
- Can stage subset of changes
- Each commit should be one logical change

---

## 🟡 Working with History Solutions

### Exercise 4: Viewing Commit History

**Solution:**
```bash
# Full history
git log

# Condensed
git log --oneline

# With graph
git log --oneline --graph --all --decorate

# Last 3 commits
git log --oneline -n 3

# Search by message
git log --grep="portfolio"

# By author
git log --author="Jane Doe"

# With file statistics
git log --stat

# With actual changes
git log -p

# View specific commit
git show HEAD
```

**Understanding Output:**
```
commit a1b2c3d4e5f6g7h8i9j0  ← Commit hash (SHA)
Author: Jane Doe <jane@example.com>  ← Who
Date:   Thu Jun 26 10:30:00 2026  ← When

    Add portfolio homepage  ← Commit message
```

**Key Points:**
- `--oneline` for quick overview
- `-p` to see actual code changes
- `--graph` visualizes branches
- `HEAD` = current commit

---

### Exercise 5: Viewing Changes

**Solution:**
```bash
# Modify index.html
# (add about section)

# View changes (unstaged)
git diff
git diff index.html

# Stage the change
git add index.html

# View changes (staged)
git diff --staged

# Commit
git commit -m "Add about section"

# View the commit
git show HEAD
```

**Understanding Diff Output:**
```diff
diff --git a/index.html b/index.html
index a1b2c3d..e4f5g6h 100644
--- a/index.html          ← Old version
+++ b/index.html          ← New version
@@ -10,6 +10,10 @@        ← Line numbers
 <body>
   <h1>Portfolio</h1>
+  <section id="about">  ← Added (green)
+    <h2>About Me</h2>
+  </section>
-  <p>Old text</p>        ← Removed (red)
 </body>
```

**Key Points:**
- Green (+) = additions
- Red (-) = deletions
- White = unchanged context
- `git diff` vs `git diff --staged` vs `git show`

---

### Exercise 6: Undoing Changes

**Solution:**
```bash
# Make bad change to style.css
# (background-color: red)

# View change
git diff style.css

# Undo (discard changes)
git restore style.css

# Verify
git diff  # Should be empty

# Make change and stage it
# (edit again)
git add style.css

# Unstage
git restore --staged style.css

# Check status
git status  # Unstaged (red)

# Discard again
git restore style.css
```

**Visual Flow:**
```
Working Directory → (git add) → Staging Area → (git commit) → Repository
     ↑                              ↑
     └── git restore <file> ────────┘
     └── git restore --staged <file> ─┘
```

**Key Points:**
- `git restore <file>` = discard working changes
- `git restore --staged <file>` = unstage
- Discarded changes are LOST (can't recover)
- Always check `git diff` before restoring

---

## 🔵 Branching Basics Solutions

### Exercise 7: Creating Your First Branch

**Solution:**
```bash
# Check current branch
git branch
# * master

# Create new branch
git branch feature/add-projects

# List branches
git branch
# * master
#   feature/add-projects

# Switch to new branch
git switch feature/add-projects

# Verify
git branch --show-current
# feature/add-projects

# Create and switch in one command
git switch -c feature/contact-form

# List all branches
git branch
# * feature/contact-form
#   feature/add-projects
#   master
```

**Understanding Branches:**
- Branch = pointer to a commit
- Creating branch = creating pointer (fast!)
- HEAD = pointer to current branch
- Branches are cheap - use them freely

**Key Points:**
- `git branch` = list or create
- `git switch` = change branches (new command)
- `git checkout` = older command for switching
- Branch names: lowercase, dashes, forward slashes

---

### Exercise 8: Working on a Branch

**Solution:**
```bash
# Switch to feature branch
git switch feature/add-projects

# Create projects.html
cat > projects.html << 'EOF'
<!DOCTYPE html>
<html>
<head>
  <title>My Projects</title>
</head>
<body>
  <h1>My Projects</h1>
  <div class="project">
    <h2>Portfolio Website</h2>
    <p>Built with HTML, CSS, and JavaScript</p>
  </div>
</body>
</html>
EOF

# Commit
git add projects.html
git commit -m "Add projects page"

# Modify index.html
# (add navigation link)

# Commit
git add index.html
git commit -m "Add navigation link to projects"

# Verify
git log --oneline -n 2

# Switch to master
git switch master
ls projects.html  # Doesn't exist!

# Switch back
git switch feature/add-projects
ls projects.html  # Exists!
```

**Branch Visualization:**
```
master:           C1 -- C2 -- C3
                        \
feature/add-projects:    C4 -- C5
```

**Key Points:**
- Each branch has its own file state
- Switching branches changes working directory
- Commits on branch don't affect master until merged
- Can switch between branches anytime (if clean)

---

### Exercise 9: Merging a Feature Branch

**Solution:**
```bash
# Switch to target branch (master)
git switch master

# View history before merge
git log --oneline --graph --all

# Merge feature branch
git merge feature/add-projects
# Fast-forward merge (if possible)

# View updated history
git log --oneline --graph

# Verify files
ls projects.html  # Now exists on master!

# Delete feature branch (cleanup)
git branch -d feature/add-projects

# Verify deletion
git branch
# * master
```

**Merge Visualization:**
```
Before:
master:           C1 -- C2 -- C3
                        \
feature:                 C4 -- C5

After (fast-forward):
master:           C1 -- C2 -- C3 -- C4 -- C5
```

**Key Points:**
- Always merge FROM feature TO master
- Switch to target branch first
- Fast-forward = linear history (no merge commit)
- Delete feature branches after merging

---

### Exercise 10: Merge with Merge Commit

**Solution:**
```bash
# Create and switch to new branch
git switch -c feature/footer

# Add footer to index.html
# (edit file)

# Commit
git add index.html
git commit -m "Add footer section"

# Switch to master
git switch master

# Merge with no fast-forward
git merge --no-ff feature/footer -m "Merge footer feature"

# View history
git log --oneline --graph -n 5
```

**Merge Commit Visualization:**
```
master:      C1 -- C2 ----------- M
                    \           /
feature/footer:      C3 -- C4 --
```

**When to Use --no-ff:**
- Preserve branch history
- Track when features were merged
- Group related commits together
- Team policy requires it

**Key Points:**
- `--no-ff` creates merge commit
- Merge commit has two parents
- Preserves branch structure in history
- Useful for feature tracking

---

## 🟣 Remote Basics Solutions

### Exercise 11: Understanding Remotes

**Solution:**
```bash
# List remotes
git remote
# origin

# Show URLs
git remote -v
# origin  https://github.com/user/repo.git (fetch)
# origin  https://github.com/user/repo.git (push)

# Detailed info
git remote show origin

# Remote branches
git branch -r
# origin/master
# origin/feature-1

# All branches
git branch -a
# * master
#   feature-1
#   remotes/origin/master
#   remotes/origin/feature-1
```

**Understanding Remotes:**
- `origin` = default remote name (convention)
- Remote branches = `origin/branch-name`
- Can have multiple remotes (origin, upstream, etc.)
- Remotes are just URLs + names

**Key Points:**
- Cloned repos automatically have `origin`
- Remote branches are read-only locally
- `git remote show` gives detailed info
- Can add/remove remotes as needed

---

### Exercise 12: Fetching and Pulling

**Solution:**
```bash
# Check current status
git status

# Fetch from remote
git fetch origin

# View remote branch
git log origin/master --oneline -n 5

# Compare local with remote
git log master..origin/master   # On remote, not local
git log origin/master..master   # On local, not remote

# Pull (fetch + merge)
git pull origin master

# Verify up to date
git status
```

**Fetch vs Pull:**
```
git fetch:
  Remote → origin/master (local copy of remote)
  Your master stays unchanged
  Safe - lets you review

git pull = git fetch + git merge:
  Remote → origin/master → master
  Updates your working directory
  Convenient but can surprise
```

**Key Points:**
- `git fetch` = download, don't merge
- `git pull` = download and merge
- Always safe to fetch
- Review changes before pulling

---

### Exercise 13: Pushing Changes

**Solution:**
```bash
# Make local change
# (edit index.html)
git add index.html
git commit -m "Update copyright year to 2026"

# Check status
git status
# "Your branch is ahead of 'origin/master' by 1 commit"

# Push to remote
git push origin master

# Verify
git status
# "Your branch is up to date with 'origin/master'"

# View remote log
git log origin/master --oneline -n 3
```

**Push Scenarios:**
```bash
# First push (set upstream)
git push -u origin master

# Subsequent pushes
git push

# Push new branch
git push -u origin feature-branch

# Push all branches
git push --all origin
```

**Key Points:**
- `git push` uploads local commits
- Can't push if remote has new commits (pull first)
- `-u` sets upstream tracking
- Requires write permissions

---

## 🔴 Best Practices Solutions

### Exercise 14: Using .gitignore

**Solution:**
```bash
# Create files that shouldn't be tracked
mkdir node_modules
touch node_modules/package.txt
touch debug.log
touch personal-notes.txt

# Check status (all shown)
git status

# Create .gitignore
cat > .gitignore << EOF
# Dependencies
node_modules/

# Logs
*.log

# Personal files
personal-notes.txt

# OS files
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
EOF

# Check status (only .gitignore shown)
git status

# Commit .gitignore
git add .gitignore
git commit -m "Add gitignore for dependencies and logs"

# Verify ignored files
git status --ignored
```

**Common .gitignore Patterns:**
```gitignore
# Files
secret.txt
config.local.json

# Patterns
*.log
*.tmp
*.swp

# Directories
node_modules/
build/
dist/
.cache/

# Exceptions
!important.log
```

**Key Points:**
- Create .gitignore early
- .gitignore itself should be tracked
- Patterns: wildcards, directories, exceptions
- Can't ignore already-tracked files (remove first)

---

### Exercise 15: Writing Good Commit Messages

**Solution:**
```bash
# Good short message
git add style.css
git commit -m "Make header responsive on mobile devices"

# Detailed message (opens editor)
git add script.js
git commit
```

**In Editor:**
```
Add form validation for contact form

- Validate email format with regex
- Require all fields before submission
- Show error messages for invalid input
- Improve user experience

Fixes #42
```

**Commit Message Best Practices:**

**Good Messages:**
```bash
✅ "Add user authentication system"
✅ "Fix navigation bug on mobile Safari"
✅ "Refactor database connection logic"
✅ "Update dependencies to latest versions"
```

**Bad Messages:**
```bash
❌ "Update"
❌ "Fix stuff"
❌ "WIP"
❌ "asdf"
❌ "Fixed bug" (which bug?)
```

**Message Structure:**
```
Short summary (50 chars or less)
<blank line>
Detailed explanation of what and why
- Bullet points for multiple changes
- Keep line length under 72 characters
- Use imperative mood: "Add" not "Added"

Fixes #123
```

**Key Points:**
- First line: imperative mood, < 50 chars
- Blank line separates summary from body
- Body: explain WHY, not just WHAT
- Reference issues/tickets if applicable

---

## 🎓 General Tips

### Understanding Git Flow
```bash
# 1. Check status
git status

# 2. See what changed
git diff

# 3. Stage changes
git add <files>

# 4. Review staged changes
git diff --staged

# 5. Commit
git commit -m "Message"

# 6. Push (if using remote)
git push
```

### When Things Go Wrong
```bash
# Uncommitted changes, need to switch branches
git stash
git switch other-branch
git stash pop

# Committed to wrong branch
git switch correct-branch
git cherry-pick <commit-hash>
git switch wrong-branch
git reset --hard HEAD~1

# Need to undo last commit
git reset --soft HEAD~1  # Keep changes
git reset --hard HEAD~1  # Discard changes

# Pushed wrong commit
# DON'T use push --force on shared branches!
# Instead: git revert <commit-hash>
```

### Making Aliases
```bash
# Create useful shortcuts
git config --global alias.st 'status'
git config --global alias.co 'checkout'
git config --global alias.br 'branch'
git config --global alias.ci 'commit'
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual 'log --oneline --graph --all --decorate'

# Use them
git st      # Instead of git status
git visual  # Pretty log
```

---

## 🎉 Congratulations!

You've completed all foundation exercises! 

### Next Steps:
1. Practice these commands daily
2. Use Git for personal projects
3. Take the quiz: `cd ../git-mastery-quiz/ && npm run dev`
4. Move to intermediate repositories:
   - Repository 2: Merge Conflicts
   - Repository 5: Remote Workflows

**Keep practicing and happy coding! 🚀**
