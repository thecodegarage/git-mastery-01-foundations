# Git Foundations - Exercises 🌱

15 hands-on exercises to master Git fundamentals.

## Exercise Format

Each exercise includes:
- **Objective**: What you'll learn
- **Scenario**: The problem setup
- **Tasks**: Step-by-step instructions
- **Validation**: How to verify success
- **Learning Points**: Key takeaways

---

## 🟢 Getting Started (Exercises 1-3)

### Exercise 1: Your First Repository

**Objective**: Initialize a Git repository and understand the `.git` folder

**Scenario**: You're starting a personal portfolio website project and want to track changes with Git.

**Tasks**:
1. Check if Git is installed:
   ```bash
   git --version
   ```

2. Configure your identity (if not done yet):
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your@email.com"
   ```

3. Navigate to this repository:
   ```bash
   pwd  # Verify you're in git-mastery-01-foundations/
   ```

4. Check Git status:
   ```bash
   git status
   ```

5. Explore the `.git` folder (DON'T modify it):
   ```bash
   ls -la .git/
   ```

**Validation**:
```bash
# Should show Git initialized
git status
# Output: "On branch master" or "On branch main"

# Check configuration
git config user.name
git config user.email
```

**Learning Points**:
- ✅ `.git` folder contains all Git history and metadata
- ✅ `git status` is your best friend - use it often!
- ✅ Configuration is stored globally or per-repository
- ✅ Git tracks the entire folder and all subfolders

---

### Exercise 2: Your First Commit

**Objective**: Stage and commit files to Git

**Scenario**: The portfolio files exist but aren't tracked. Add them to Git.

**Tasks**:
1. Check current status:
   ```bash
   git status
   ```
   Notice "untracked files" in red

2. Stage the HTML file:
   ```bash
   git add index.html
   git status  # Now shows "Changes to be committed" in green
   ```

3. Commit with a message:
   ```bash
   git commit -m "Add portfolio homepage"
   ```

4. View your commit:
   ```bash
   git log
   ```

5. Stage and commit the CSS:
   ```bash
   git add style.css
   git commit -m "Add stylesheet for portfolio"
   ```

6. Stage and commit the JavaScript:
   ```bash
   git add script.js
   git commit -m "Add interactive functionality"
   ```

**Validation**:
```bash
# Should show 3 commits
git log --oneline

# Working directory should be clean
git status
# Output: "nothing to commit, working tree clean"

