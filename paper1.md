# Git & GitHub — Complete Answers

## Q1. What is GitHub? What is a GitHub Repository?

### GitHub

**GitHub** is a cloud-based platform used to host Git repositories. It helps developers store, manage, collaborate on, and share their source code.

### GitHub Repository

A **GitHub repository (repo)** is a storage location for a project. It contains source code, files, folders, commits, branches, and project history.

### Example

Suppose we create a **Bank App** project:

```bash
Bank-App/
├── README.md
├── app.py
├── login.py
└── account.py
```

This project can be stored in a GitHub repository named:

```text
Bank-App
```

---

# Q2. What is a Version Control System (VCS)?

A **Version Control System (VCS)** is a system that tracks changes made to files over time.

It allows developers to:

* Track changes
* Restore previous versions
* Work with multiple developers
* Create branches
* Compare changes
* Maintain project history

## Types of VCS

### 1. Local Version Control System

The versions are stored on the local computer.

### 2. Centralized Version Control System (CVCS)

A central server stores the project and its history.

Examples:

* SVN
* CVS

### 3. Distributed Version Control System (DVCS)

Every developer has a complete copy of the repository and its history.

Examples:

* Git
* Mercurial

### Git

**Git** is a distributed version control system used to track changes in source code and manage different versions of a project.

---

# Q3. What is a `.gitignore` File?

A `.gitignore` file tells Git which files and folders should **not be tracked or committed** to the repository.

## Why is it used?

It is commonly used to ignore:

* Temporary files
* Build files
* IDE settings
* Dependencies
* Environment/configuration files containing local secrets

### Example 1 — Python

```gitignore
__pycache__/
*.pyc
```

This prevents Python cache files from being tracked.

### Example 2 — Environment File

```gitignore
.env
```

This prevents local environment/configuration files from being committed.

### Example `.gitignore`

```gitignore
# Python cache
__pycache__/

# Environment variables
.env

# VS Code settings
.vscode/
```

---

# Q4. What is a Collaborator in GitHub?

A **collaborator** is a person who has been given access to contribute to a GitHub repository.

A collaborator can generally work with the repository according to the permissions assigned to them.

## How to Add a Collaborator

1. Open the GitHub repository.
2. Go to **Settings**.
3. Open **Collaborators** / **Collaborators and teams**.
4. Click **Add people**.
5. Search for the person's GitHub username or email.
6. Select the person.
7. Send the invitation.

After accepting the invitation, the collaborator can work on the repository according to their granted permissions.

---

# Q5. Recover Deleted Branch and Deleted File

## A) Recover a Deleted Branch

If a branch was deleted but its commit still exists in the Git history/reflog, first find the commit:

```bash
git reflog
```

Find the commit where the deleted branch was pointing.

Then recreate the branch:

```bash
git switch -c branch-name commit-hash
```

### Example

```bash
git reflog
git switch -c feature-login abc1234
```

---

## B) Recover a Deleted File

### From the Latest Commit

If the file was deleted from the working tree but exists in the latest commit:

```bash
git restore --source=HEAD -- filename
```

Example:

```bash
git restore --source=HEAD -- login.py
```

### From a Different Commit

If the file needs to be recovered from another commit:

```bash
git restore --source=commit-hash -- filename
```

Example:

```bash
git restore --source=abc1234 -- login.py
```

---

# Q6. Revert a Commit and Change Previous Commit Message

## A) How to Revert a Commit?

`git revert` creates a **new commit** that reverses the changes introduced by an earlier commit.

### Command

```bash
git revert commit-hash
```

Example:

```bash
git revert abc1234
```

### Use Case

Suppose a commit introduced a bug:

```text
A → B → C
```

If commit `C` contains a problem, we can use:

```bash
git revert C
```

Git creates a new commit that reverses the changes made by `C`.

This is useful when the commit has already been shared with others and we want to preserve the project history.

---

