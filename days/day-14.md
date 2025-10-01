# Day 14: Advanced Git Workflows ⚡

## 📋 Overview

Master the sophisticated Git workflows used by large-scale open source projects. Today you'll learn advanced branching strategies, release management, automated workflows, and Git techniques that enable teams to collaborate efficiently on complex projects. These skills are essential for contributing to major projects and leading your own.

## 🎯 Learning Objectives

- Master advanced Git branching strategies (Git Flow, GitHub Flow, etc.)
- Learn sophisticated merge and rebase techniques
- Understand release management and versioning strategies
- Practice advanced Git commands for complex scenarios
- Implement automated workflows with Git hooks and CI/CD
- Develop skills for managing large repositories and histories

## 📚 Prerequisites

- Solid understanding of basic Git commands and concepts
- Experience with branching, merging, and pull requests
- Familiarity with collaborative development workflows
- Understanding of software development lifecycle

## ⏱️ Estimated Time

Approximately 180-220 minutes

## 🧭 Difficulty Level

🔴 **Hard** - Advanced technical skills and workflow management

---

## 📖 Theory Section

### Git Workflow Strategies

**Centralized Workflow**:
- Single main branch for all development
- Simple but limited scalability
- Best for small teams and simple projects
- Minimal branching overhead

**Feature Branch Workflow**:
- Separate branches for each feature
- Merge back to main when complete
- Good balance of simplicity and isolation
- Supports code review and testing

**Git Flow**:
- Structured branching model with specific purposes
- Main, develop, feature, release, and hotfix branches
- Formal release management process
- Best for projects with scheduled releases

**GitHub Flow**:
- Simplified flow with main branch and feature branches
- Continuous deployment friendly
- Fast iteration and deployment cycles
- Popular for web applications and SaaS

**GitLab Flow**:
- Combines Git Flow and GitHub Flow concepts
- Environment-specific branches (staging, production)
- Upstream-first development approach
- Good for complex deployment scenarios

### Advanced Git Concepts

**Merge vs. Rebase**:
- **Merge**: Preserves history, creates merge commits
- **Rebase**: Rewrites history, creates linear timeline
- **Interactive Rebase**: Allows editing commit history
- **Merge Strategies**: Different algorithms for combining changes

**Git Hooks**:
- Scripts that run at specific Git events
- Client-side and server-side hooks
- Automation for testing, formatting, and validation
- Integration with CI/CD systems

**Advanced References**:
- **HEAD**: Current branch pointer
- **Reflog**: History of reference changes
- **Tags**: Named references to specific commits
- **Remote Tracking**: Relationship between local and remote branches

---

## 💻 Hands-On Practice

### Step 1: Master Git Flow Workflow

Learn the complete Git Flow branching strategy:

1. **Git Flow Setup and Initialization**:
   ```bash
   # Install git-flow (if not already installed)
   # macOS: brew install git-flow
   # Ubuntu: sudo apt-get install git-flow
   
   # Initialize git flow in your repository
   git flow init
   
   # This creates the branch structure:
   # - main (production releases)
   # - develop (integration branch)
   # - feature/* (new features)
   # - release/* (release preparation)
   # - hotfix/* (emergency fixes)
   ```

2. **Feature Development Workflow**:
   ```bash
   # Start a new feature
   git flow feature start user-authentication
   # This creates: feature/user-authentication branch from develop
   
   # Work on your feature
   echo "# User Authentication Module" > auth.md
   git add auth.md
   git commit -m "feat: add user authentication module"
   
   # Continue development
   echo "## Login functionality" >> auth.md
   git add auth.md
   git commit -m "feat: implement login functionality"
   
   # Finish the feature
   git flow feature finish user-authentication
   # This merges feature branch into develop and deletes feature branch
   ```

3. **Release Management Workflow**:
   ```bash
   # Start a release
   git flow release start 1.0.0
   # This creates: release/1.0.0 branch from develop
   
   # Prepare release (update version, changelog, etc.)
   echo "Version 1.0.0" > VERSION
   echo "# Changelog\n\n## v1.0.0\n- User authentication" > CHANGELOG.md
   git add VERSION CHANGELOG.md
   git commit -m "chore: prepare release 1.0.0"
   
   # Finish the release
   git flow release finish 1.0.0
   # This merges into main, tags the release, merges back to develop
   ```