# Count commits
git rev-list --count HEAD
# Should show: 3 (or more if repo has existing history)
```

**Learning Points**:
- ✅ Untracked files (red) → Staged files (green) → Committed
- ✅ Commit messages should be clear and descriptive
- ✅ Each commit is a snapshot of your project
- ✅ `git status` shows what's happening at each step

---

### Exercise 3: Understanding Staging Area

**Objective**: Learn the difference between working directory, staging area, and repository

**Scenario**: Make changes to multiple files but commit them separately.

**Tasks**:
1. Modify index.html - add your name to the title:
   ```html
   <title>John Doe - Portfolio</title>
   ```

2. Modify style.css - change a color:
   ```css
   body { background-color: #f0f0f0; }
   ```

3. Check status:
   ```bash
   git status
   ```
   Both files show as "modified" (red)

4. Stage only the HTML file:
   ```bash
   git add index.html
   git status  # HTML green, CSS still red
   ```

5. Commit the HTML change:
   ```bash
   git commit -m "Personalize portfolio title"
   ```

6. Now stage and commit the CSS:
   ```bash
   git add style.css
   git commit -m "Update background color"
   ```

**Validation**:
```bash
# Should show 2 new commits
git log --oneline -n 2

# Working directory clean
git status
```

**Learning Points**:
- ✅ Working Directory → Staging Area → Repository
- ✅ Staging lets you craft focused commits
- ✅ Can commit files separately even if modified together
- ✅ Commits should be logical, focused changes

---

## 🟡 Working with History (Exercises 4-6)

### Exercise 4: Viewing Commit History

**Objective**: Master `git log` and understand commit information

**Scenario**: Review what changes were made and when.

**Tasks**:
1. View full commit history:
   ```bash
   git log
   ```

2. View condensed one-line format:
   ```bash
   git log --oneline
   ```

3. View with graph visualization:
   ```bash
   git log --oneline --graph --all --decorate
   ```

4. View last 3 commits only:
   ```bash
   git log --oneline -n 3
   ```

5. Search commits by message:
   ```bash
   git log --grep="portfolio"
   ```

6. View commits by author:
   ```bash
   git log --author="Your Name"
   ```

7. View file changes in each commit:
   ```bash
   git log --stat
   ```

8. View actual code changes:
   ```bash
   git log -p
   ```

**Validation**:
```bash
# Get specific commit info
git show HEAD

# Count total commits
git rev-list --count HEAD
```

**Learning Points**:
- ✅ Each commit has: hash (SHA), author, date, message
- ✅ `--oneline` for quick overview
- ✅ `-p` shows actual code changes (patch)
- ✅ `--graph` visualizes branch history

---

### Exercise 5: Viewing Changes

**Objective**: Use `git diff` to see what changed

**Scenario**: You're working on updates and want to see what's different.

**Tasks**:
1. Modify index.html - add a new section:
   ```html
   <section id="about">
     <h2>About Me</h2>
     <p>I'm a developer learning Git!</p>
   </section>
   ```

2. View changes in working directory:
   ```bash
   git diff
   ```
   Shows additions in green (+), deletions in red (-)

3. View changes for specific file:
   ```bash
   git diff index.html
   ```

4. Stage the change:
   ```bash
   git add index.html
   ```

5. View staged changes:
   ```bash
   git diff --staged
   # or
   git diff --cached
   ```

6. Commit the change:
   ```bash
   git commit -m "Add about section"
   ```

7. View changes in last commit:
   ```bash
   git show HEAD
   ```

**Validation**:
```bash
# After commit, diff should be empty
git diff
git diff --staged

# Show the commit you just made
git show HEAD
```

**Learning Points**:
- ✅ `git diff` = working directory vs staging
- ✅ `git diff --staged` = staging vs repository
- ✅ `git show` = view specific commit
- ✅ Green = additions, Red = deletions

---

### Exercise 6: Undoing Changes

**Objective**: Learn to undo changes safely at different stages

**Scenario**: Made mistakes and need to revert them.

**Tasks**:
1. Modify style.css - make a bad change:
   ```css
   body { background-color: red; }  /* Ugly! */
   ```

2. View the change:
   ```bash
   git diff style.css
   ```

3. Undo the change (restore from last commit):
   ```bash
   git restore style.css
   # Old way: git checkout -- style.css
   
   git diff  # Should show nothing
   ```

4. Make change again and stage it:
   ```bash
   # Add the red background again
   git add style.css
   git status  # Staged (green)
   ```

5. Unstage the file:
   ```bash
   git restore --staged style.css
   # Old way: git reset HEAD style.css
   
   git status  # Back to unstaged (red)
   ```

6. Discard the change:
   ```bash
   git restore style.css
   ```

**Validation**:
```bash
# Working directory should be clean
git status

# File should have original content
git diff style.css  # Should show nothing
```

**Learning Points**:
- ✅ `git restore <file>` = discard working directory changes
- ✅ `git restore --staged <file>` = unstage changes
- ✅ Changes discarded with `restore` are GONE (can't recover)
- ✅ Always check `git diff` before discarding

---

## 🔵 Branching Basics (Exercises 7-10)

### Exercise 7: Creating Your First Branch

**Objective**: Create and switch between branches

**Scenario**: Want to experiment with a new feature without affecting main code.

**Tasks**:
1. Check current branch:
   ```bash
   git branch
   # Shows * master (or * main)
   ```

2. Create a new branch:
   ```bash
   git branch feature/add-projects
   ```

3. List all branches:
   ```bash
   git branch
   # Shows both branches, * indicates current
   ```

4. Switch to the new branch:
   ```bash
   git switch feature/add-projects
   # Old way: git checkout feature/add-projects
   ```

5. Verify you switched:
   ```bash
   git branch  # * should be on new branch
   git status
   ```

6. Create and switch in one command:
   ```bash
   git switch -c feature/contact-form
   # Old way: git checkout -b feature/contact-form
   ```

**Validation**:
```bash
# List all branches
git branch
# Should see: master, feature/add-projects, feature/contact-form

# Check current branch
git branch --show-current
```

**Learning Points**:
- ✅ Branches let you work on features independently
- ✅ `git branch` = list or create branches
- ✅ `git switch` = change branches (newer command)
- ✅ `git checkout` = older way to switch branches

---

### Exercise 8: Working on a Branch

**Objective**: Make commits on a feature branch

**Scenario**: Build a projects section on a feature branch.

**Tasks**:
1. Ensure you're on feature/add-projects:
   ```bash
   git switch feature/add-projects
   ```

2. Create a new file `projects.html`:
   ```html
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
   ```

3. Add and commit:
   ```bash
   git add projects.html
   git commit -m "Add projects page"
   ```

4. Modify index.html to link to projects:
   ```html
   <nav>
     <a href="projects.html">Projects</a>
   </nav>
   ```

5. Commit the change:
   ```bash
   git add index.html
   git commit -m "Add navigation link to projects"
   ```

6. View branch history:
   ```bash
   git log --oneline
   ```

**Validation**:
```bash
# Should show 2 new commits on this branch
git log --oneline -n 2

# Switch back to master
git switch master

# File shouldn't exist on master
ls projects.html  # Should fail or not show

# Switch back to feature branch
git switch feature/add-projects
ls projects.html  # Should exist!
```

**Learning Points**:
- ✅ Each branch has its own commits and file state
- ✅ Files exist on branch where they're committed
- ✅ Switching branches changes working directory
- ✅ Branches are independent until merged

---

### Exercise 9: Merging a Feature Branch

**Objective**: Merge feature branch into master

**Scenario**: Projects section is done - merge it to master.

**Tasks**:
1. Switch to master (target branch):
   ```bash
   git switch master
   ```

2. View history before merge:
   ```bash
   git log --oneline --graph --all
   ```

3. Merge the feature branch:
   ```bash
   git merge feature/add-projects
   ```

4. Git performs "fast-forward" merge (if no conflicts)

5. View updated history:
   ```bash
   git log --oneline --graph
   ```

6. Verify files are now on master:
   ```bash
   ls projects.html  # Should exist now
   ```

7. Optionally delete the feature branch:
   ```bash
   git branch -d feature/add-projects
   ```

**Validation**:
```bash
# History should include commits from feature branch
git log --oneline

# projects.html should exist
cat projects.html

# Feature branch deleted
git branch  # Shouldn't show feature/add-projects
```

**Learning Points**:
- ✅ Always merge FROM feature branch TO master
- ✅ Switch to target branch (master) first, then merge
- ✅ Fast-forward = no merge commit (linear history)
- ✅ Delete feature branches after merging (cleanup)

---

### Exercise 10: Merge with Merge Commit

**Objective**: Create a merge commit (no fast-forward)

**Scenario**: Want to preserve branch history in commits.

**Tasks**:
1. Create and switch to new branch:
   ```bash
   git switch -c feature/footer
   ```

2. Modify index.html - add footer:
   ```html
   <footer>
     <p>&copy; 2026 Your Name. All rights reserved.</p>
   </footer>
   ```

3. Commit the change:
   ```bash
   git add index.html
   git commit -m "Add footer section"
   ```

4. Switch back to master:
   ```bash
   git switch master
   ```

5. Merge with no fast-forward:
   ```bash
   git merge --no-ff feature/footer -m "Merge footer feature"
   ```

6. View the merge commit:
   ```bash
   git log --oneline --graph
   ```
   Notice the merge commit and branch structure

**Validation**:
```bash
# Should show merge commit
git log --oneline -n 1
# Should include "Merge" in message

# Graph should show branch and merge
git log --oneline --graph -n 5
```

**Learning Points**:
- ✅ `--no-ff` creates merge commit (preserves history)
- ✅ Merge commits have two parents
- ✅ Useful for tracking when features were merged
- ✅ Some teams prefer this over fast-forward

---

## 🟣 Remote Basics (Exercises 11-13)

### Exercise 11: Understanding Remotes

**Objective**: View and understand remote connections

**Scenario**: This repo is cloned from GitHub - explore the connection.

**Tasks**:
1. View remote repositories:
   ```bash
   git remote
   # Should show: origin
   ```

2. View remote URLs:
   ```bash
   git remote -v
   # Shows fetch and push URLs
   ```

3. View more detail:
   ```bash
   git remote show origin
   ```

4. View remote branches:
   ```bash
   git branch -r
   # Shows remote branches like origin/master
   ```

5. View all branches (local + remote):
   ```bash
   git branch -a
   ```

**Validation**:
```bash
# Should have an origin remote
git remote -v | grep origin

# Should show remote tracking branches
git branch -r
```

**Learning Points**:
- ✅ `origin` is default name for cloned remote
- ✅ Remote branches prefixed with `origin/`
- ✅ Local and remote branches are separate
- ✅ `git remote` manages remote connections

---

### Exercise 12: Fetching and Pulling

**Objective**: Understand difference between fetch and pull

**Scenario**: Simulate getting updates from remote repository.

**Tasks**:
1. Check current status with remote:
   ```bash
   git status
   # Should say "Your branch is up to date with 'origin/master'"
   ```

2. View what fetch would do (dry run):
   ```bash
   git fetch --dry-run
   ```

3. Fetch from remote:
   ```bash
   git fetch origin
   ```

4. View remote tracking branch:
   ```bash
   git log origin/master --oneline -n 5
   ```

5. Compare local with remote:
   ```bash
   git log master..origin/master  # Commits on remote not in local
   git log origin/master..master  # Commits on local not in remote
   ```

6. Understand pull = fetch + merge:
   ```bash
   # This is what pull does:
   # git fetch origin
   # git merge origin/master
   
   # Do it in one command:
   git pull origin master
   ```

**Validation**:
```bash
# Should be up to date
git status

# Local and remote should match
git log HEAD --oneline -n 1
git log origin/master --oneline -n 1
# Should show same commit
```

**Learning Points**:
- ✅ `git fetch` = download commits (doesn't change working dir)
- ✅ `git pull` = fetch + merge (updates working directory)
- ✅ `fetch` is safer - lets you review before merging
- ✅ `pull` is convenient but can surprise you

---

### Exercise 13: Pushing Changes

**Objective**: Push local commits to remote repository

**Scenario**: You've made local commits - share them with the remote.

**Tasks**:
1. Make a change locally:
   ```bash
   # Edit index.html - add copyright year
   git add index.html
   git commit -m "Update copyright year to 2026"
   ```

2. Check status:
   ```bash
   git status
   # Should say "Your branch is ahead of 'origin/master' by 1 commit"
   ```

3. Push to remote:
   ```bash
   git push origin master
   ```

4. Verify push succeeded:
   ```bash
   git status
   # Should say "Your branch is up to date with 'origin/master'"
   ```

5. View remote log:
   ```bash
   git log origin/master --oneline -n 3
   ```

**Validation**:
```bash
# Should show pushed commit on remote
git log origin/master --oneline -n 1

# Status should be up to date
git status
```

**Learning Points**:
- ✅ `git push` uploads local commits to remote
- ✅ Push requires write permissions
- ✅ Can't push if remote has commits you don't have (pull first)
- ✅ `origin master` = remote name and branch name

---

## 🔴 Best Practices (Exercises 14-15)

### Exercise 14: Using .gitignore

**Objective**: Prevent unwanted files from being tracked

**Scenario**: Node modules, logs, and personal notes shouldn't be in Git.

**Tasks**:
1. Create some files that shouldn't be tracked:
   ```bash
   mkdir node_modules
   touch node_modules/package.txt
   touch debug.log
   touch personal-notes.txt
   ```

2. Check status:
   ```bash
   git status
   # All files shown as untracked
   ```

3. Create `.gitignore` file:
   ```bash
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
   EOF
   ```

4. Check status again:
   ```bash
   git status
   # Should only show .gitignore, not the ignored files
   ```

5. Commit the .gitignore:
   ```bash
   git add .gitignore
   git commit -m "Add gitignore for dependencies and logs"
   ```

6. Verify ignored files stay ignored:
   ```bash
   git status  # Should be clean
   ```

**Validation**:
```bash
# Check what's ignored
git status --ignored

# Try to add ignored file (should warn)
git add debug.log
# Git should say it's ignored

# .gitignore should be tracked
git ls-files | grep .gitignore
```

**Learning Points**:
- ✅ `.gitignore` tells Git which files to ignore
- ✅ Patterns: `*.log` (wildcards), `folder/` (directories)
- ✅ Apply .gitignore before first commit
- ✅ .gitignore itself should be tracked

---

### Exercise 15: Writing Good Commit Messages

**Objective**: Practice writing clear, meaningful commit messages

**Scenario**: Make several commits with properly formatted messages.

**Tasks**:
1. Read commit message best practices:
   - First line: short summary (50 chars or less)
   - Blank line
   - Detailed explanation if needed
   - Use imperative mood: "Add feature" not "Added feature"
   - Explain WHY, not just WHAT

2. Make a good commit:
   ```bash
   # Edit style.css - improve responsiveness
   git add style.css
   git commit -m "Make header responsive on mobile devices"
   ```

3. Make a detailed commit:
   ```bash
   # Edit script.js - add form validation
   git add script.js
   git commit  # Opens editor
   ```

   Write in editor:
   ```
   Add form validation for contact form

   - Validate email format with regex
   - Require all fields before submission
   - Show error messages for invalid input
   - Improve user experience
   ```

4. View your commit history:
   ```bash
   git log --oneline -n 5
   ```

5. View full messages:
   ```bash
   git log -n 2
   ```

**Validation**:
```bash
# Check message format
git log --oneline -n 1
# First line should be concise

# View full message
git show HEAD
# Should have explanation if needed
```

**Learning Points**:
- ✅ Good messages help future you and teammates
- ✅ Summary line: imperative mood, under 50 chars
- ✅ Detailed body: WHY you made changes
- ✅ Group related changes in one commit

---

## 🎉 Completion

Congratulations! You've completed all 15 exercises!

### What You've Learned:
- ✅ Initialize and configure Git
- ✅ Stage and commit changes
- ✅ View history and diffs
- ✅ Undo changes safely
- ✅ Create and merge branches
- ✅ Work with remote repositories
- ✅ Use .gitignore effectively
- ✅ Write good commit messages

### Next Steps:
1. Review SOLUTIONS.md for alternative approaches
2. Take the quiz in `../git-mastery-quiz/`
3. Move to intermediate topics:
   - Repository 2: Merge Conflicts
   - Repository 5: Remote Workflows
   - Repository 7: Branching Strategies

### Keep Practicing!
Git mastery comes with practice. Try these challenges:
- Use Git for a personal project
- Practice branching workflows
- Contribute to open source
- Help others learn Git

**Happy Gitting! 🚀**