## B) Change the Previous Commit Message

There are two common situations.

### Method 1 — Change Only the Commit Message

If the previous commit has no new changes to add:

```bash
git commit --amend -m "New commit message"
```

Example:

```bash
git commit --amend -m "Fix login validation"
```

### Method 2 — Change the Message and Add More Changes

First modify the required files:

```bash
git add filename
```

Then amend the previous commit:

```bash
git commit --amend -m "Updated commit message"
```

### Important

If the old commit has already been pushed to GitHub, amending changes its commit history. Updating the remote may require:

```bash
git push --force-with-lease
```

Use force-pushing carefully on shared branches.

---

# Q7. Branches, Commit Details, Tags and GitHub Projects

## A) Create and Switch to a New Branch

### Modern Command

```bash
git switch -c feature-login
```

This creates and switches to the new branch.

### Alternative

```bash
git checkout -b feature-login
```

---

## B) View Details of a Specific Commit

Use:

```bash
git show commit-hash
```

Example:

```bash
git show abc1234
```

This displays information such as:

* Commit ID
* Author
* Date
* Commit message
* Changes introduced by the commit

---

## C) What are Git Tags?

A **Git tag** is a reference used to mark a specific point in the Git history.

Tags are commonly used to mark releases such as:

```text
v1.0
v1.1
v2.0
```

### Create a Tag

```bash
git tag v1.0
```

### Tag a Specific Commit

```bash
git tag v1.0 commit-hash
```

### Push the Tag to GitHub

```bash
git push origin v1.0
```

Or push all tags:

```bash
git push origin --tags
```

---

## D) What is GitHub Projects?

**GitHub Projects** is a project-management feature that helps teams organize and track work related to repositories.

It can be used to manage:

* Tasks
* Issues
* Features
* Bugs
* Development progress

### Practical Use

For a **Bank App**, a project board could contain:

```text
Todo → In Progress → Review → Done
```

Team members can move tasks through these stages as development progresses.

---

# Q8. Complete Bank App Git Workflow

## Step 1 — Create Repository

Create a new repository on GitHub named:

```text
Bank-App
```

---

## Step 2 — Clone the Repository

Copy the repository URL and run:

```bash
git clone https://github.com/USERNAME/Bank-App.git
```

Move into the project:

```bash
cd Bank-App
```

---

## Step 3 — Create Project Files

Example:

```text
Bank-App/
├── README.md
├── app.py
├── login.py
└── account.py
```

Create/edit the required files.

---

## Step 4 — Check Repository Status

```bash
git status
```

---

## Step 5 — Add Files

Add all files:

```bash
git add .
```

Or add a specific file:

```bash
git add app.py
```

---

## Step 6 — Commit Changes

```bash
git commit -m "Initial Bank App setup"
```

---

## Step 7 — Push to GitHub

```bash
git push origin main
```

---

## Step 8 — Create a Feature Branch

Create and switch to a feature branch:

```bash
git switch -c feature-login
```

---

## Step 9 — Develop the Feature

Create or modify the required files.

Then check the changes:

```bash
git status
```

---

## Step 10 — Add and Commit Feature

```bash
git add .
git commit -m "Add login feature"
```

---

## Step 11 — Push Feature Branch

```bash
git push -u origin feature-login
```

---

## Step 12 — Merge the Feature

After reviewing the feature, switch back to `main`:

```bash
git switch main
```

Update the local branch:

```bash
git pull origin main
```

Merge the feature:

```bash
git merge feature-login
```

---

## Step 13 — Push the Merged Project

```bash
git push origin main
```

---

## Complete Workflow

```text
Create GitHub Repository
          ↓
       Clone Repo
          ↓
     Create Files
          ↓
       git add
          ↓
      git commit
          ↓
       git push
          ↓
 Create Feature Branch
          ↓
   Develop Feature
          ↓
       git add
          ↓
      git commit
          ↓
       git push
          ↓
   Review Feature
          ↓
    Switch to main
          ↓
      git merge
          ↓
       git push
          ↓
    Final Project
```