4. **Hotfix Workflow**:
   ```bash
   # Start a hotfix from main
   git flow hotfix start security-patch
   
   # Fix the critical issue
   echo "Security patch applied" > security-fix.md
   git add security-fix.md
   git commit -m "fix: apply critical security patch"
   
   # Finish the hotfix
   git flow hotfix finish security-patch
   # This merges into main, tags, and merges back to develop
   ```

### Step 2: Master Advanced Rebase Techniques

Learn sophisticated history manipulation:

1. **Interactive Rebase for History Cleanup**:
   ```bash
   # Create a messy commit history to clean up
   git checkout -b feature/cleanup-demo
   
   echo "Initial work" > demo.txt
   git add demo.txt && git commit -m "WIP: initial work"
   
   echo "More work" >> demo.txt
   git add demo.txt && git commit -m "fix typo"
   
   echo "Final work" >> demo.txt
   git add demo.txt && git commit -m "WIP: more changes"
   
   echo "Documentation" > README.md
   git add README.md && git commit -m "add docs"
   
   # Interactive rebase to clean up last 4 commits
   git rebase -i HEAD~4
   
   # In the editor, you can:
   # pick = keep commit as-is
   # reword = change commit message
   # edit = stop to amend commit
   # squash = combine with previous commit
   # fixup = like squash but discard commit message
   # drop = remove commit entirely
   ```

2. **Advanced Rebase Operations**:
   ```bash
   # Rebase with conflict resolution
   git checkout develop
   echo "Conflicting change" > demo.txt
   git add demo.txt && git commit -m "conflicting change on develop"
   
   git checkout feature/cleanup-demo
   git rebase develop
   # Resolve conflicts, then:
   git add demo.txt
   git rebase --continue
   
   # Rebase onto a different base
   git rebase --onto main develop feature/cleanup-demo
   
   # Abort rebase if things go wrong
   git rebase --abort
   ```

3. **Commit Splitting and Editing**:
   ```bash
   # Create a commit that should be split
   echo "Feature A code" > feature-a.txt
   echo "Feature B code" > feature-b.txt
   git add feature-a.txt feature-b.txt
   git commit -m "implement features A and B"
   
   # Interactive rebase to split the commit
   git rebase -i HEAD~1
   # Mark the commit as 'edit'
   
   # When rebase stops, reset the commit
   git reset HEAD~1
   
   # Create separate commits
   git add feature-a.txt
   git commit -m "implement feature A"
   
   git add feature-b.txt
   git commit -m "implement feature B"
   
   # Continue the rebase
   git rebase --continue
   ```

### Step 3: Implement Advanced Merge Strategies

Master different merge approaches:

1. **Merge Strategy Options**:
   ```bash
   # Create branches to demonstrate merge strategies
   git checkout -b feature/merge-demo
   echo "Feature work" > feature.txt
   git add feature.txt && git commit -m "add feature work"
   
   git checkout main
   echo "Main work" > main.txt
   git add main.txt && git commit -m "add main work"
   
   # Default merge (creates merge commit)
   git merge feature/merge-demo
   
   # Fast-forward merge (when possible)
   git checkout -b feature/fast-forward
   echo "Fast forward work" > ff.txt
   git add ff.txt && git commit -m "fast forward work"
   git checkout main
   git merge --ff-only feature/fast-forward
   
   # Squash merge (combines all commits into one)
   git checkout -b feature/squash-demo
   echo "Work 1" > work1.txt && git add work1.txt && git commit -m "work 1"
   echo "Work 2" > work2.txt && git add work2.txt && git commit -m "work 2"
   git checkout main
   git merge --squash feature/squash-demo
   git commit -m "feat: implement squashed feature"
   ```

2. **Merge Conflict Resolution Strategies**:
   ```bash
   # Create conflicting changes
   git checkout -b feature/conflict-demo
   echo "Feature version" > conflict.txt
   git add conflict.txt && git commit -m "feature version"
   
   git checkout main
   echo "Main version" > conflict.txt
   git add conflict.txt && git commit -m "main version"
   
   # Attempt merge (will conflict)
   git merge feature/conflict-demo
   
   # View conflict with different tools
   git status
   git diff
   git mergetool  # If configured
   
   # Resolve conflict manually
   echo "Resolved version combining both" > conflict.txt
   git add conflict.txt
   git commit -m "resolve merge conflict"
   
   # Alternative: use merge strategies
   git merge -X ours feature/conflict-demo    # Prefer our changes
   git merge -X theirs feature/conflict-demo  # Prefer their changes
   ```

### Step 4: Advanced Git Commands and Techniques

Learn powerful Git commands for complex scenarios:

