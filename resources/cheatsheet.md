# GitHub & Git Cheatsheet 📋

A comprehensive quick reference guide for all the essential Git and GitHub commands, workflows, and best practices you've learned during your 21-day journey.

---

## 🚀 Quick Start Commands

### Initial Setup
```bash
# Configure Git (first time setup)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main

# Check configuration
git config --list
git config user.name
git config user.email
```

### Repository Initialization
```bash
# Initialize new repository
git init
git init <directory-name>

# Clone existing repository
git clone <repository-url>
git clone <repository-url> <directory-name>

# Clone specific branch
git clone -b <branch-name> <repository-url>
```

---

## 📁 Basic Git Operations

### File Operations
```bash
# Check repository status
git status
git status -s  # Short format

# Add files to staging area
git add <file-name>
git add .                    # Add all files
git add *.js                 # Add all JavaScript files
git add -A                   # Add all files including deletions

# Remove files
git rm <file-name>           # Remove file and stage deletion
git rm --cached <file-name>  # Remove from staging, keep in working directory

# Move/rename files
git mv <old-name> <new-name>
```

### Committing Changes
```bash
# Commit staged changes
git commit -m "Commit message"
git commit -am "Add and commit message"  # Add and commit in one step

# Amend last commit
git commit --amend -m "New commit message"
git commit --amend --no-edit  # Keep same message

# Interactive commit
git add -p  # Add parts of files interactively
```

### Viewing History
```bash
# View commit history
git log
git log --oneline            # Compact view
git log --graph              # Show branch graph
git log --stat               # Show file statistics
git log -p                   # Show patch/diff
git log -n 5                 # Show last 5 commits

# View specific file history
git log <file-name>
git log --follow <file-name>  # Follow renames

# Show differences
git diff                     # Working directory vs staging
git diff --staged            # Staging vs last commit
git diff HEAD~1              # Current vs previous commit
git diff <commit1> <commit2> # Between two commits
```

---

## 🌿 Branching & Merging

### Branch Operations
```bash
# List branches
git branch                   # Local branches
git branch -r                # Remote branches
git branch -a                # All branches

# Create and switch branches
git branch <branch-name>     # Create branch
git checkout <branch-name>   # Switch to branch
git checkout -b <branch-name> # Create and switch
git switch <branch-name>     # Modern way to switch
git switch -c <branch-name>  # Create and switch (modern)

# Delete branches
git branch -d <branch-name>  # Delete merged branch
git branch -D <branch-name>  # Force delete branch
git push origin --delete <branch-name>  # Delete remote branch
```

### Merging
```bash
# Merge branches
git merge <branch-name>      # Merge into current branch
git merge --no-ff <branch-name>  # Force merge commit
git merge --squash <branch-name> # Squash merge

# Abort merge
git merge --abort
```

### Rebasing
```bash
# Rebase current branch
git rebase <base-branch>
git rebase -i <base-branch>  # Interactive rebase
git rebase -i HEAD~3         # Interactive rebase last 3 commits

# Continue/abort rebase
git rebase --continue
git rebase --abort
git rebase --skip
```

---

## 🌐 Remote Operations

### Remote Management
```bash
# List remotes
git remote -v

# Add remote
git remote add <name> <url>
git remote add origin <repository-url>

# Change remote URL
git remote set-url origin <new-url>

# Remove remote
git remote remove <name>
```

### Fetching & Pulling
```bash
# Fetch from remote
git fetch                    # Fetch all remotes
git fetch origin             # Fetch specific remote
git fetch origin <branch>    # Fetch specific branch

# Pull changes
git pull                     # Fetch and merge
git pull origin <branch>     # Pull specific branch
git pull --rebase            # Fetch and rebase
```

### Pushing
```bash
# Push to remote
git push                     # Push current branch
git push origin <branch>     # Push specific branch
git push -u origin <branch>  # Push and set upstream
git push --force-with-lease  # Safe force push
git push --tags              # Push tags
```