---

# Q9. Complete Release Workflow for Bank App v1.0

## Step 1 — Start with Main Branch

```bash
git switch main
git pull origin main
```

---

## Step 2 — Create Feature Branch

For example, create a login feature:

```bash
git switch -c feature-login
```

---

## Step 3 — Develop the Feature

Create or modify the required files.

Check the changes:

```bash
git status
```

---

## Step 4 — Commit the Feature

```bash
git add .
git commit -m "Add login feature"
```

---

## Step 5 — Push the Feature Branch

```bash
git push -u origin feature-login
```

---

## Step 6 — Collaboration and Code Review

Create a **Pull Request (PR)** on GitHub.

The team can:

* Review the code
* Discuss changes
* Request modifications
* Approve the Pull Request

---

## Step 7 — Merge the Feature

After the review is complete, merge the feature branch into `main`.

Then update the local repository:

```bash
git switch main
git pull origin main
```

---

## Step 8 — Prepare the v1.0 Release

Make sure the project is working correctly.

Check the commit history:

```bash
git log --oneline
```

---

## Step 9 — Create Release Tag

Create the `v1.0` tag:

```bash
git tag v1.0
```

---

## Step 10 — Push the Tag to GitHub

```bash
git push origin v1.0
```

Or:

```bash
git push origin --tags
```

The repository now contains the tagged version:

```text
v1.0
```

---

## Step 11 — Critical Bug Found After Release

If a critical bug is found in the released version, identify the commit that introduced the problematic change.

```bash
git log --oneline
```

Then revert the problematic commit:

```bash
git revert commit-hash
```

Example:

```bash
git revert abc1234
```

---

## Step 12 — Push the Revert

```bash
git push origin main
```

This creates a new commit that reverses the problematic changes while preserving the existing history.

---

# Complete Release Flow

```text
Feature Development
        ↓
Create Feature Branch
        ↓
Write Code
        ↓
Commit Changes
        ↓
Push Feature Branch
        ↓
Create Pull Request
        ↓
Code Review
        ↓
Approval
        ↓
Merge into Main
        ↓
Test Final Project
        ↓
Create v1.0 Tag
        ↓
Push Tag to GitHub
        ↓
v1.0 Released
        ↓
Critical Bug Found
        ↓
Identify Problematic Commit
        ↓
git revert commit-hash
        ↓
Push Revert
        ↓
Fixed Main Branch
```

---

# Quick Git Command Reference

| Task                | Command                                           |
| ------------------- | ------------------------------------------------- |
| Clone repository    | `git clone <url>`                                 |
| Check status        | `git status`                                      |
| Add files           | `git add .`                                       |
| Commit              | `git commit -m "message"`                         |
| Push                | `git push origin main`                            |
| Pull                | `git pull origin main`                            |
| Create branch       | `git switch -c branch-name`                       |
| Switch branch       | `git switch branch-name`                          |
| Merge branch        | `git merge branch-name`                           |
| View commits        | `git log --oneline`                               |
| View commit details | `git show commit-hash`                            |
| Revert commit       | `git revert commit-hash`                          |
| Amend commit        | `git commit --amend -m "message"`                 |
| Recover branch      | `git reflog` + `git switch -c branch commit-hash` |
| Restore file        | `git restore --source=commit -- filename`         |
| Create tag          | `git tag v1.0`                                    |
| Push tag            | `git push origin v1.0`                            |
| Push all tags       | `git push origin --tags`                          |

---

## Conclusion

Git and GitHub provide a complete workflow for managing source code, tracking changes, collaborating with team members, working with branches, reviewing code, and releasing different versions of a project.

The **Bank App** workflow demonstrates how these Git and GitHub features can be combined from initial project creation through feature development, collaboration, merging, release tagging, and handling a critical bug.