1. **Git Reflog and Recovery**:
   ```bash
   # View reflog to see all reference changes
   git reflog
   
   # Recover a deleted branch
   git branch feature/recovered <commit-hash-from-reflog>
   
   # Recover from a bad reset
   git reset --hard HEAD@{2}  # Go back 2 reflog entries
   
   # Find lost commits
   git fsck --lost-found
   git show <dangling-commit-hash>
   ```

2. **Advanced Git Search and Investigation**:
   ```bash
   # Search for specific content in history
   git log -S "function_name" --oneline
   git log -G "regex_pattern" --oneline
   
   # Find when a line was introduced
   git blame filename.txt
   git log -L 10,20:filename.txt  # History of lines 10-20
   
   # Binary search for bugs
   git bisect start
   git bisect bad HEAD
   git bisect good v1.0.0
   # Git will checkout commits for you to test
   git bisect good  # or git bisect bad
   git bisect reset  # When done
   ```

3. **Git Worktrees for Parallel Development**:
   ```bash
   # Create additional working directories
   git worktree add ../project-feature feature/new-feature
   git worktree add ../project-hotfix hotfix/urgent-fix
   
   # List all worktrees
   git worktree list
   
   # Work in different directories simultaneously
   cd ../project-feature
   # Make changes to feature
   
   cd ../project-hotfix
   # Make urgent fixes
   
   # Remove worktree when done
   git worktree remove ../project-feature
   ```

### Step 5: Implement Git Hooks and Automation

Set up automated workflows with Git hooks:

1. **Client-Side Hooks**:
   ```bash
   # Navigate to hooks directory
   cd .git/hooks
   
   # Create pre-commit hook for code formatting
   cat > pre-commit << 'EOF'
   #!/bin/sh
   # Run code formatter before commit
   
   echo "Running pre-commit checks..."
   
   # Check for JavaScript files and run prettier
   js_files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.js$')
   if [ -n "$js_files" ]; then
       echo "Formatting JavaScript files..."
       npx prettier --write $js_files
       git add $js_files
   fi
   
   # Run tests
   echo "Running tests..."
   npm test
   if [ $? -ne 0 ]; then
       echo "Tests failed. Commit aborted."
       exit 1
   fi
   
   echo "Pre-commit checks passed!"
   EOF
   
   chmod +x pre-commit
   ```

2. **Commit Message Validation Hook**:
   ```bash
   # Create commit-msg hook for conventional commits
   cat > commit-msg << 'EOF'
   #!/bin/sh
   # Validate commit message format
   
   commit_regex='^(feat|fix|docs|style|refactor|test|chore)(\(.+\))?: .{1,50}'
   
   if ! grep -qE "$commit_regex" "$1"; then
       echo "Invalid commit message format!"
       echo "Format: type(scope): description"
       echo "Types: feat, fix, docs, style, refactor, test, chore"
       echo "Example: feat(auth): add user login functionality"
       exit 1
   fi
   EOF
   
   chmod +x commit-msg
   ```

3. **Pre-Push Hook for Additional Validation**:
   ```bash
   # Create pre-push hook
   cat > pre-push << 'EOF'
   #!/bin/sh
   # Run additional checks before pushing
   
   protected_branch='main'
   current_branch=$(git symbolic-ref HEAD | sed -e 's,.*/\(.*\),\1,')
   
   if [ $protected_branch = $current_branch ]; then
       echo "Direct push to main branch is not allowed!"
       echo "Please create a pull request instead."
       exit 1
   fi
   
   # Run full test suite
   echo "Running full test suite before push..."
   npm run test:full
   if [ $? -ne 0 ]; then
       echo "Tests failed. Push aborted."
       exit 1
   fi
   
   echo "Pre-push checks passed!"
   EOF
   
   chmod +x pre-push
   ```

### Step 6: Advanced Repository Management

Learn techniques for managing large and complex repositories:

1. **Git Submodules for Component Management**:
   ```bash
   # Add a submodule
   git submodule add https://github.com/example/library.git lib/external-library
   
   # Initialize and update submodules
   git submodule init
   git submodule update
   
   # Clone repository with submodules
   git clone --recursive https://github.com/your/repository.git
   
   # Update submodules to latest
   git submodule update --remote
   
   # Work within a submodule
   cd lib/external-library
   git checkout -b feature/improvements
   # Make changes
   git commit -m "improve external library"
   git push origin feature/improvements
   
   # Update parent repository to use new submodule commit
   cd ../..
   git add lib/external-library
   git commit -m "update external library to latest version"
   ```