---

## 🏷️ Tags & Releases

### Tag Operations
```bash
# List tags
git tag
git tag -l "v1.*"           # List tags matching pattern

# Create tags
git tag <tag-name>          # Lightweight tag
git tag -a <tag-name> -m "Tag message"  # Annotated tag
git tag -a <tag-name> <commit-hash>     # Tag specific commit

# Push tags
git push origin <tag-name>
git push origin --tags      # Push all tags

# Delete tags
git tag -d <tag-name>       # Delete local tag
git push origin --delete <tag-name>  # Delete remote tag
```

---

## 🔄 Undoing Changes

### Working Directory
```bash
# Discard changes in working directory
git checkout -- <file-name>
git restore <file-name>     # Modern way

# Discard all changes
git checkout -- .
git restore .
```

### Staging Area
```bash
# Unstage files
git reset HEAD <file-name>
git restore --staged <file-name>  # Modern way

# Unstage all files
git reset HEAD
git restore --staged .
```

### Commits
```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Revert commit (create new commit)
git revert <commit-hash>
git revert HEAD             # Revert last commit
```

### Advanced Undo
```bash
# Find lost commits
git reflog

# Reset to specific commit
git reset --hard <commit-hash>

# Cherry-pick specific commit
git cherry-pick <commit-hash>
```

---

## 🔍 Searching & Finding

### Search in Code
```bash
# Search in files
git grep "search-term"
git grep -n "search-term"   # Show line numbers
git grep -i "search-term"   # Case insensitive

# Search in commit messages
git log --grep="search-term"

# Search in commit content
git log -S "search-term"    # Search for code changes
git log -G "regex-pattern"  # Search with regex
```

### Finding Changes
```bash
# Find when line was changed
git blame <file-name>
git blame -L 10,20 <file-name>  # Specific lines

# Find commits that changed file
git log --follow <file-name>

# Show what changed in commit
git show <commit-hash>
git show <commit-hash>:<file-name>  # Specific file
```

---

## 🛠️ Advanced Git Operations

### Stashing
```bash
# Stash changes
git stash
git stash push -m "Stash message"
git stash -u                # Include untracked files

# List stashes
git stash list

# Apply stashes
git stash apply             # Apply latest stash
git stash apply stash@{2}   # Apply specific stash
git stash pop               # Apply and remove stash

# Drop stashes
git stash drop stash@{2}
git stash clear             # Remove all stashes
```

### Submodules
```bash
# Add submodule
git submodule add <repository-url> <path>

# Initialize submodules
git submodule init
git submodule update

# Clone with submodules
git clone --recursive <repository-url>

# Update submodules
git submodule update --remote
```

### Worktrees
```bash
# Create worktree
git worktree add <path> <branch>

# List worktrees
git worktree list

# Remove worktree
git worktree remove <path>
```

---

## 🐙 GitHub-Specific Operations

### GitHub CLI (gh)
```bash
# Authentication
gh auth login

# Repository operations
gh repo create <name>
gh repo clone <owner/repo>
gh repo fork <owner/repo>
gh repo view <owner/repo>

# Issues
gh issue list
gh issue create --title "Title" --body "Description"
gh issue view <number>
gh issue close <number>

# Pull requests
gh pr list
gh pr create --title "Title" --body "Description"
gh pr view <number>
gh pr checkout <number>
gh pr merge <number>
gh pr review <number>
```

### SSH Setup
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Test SSH connection
ssh -T git@github.com
```

---

## 🔧 Configuration & Aliases

### Useful Git Aliases
```bash
# Set up common aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.amend "commit --amend --no-edit"
```

### Advanced Configuration
```bash
# Set default editor
git config --global core.editor "code --wait"

# Set merge tool
git config --global merge.tool vimdiff

# Auto-correct typos
git config --global help.autocorrect 1

# Colorful output
git config --global color.ui auto

