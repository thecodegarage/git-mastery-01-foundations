# Repository 1: Git Basics & Daily Workflow 🌱

**Master the fundamentals and daily Git commands with confidence**

## 🎯 Learning Objectives

By completing this repository, you will:

- ✅ Understand what Git is and why it's essential
- ✅ Configure Git for your identity
- ✅ Initialize and clone repositories
- ✅ Track changes with add and commit
- ✅ Write meaningful commit messages
- ✅ View and understand commit history
- ✅ Create and switch between branches
- ✅ Perform basic merges (without conflicts)
- ✅ Work with remote repositories (push, pull, fetch)
- ✅ Undo changes safely
- ✅ Use .gitignore effectively
- ✅ Follow best practices for daily workflow

## 📊 Difficulty Level

🟢 **Beginner** - No Git experience required!

**Prerequisites:**
- Computer with terminal/command line access
- Text editor (VS Code recommended)
- Willingness to learn!

**Estimated Time:** 4-6 hours

## 🏗️ Repository Setup

This repository simulates a **Personal Portfolio Website** project where you'll practice all the Git basics.

### What's Included

- **15 Progressive Exercises** - From first commit to remote collaboration
- **Real project structure** - HTML, CSS, JavaScript files
- **Step-by-step guidance** - Clear instructions for each command
- **Validation checks** - Verify you did it correctly
- **Common mistakes** - Learn from typical beginner errors

## 📚 What's Included

- **EXERCISES.md** - 15 hands-on exercises for beginners
- **GIT-CHEATSHEET.md** - Essential commands reference
- **SOLUTIONS.md** - Detailed solutions
- **TROUBLESHOOTING.md** - Common beginner issues
- **GLOSSARY.md** - Git terminology explained

## 🚀 Getting Started

**Note:** This repository is ready to use immediately! Unlike other practice repositories, you'll practice Git commands directly on the included files (index.html, style.css, script.js). No setup script needed.

### 1. Verify Git Installation

```bash
# Check if Git is installed
git --version

# Should show something like: git version 2.40.0
# If not installed: https://git-scm.com/downloads
```

### 2. First-Time Setup

```bash
# Configure your identity (required!)
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Verify configuration
git config --list
```

### 3. Understand This Repository

You're currently in a portfolio website project with:

```
portfolio/
├── index.html          # Homepage
├── about.html          # About page
├── style.css           # Styling
├── script.js           # JavaScript
├── images/             # Image assets
└── projects/           # Project showcase
```

### 4. Start with Exercise 1

Open EXERCISES.md and begin!

```bash
code EXERCISES.md
# Or: cat EXERCISES.md
```

## 💡 Key Concepts

### What is Git?

**Git** is a version control system that:
- Tracks changes to your files over time
- Lets you revert to previous versions
- Enables collaboration with others
- Creates a complete history of your project

Think of it as "Track Changes" for code, but much more powerful!

### Basic Workflow

The daily Git workflow has 4 steps:

```
1. WORK     →  2. STAGE    →  3. COMMIT   →  4. SHARE
   ↓              ↓              ↓              ↓
Edit files    git add .    git commit    git push
```

### The Three States

Files in Git can be in three states:

1. **Modified** - Changed but not staged
2. **Staged** - Marked for next commit
3. **Committed** - Safely stored in Git history

```bash
# Check which state files are in
git status
```

### Branches

**Branches** let you work on features without affecting the main code:

```
main    ●──●──●──●
              ↘
feature        ●──●
```

You can create a branch, make changes, then merge back to main!

## 🎓 Learning Strategy

### Recommended Approach

1. **Read each exercise fully** before starting
2. **Type commands yourself** - Don't copy/paste
3. **Use `git status` constantly** - It's your friend!
4. **Make mistakes** - Best way to learn
5. **Experiment** - Try variations of commands
6. **Ask questions** - Check TROUBLESHOOTING.md

### If You Get Stuck

1. **Read Git's output** - It often tells you what to do
2. **Check `git status`** - Shows current state
3. **Look at TROUBLESHOOTING.md** - Common issues covered
4. **Review SOLUTIONS.md** - But try first!
5. **Start over if needed** - It's practice!