2. **Git LFS for Large Files**:
   ```bash
   # Install and initialize Git LFS
   git lfs install
   
   # Track large file types
   git lfs track "*.psd"
   git lfs track "*.zip"
   git lfs track "*.mp4"
   
   # Add .gitattributes file
   git add .gitattributes
   git commit -m "configure Git LFS for large files"
   
   # Add large files (they'll be stored in LFS)
   git add large-file.zip
   git commit -m "add large file via LFS"
   
   # View LFS files
   git lfs ls-files
   ```

3. **Repository Maintenance and Optimization**:
   ```bash
   # Clean up unnecessary files and optimize repository
   git gc --aggressive --prune=now
   
   # Verify repository integrity
   git fsck --full
   
   # Show repository size and statistics
   git count-objects -vH
   
   # Find large objects in history
   git rev-list --objects --all | \
   git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
   sed -n 's/^blob //p' | \
   sort --numeric-sort --key=2 | \
   tail -10
   
   # Remove sensitive data from history (use with caution!)
   git filter-branch --force --index-filter \
   'git rm --cached --ignore-unmatch sensitive-file.txt' \
   --prune-empty --tag-name-filter cat -- --all
   ```

### Step 7: CI/CD Integration with Git Workflows

Implement automated workflows with continuous integration:

1. **GitHub Actions Workflow**:
   ```yaml
   # .github/workflows/ci.yml
   name: Continuous Integration
   
   on:
     push:
       branches: [ main, develop ]
     pull_request:
       branches: [ main, develop ]
   
   jobs:
     test:
       runs-on: ubuntu-latest
       
       strategy:
         matrix:
           node-version: [14.x, 16.x, 18.x]
       
       steps:
       - uses: actions/checkout@v3
       
       - name: Use Node.js ${{ matrix.node-version }}
         uses: actions/setup-node@v3
         with:
           node-version: ${{ matrix.node-version }}
           cache: 'npm'
       
       - run: npm ci
       - run: npm run build --if-present
       - run: npm test
       - run: npm run lint
       
       - name: Upload coverage reports
         uses: codecov/codecov-action@v3
         if: matrix.node-version == '16.x'
   
     release:
       needs: test
       runs-on: ubuntu-latest
       if: github.ref == 'refs/heads/main'
       
       steps:
       - uses: actions/checkout@v3
         with:
           fetch-depth: 0
       
       - name: Semantic Release
         uses: cycjimmy/semantic-release-action@v3
         env:
           GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
           NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
   ```

2. **Automated Release Workflow**:
   ```yaml
   # .github/workflows/release.yml
   name: Release
   
   on:
     push:
       tags:
         - 'v*'
   
   jobs:
     release:
       runs-on: ubuntu-latest
       
       steps:
       - uses: actions/checkout@v3
       
       - name: Create Release
         uses: actions/create-release@v1
         env:
           GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
         with:
           tag_name: ${{ github.ref }}
           release_name: Release ${{ github.ref }}
           body: |
             Changes in this Release
             - Feature 1
             - Feature 2
             - Bug fixes
           draft: false
           prerelease: false
   ```

---

## 🎯 Today's Challenge

### Main Challenge: Implement a Complete Advanced Workflow

**Objective**: Set up and demonstrate a sophisticated Git workflow for a real project

**Success Criteria**:
- ✅ Implement a complete branching strategy (Git Flow or custom)
- ✅ Set up automated Git hooks for quality control
- ✅ Configure CI/CD pipeline with Git integration
- ✅ Demonstrate advanced Git techniques (rebase, merge strategies)
- ✅ Handle complex scenarios (conflicts, recovery, large files)
- ✅ Document the workflow for team adoption

**Workflow Implementation Options** (Choose One):

1. **Enterprise Git Flow Setup**:
   - Implement full Git Flow with all branch types
   - Set up automated testing and deployment pipelines
   - Create comprehensive documentation and training materials
   - Handle complex merge scenarios and conflict resolution

2. **Continuous Deployment Workflow**:
   - Implement GitHub Flow with automated deployment
   - Set up feature flags and progressive rollouts
   - Create automated testing and quality gates
   - Implement rollback and recovery procedures

3. **Open Source Project Workflow**:
   - Design workflow for external contributors
   - Set up automated code review and testing
   - Implement release management and versioning
   - Create contributor onboarding and guidelines