# Line ending configuration
git config --global core.autocrlf input  # Mac/Linux
git config --global core.autocrlf true   # Windows
```

---

## 🚨 Emergency Commands

### When Things Go Wrong
```bash
# Abort current operation
git merge --abort
git rebase --abort
git cherry-pick --abort

# Recover lost work
git reflog                  # Find lost commits
git fsck --lost-found       # Find orphaned objects

# Force sync with remote
git fetch origin
git reset --hard origin/main

# Clean working directory
git clean -fd               # Remove untracked files and directories
git clean -fX               # Remove ignored files
```

### Conflict Resolution
```bash
# During merge conflicts
git status                  # See conflicted files
# Edit files to resolve conflicts
git add <resolved-file>
git commit                  # Complete merge

# Use merge tools
git mergetool
```

---

## 📊 Workflow Patterns

### Feature Branch Workflow
```bash
# 1. Create feature branch
git checkout -b feature/new-feature

# 2. Work and commit
git add .
git commit -m "Add new feature"

# 3. Push to remote
git push -u origin feature/new-feature

# 4. Create pull request (via GitHub)
gh pr create

# 5. After review, merge and cleanup
git checkout main
git pull origin main
git branch -d feature/new-feature
```

### Gitflow Workflow
```bash
# Start new feature
git checkout develop
git checkout -b feature/feature-name

# Finish feature
git checkout develop
git merge --no-ff feature/feature-name
git branch -d feature/feature-name

# Start release
git checkout develop
git checkout -b release/1.0.0

# Finish release
git checkout main
git merge --no-ff release/1.0.0
git tag -a v1.0.0
git checkout develop
git merge --no-ff release/1.0.0
```

### Hotfix Workflow
```bash
# Start hotfix
git checkout main
git checkout -b hotfix/critical-fix

# Finish hotfix
git checkout main
git merge --no-ff hotfix/critical-fix
git tag -a v1.0.1
git checkout develop
git merge --no-ff hotfix/critical-fix
```

---

## 📝 Commit Message Conventions

### Conventional Commits
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

**Examples:**
```
feat(auth): add OAuth2 authentication
fix(api): resolve null pointer exception
docs(readme): update installation instructions
style(css): improve button styling
refactor(utils): extract common functions
test(auth): add unit tests for login
chore(deps): update dependencies
```

---

## 🎯 Best Practices Quick Reference

### Commit Best Practices
- ✅ Make small, focused commits
- ✅ Write clear, descriptive commit messages
- ✅ Commit related changes together
- ✅ Test before committing
- ❌ Don't commit broken code
- ❌ Don't commit sensitive information

### Branch Best Practices
- ✅ Use descriptive branch names
- ✅ Keep branches short-lived
- ✅ Regularly sync with main branch
- ✅ Delete merged branches
- ❌ Don't work directly on main
- ❌ Don't let branches become stale

### Collaboration Best Practices
- ✅ Pull before pushing
- ✅ Review code thoroughly
- ✅ Communicate changes clearly
- ✅ Respect project conventions
- ❌ Don't force push to shared branches
- ❌ Don't ignore merge conflicts

---

## 🔗 Quick Links

- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)
- [GitHub CLI Manual](https://cli.github.com/manual/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)

---

## 💡 Pro Tips

1. **Use `git status` frequently** - Always know what's happening in your repository
2. **Commit early and often** - Small commits are easier to understand and revert
3. **Write meaningful commit messages** - Your future self will thank you
4. **Use branches for everything** - Keep main branch stable
5. **Learn keyboard shortcuts** - Speed up your workflow
6. **Set up aliases** - Make common commands shorter
7. **Use `.gitignore`** - Don't commit unnecessary files
8. **Backup important work** - Push to remote regularly

---

*This cheatsheet covers the essential commands and workflows from your 21-day GitHub mastery journey. Keep it handy for quick reference!* 📚