## 📈 Progress Tracking

Track your exercise completion:

### Understanding Git
- [ ] Exercise 1: Your First Repository
- [ ] Exercise 2: Making Commits
- [ ] Exercise 3: Viewing History

### Working with Changes
- [ ] Exercise 4: Staging Changes
- [ ] Exercise 5: Undoing Changes
- [ ] Exercise 6: Using .gitignore

### Branching Basics
- [ ] Exercise 7: Creating Branches
- [ ] Exercise 8: Switching Branches
- [ ] Exercise 9: Merging Branches

### Remote Repositories
- [ ] Exercise 10: Understanding Remotes
- [ ] Exercise 11: Pushing Changes
- [ ] Exercise 12: Pulling Changes
- [ ] Exercise 13: Cloning Repositories

### Daily Workflow
- [ ] Exercise 14: Full Workflow Practice
- [ ] Exercise 15: Best Practices

## ✅ Completion Criteria

You've mastered Git basics when you can:

1. ✅ Initialize a new Git repository
2. ✅ Make commits with good messages
3. ✅ View and understand commit history
4. ✅ Create and switch between branches
5. ✅ Merge branches successfully
6. ✅ Push and pull from remote repositories
7. ✅ Undo mistakes safely
8. ✅ Explain Git workflow to someone else
9. ✅ Score 80%+ on the Git Basics quiz

## 🎯 Next Steps

After completing this repository:

1. **Take the quiz** - Test your foundational knowledge
2. **Score 80%+?** - Move to next repository
3. **Below 80%?** - Retry exercises, retake quiz
4. **Want more practice?** - Re-clone and try again!

### Recommended Next Topics

Based on your experience level:

**If still building confidence:**
- [Branching Strategies](https://github.com/TheCodeGarage/git-practice-branching-strategies)

**If comfortable with basics:**
- [Merge Conflicts](https://github.com/TheCodeGarage/git-practice-merge-conflicts)
- [Remote Workflows](https://github.com/TheCodeGarage/git-practice-remote-workflows)

## 🛠️ Reset Instructions

### Start an Exercise Over

```bash
# Reset to last commit
git reset --hard HEAD

# Clean untracked files
git clean -fd
```

### Reset Entire Repository

```bash
# Delete and re-clone
cd ..
rm -rf 00-git-basics
git clone https://github.com/TheCodeGarage/git-practice-foundations
```

## 📚 Additional Resources

- [Pro Git Book](https://git-scm.com/book) - Free, comprehensive
- [Git Documentation](https://git-scm.com/doc) - Official docs
- [GitHub Git Guides](https://github.com/git-guides) - Quick guides
- Use `git help <command>` in terminal

## 🌟 Important Tips for Beginners

### Do's ✅

- **Use `git status` constantly** - Shows what's happening
- **Read Git's messages** - They're helpful!
- **Commit often** - Small commits are better than big ones
- **Write clear commit messages** - Future you will thank you
- **Practice regularly** - 15 minutes daily beats 2 hours weekly

### Don'ts ❌

- **Don't panic** - Git is forgiving, most things can be undone
- **Don't skip `git status`** - It prevents mistakes
- **Don't commit sensitive data** - Use .gitignore!
- **Don't make huge commits** - Keep them focused
- **Don't fear mistakes** - They're how you learn

## 🎓 Git Vocabulary

Essential terms you'll encounter:

- **Repository (repo)** - Project folder tracked by Git
- **Commit** - Snapshot of your project at a point in time
- **Branch** - Independent line of development
- **HEAD** - Pointer to your current location
- **Origin** - Default name for remote repository
- **Clone** - Copy a repository to your computer
- **Push** - Send commits to remote repository
- **Pull** - Get commits from remote repository
- **Merge** - Combine changes from different branches

See GLOSSARY.md for complete definitions!

---

**Ready to start?** Open [EXERCISES.md](EXERCISES.md) and begin with Exercise 1!

**New to command line?** That's okay! The exercises will guide you step-by-step.

**Questions?** Check [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common beginner issues.

---

🌱 **Remember:** Every Git expert was once a beginner. Take your time, make mistakes, and enjoy the learning process!
