
# 📘 Git Interview Questions – For Testers & Developers

A curated list of commonly asked Git interview questions, categorized by skill level.

---

## 🔹 Basic Git Questions

1. **What is Git and why is it used?**  
   Git is a distributed version control system used to track changes in source code during software development. It allows multiple developers to work on a project simultaneously.

2. **What is the difference between Git and GitHub/GitLab/Bitbucket?**  
   Git is the version control tool. GitHub/GitLab/Bitbucket are platforms for hosting Git repositories with additional collaboration features.

3. **What is the difference between `git pull` and `git fetch`?**  
   `git pull` fetches and merges changes from the remote.  
   `git fetch` only downloads changes without merging.

4. **What does `git status` do?**  
   It shows the current state of the working directory and staging area.

5. **How do you clone a repository?**  
   ```bash
   git clone <repository-url>
````

6. **What is `.gitignore`?**
   A file listing patterns of files and directories to be ignored by Git.

---

## 🔹 Intermediate Git Questions

1. **How do you create and switch to a new branch?**

   ```bash
   git checkout -b new-branch
   ```

2. **What is the difference between `git merge` and `git rebase`?**

   * `merge` keeps the history as is and adds a merge commit.
   * `rebase` rewrites history for a linear flow.

3. **How do you resolve merge conflicts?**
   Manually edit conflicting files, then run:

   ```bash
   git add <file>
   git commit
   ```

4. **How do you undo a commit?**

   * To modify the last commit: `git commit --amend`
   * To undo and keep changes: `git reset --soft HEAD~1`
   * To undo and discard changes: `git reset --hard HEAD~1`

5. **What is `git stash` used for?**
   Temporarily shelves changes so you can work on something else.

---

## 🔹 Advanced Git Topics

1. **Explain `git cherry-pick`.**
   Applies the changes introduced by an existing commit onto the current branch.

2. **Difference between `git reset`, `git revert`, and `git checkout`?**

   * `reset`: Moves HEAD and changes history
   * `revert`: Creates a new commit to undo a previous one
   * `checkout`: Switches branches or restores files

3. **What is a Git tag?**
   Tags mark specific points in history, usually for releases.

4. **Explain a branching strategy you’ve used.**
   Example: Git Flow, Feature Branching, or Trunk-Based Development.

5. **What are hooks in Git?**
   Scripts that run before/after Git events like commit, push, etc.

6. **How do you enable code reviews in Git workflows?**
   Using Pull Requests (PRs) with reviewer assignments and automated checks.

---

## 🛠 Common Git Commands Cheat Sheet

```bash
git init                 # Initialize repo
git clone <url>          # Clone repo
git add .                # Stage changes
git commit -m "msg"      # Commit changes
git status               # See status
git push origin branch   # Push to remote
git pull                 # Pull from remote
git log --oneline        # Short log
git branch               # List branches
git checkout -b feature  # Create/switch branch
git merge branch         # Merge branch
git stash                # Stash changes
git tag v1.0             # Create tag
```

---

## ✅ Best Practices

* Use meaningful commit messages
* Create pull requests for code reviews
* Keep branches short-lived
* Avoid force-push on shared branches
* Regularly pull latest changes before pushing

---

> ✨ Follow [Shaivi Connect](https://github.com/shaiphali123) for more dev/tester-friendly interview content!



Let me know!
```