4. **Monorepo Management Workflow**:
   - Set up workflow for large, multi-component repository
   - Implement selective testing and deployment
   - Manage dependencies and cross-component changes
   - Set up workspace and build optimization

**Bonus Challenges**:
- 🌟 Create custom Git commands or aliases for your workflow
- 🌟 Implement advanced Git hooks with external tool integration
- 🌟 Set up Git LFS and submodule management
- 🌟 Create automated workflow documentation and training materials

---

## 📝 Git Workflow Comparison

| Workflow | Complexity | Release Frequency | Team Size | Best For |
|----------|------------|-------------------|-----------|----------|
| **Centralized** | Low | Any | Small | Simple projects |
| **Feature Branch** | Medium | Medium | Medium | Most projects |
| **Git Flow** | High | Scheduled | Large | Enterprise software |
| **GitHub Flow** | Low | Continuous | Any | Web applications |
| **GitLab Flow** | Medium | Continuous | Medium-Large | Complex deployments |

---

## 🔍 Advanced Git Commands Reference

| Command | Purpose | Example |
|---------|---------|---------|
| `git reflog` | View reference history | `git reflog --oneline` |
| `git bisect` | Binary search for bugs | `git bisect start HEAD v1.0` |
| `git worktree` | Multiple working directories | `git worktree add ../feature feature-branch` |
| `git filter-branch` | Rewrite history | `git filter-branch --tree-filter 'rm -f passwords.txt'` |
| `git rev-list` | List commits | `git rev-list --count HEAD` |
| `git show-branch` | Show branch relationships | `git show-branch --all` |
| `git cherry-pick` | Apply specific commits | `git cherry-pick abc123..def456` |
| `git revert` | Safely undo commits | `git revert --no-commit HEAD~3..HEAD` |

---

## 💡 Pro Tips

1. **Choose the Right Workflow**: Match your workflow to your team size, release frequency, and project complexity.

2. **Automate Quality Gates**: Use hooks and CI/CD to enforce standards automatically.

3. **Keep History Clean**: Use interactive rebase to create clear, logical commit history.

4. **Plan for Recovery**: Always know how to undo or recover from Git operations.

5. **Document Your Workflow**: Create clear guidelines for your team's Git practices.

6. **Practice Complex Scenarios**: Regularly practice conflict resolution and recovery procedures.

7. **Monitor Repository Health**: Keep an eye on repository size, performance, and integrity.

---

## 📚 Additional Resources

- [Pro Git Book](https://git-scm.com/book)
- [Git Flow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Git Hooks Documentation](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks)
- [Semantic Versioning](https://semver.org/)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

## ✅ Checklist

- [ ] Mastered advanced branching strategies (Git Flow, GitHub Flow)
- [ ] Implemented sophisticated merge and rebase techniques
- [ ] Set up automated Git hooks for quality control
- [ ] Configured CI/CD integration with Git workflows
- [ ] Practiced advanced Git commands and recovery techniques
- [ ] Managed large repositories with submodules and LFS
- [ ] Created comprehensive workflow documentation
- [ ] Handled complex scenarios and conflict resolution
- [ ] Optimized repository performance and maintenance
- [ ] Trained others on advanced Git techniques

---

## 🎉 Reflection

Reflect on your advanced Git mastery:

1. **Which Git workflows feel most natural to you?**
   - What matches your development style and project needs?
   - Which workflows would you recommend to others?

2. **What advanced techniques were most challenging?**
   - How did you overcome complex merge conflicts?
   - What recovery scenarios did you practice?

3. **How will these skills impact your contributions?**
   - What projects can you now contribute to more effectively?
   - How will you help others learn these techniques?

4. **What automation opportunities did you identify?**
   - Which manual processes can be automated with hooks?
   - How can CI/CD improve your workflow quality?

5. **How will you continue mastering Git?**
   - What advanced scenarios do you want to practice more?
   - Which Git features are you excited to explore further?

---

## 🔗 Navigation

[← Previous Day: Project Leadership](./day-13.md) | [Back to Main](../README.md) | [Next Day: Security and Best Practices →](./day-15.md)

---

💡 **Remember**: "Git is a tool that amplifies your ability to collaborate and manage complexity. Master the tool, and you master the craft."

**Incredible achievement! You've mastered the advanced Git workflows that power the world's largest open source projects. You can now handle complex development scenarios, implement sophisticated automation, and guide teams through efficient collaboration processes. Tomorrow, we'll focus on security and best practices to ensure your contributions are safe and professional! ⚡**