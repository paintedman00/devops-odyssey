# Git Notes

## Table of Contents
1. [Introduction](#introduction)
2. [Installation and Configuration](#installation-and-configuration)
3. [Basic Git Commands](#basic-git-commands)
4. [Branch Management](#branch-management)
5. [Staging and Committing](#staging-and-committing)
6. [File Management](#file-management)
7. [Stash Management](#stash-management)
8. [Remote Repositories](#remote-repositories)
9. [Git Bash Commands](#git-bash-commands)
10. [Git Workflow and Best Practices](#git-workflow-and-best-practices)
11. [Advanced Git Commands](#advanced-git-commands)
12. [Open Source Contribution](#open-source-contribution)
13. [Git Lifecycle](#git-lifecycle)
14. [Difference Between Merge and Rebase](#difference-between-merge-and-rebase)
15. [Troubleshooting](#troubleshooting)
16. [Additional Resources](#additional-resources)
17. [Glossary](#glossary)
18. [Cheat Sheet](#cheat-sheet)

## Introduction
Git is a distributed version control system designed to handle everything from small to very large projects with speed and efficiency. GitHub is a web-based platform that uses Git for version control and collaboration.

## Installation and Configuration

### Check Git Version
```sh
git --version
```

### Install Git
#### Windows
1. Go to the Git website: [git-scm.com/downloads](https://git-scm.com/downloads)
2. Download and run the installer.
3. Follow the prompts to complete the installation.

#### Mac OS
1. Install Xcode Command Line Tools:
    ```sh
    xcode-select --install
    ```
2. Install Homebrew package manager:
    ```sh
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
3. Use Homebrew to install Git:
    ```sh
    brew install git
    ```

#### Linux
1. Update the package index:
    ```sh
    sudo apt-get update
    ```
2. Install Git:
    ```sh
    sudo apt-get install git
    ```

### Initial Git Configuration
#### Configure User Name
```sh
git config --global user.name "your_github_username"
```

#### Configure Email
```sh
git config --global user.email "your_email@example.com"
```

#### Set Preferred Text Editor
```sh
git config --global core.editor "editor-of-your-choice"
```

#### Check Git Configuration
```sh
git config --list
```

## Basic Git Commands

### Initialize a New Git Repository
```sh
git init
```

### Clone an Existing Repository
```sh
git clone <repository-url>
```

### View Commit Log
```sh
git log
```

### Checkout a Specific Commit
```sh
git checkout <hash-code>
```

### Add and Commit Files
#### Add Files to Staging
```sh
git add <file>
```
#### Commit with a Message
```sh
git commit -m "commit message"
```

### View Current Tree Status
```sh
git status
```

## Branch Management

### Create a New Branch
```sh
git branch <branchName>
```

### Switch to Branch
```sh
git checkout <branchName>
```

### Create and Switch to New Branch
```sh
git checkout -b <branchName>
```

### List Local Branches
```sh
git branch -a
```

### List Remote Branches
```sh
git branch -r
```

### Rename Local Branch
```sh
git branch -m $NEW_BRANCH_NAME
```

### Rename Remote Branch
```sh
git push origin :$OLD_BRANCH_NAME $NEW_BRANCH_NAME
git push origin -u $NEW_BRANCH_NAME
```

### Delete Local Branch
```sh
git branch -d $BRANCH_NAME
```

### Delete Remote Branch
```sh
git push origin --delete $BRANCH_NAME
```

### Merge Branch
```sh
git merge <branchName>
```

## Staging and Committing

### Stage Changes
```sh
git add <file>
```

### Stage All Changes
```sh
git add .
```

### Add All Files with Specific Extension
```sh
git add *.<fileExtension>
```

### Unstage a File
```sh
git reset <hashNum>
```

### Remove File from Staging
```sh
git restore --staged <file>
git rm --cached <file>
```

### Commit with a Message
```sh
git commit -m "<message>"
```

### Combined Commands
1. Stage & Commit:
    ```sh
    git commit -a -m "message"
    ```
2. Create Branch & Checkout:
    ```sh
    git checkout -b branchname
    ```

## File Management

### List Hidden Files
```sh
ls -a
```

### Create a File
```sh
touch <file>
```

### View File Contents
```sh
cat <file>
```

### Delete a File
```sh
rm -rf <file>
```

## Stash Management

### Stash Changes
```sh
git stash
```

### Stash with Message
```sh
git stash save "<message>"
```

### List Stashes
```sh
git stash list
```

### Apply Stash
```sh
git stash apply
```

### Pop Stash
```sh
git stash pop
```

### Clear Stash
```sh
git stash clear
```

### Create a Branch from Stash
```sh
git stash branch $BRANCH_NAME
```

### Drop a Specific Stash
```sh
git stash drop $STASH_ID
```

## Remote Repositories

### Add Remote Repository
```sh
git remote add origin <https://gitRepoURL.git>
```

### View Remote URLs
```sh
git remote -v
```

### Push Changes to Remote
```sh
git push origin <HEAD Branch>
```

### Pull Remote Changes
```sh
git pull
```

### Remove Remote URL
```sh
git remote rm origin
```

### Update Remote URL
```sh
git remote set-url origin <newRemoteRepoURL.git>
```

### Add Upstream Repository
```sh
git remote add upstream <URL>
```

### Check Remote Repository
```sh
git remote
```

## Git Bash Commands

### Move to Previous Directory
```sh
cd ..
```

### Move to Home Directory
```sh
cd ~
```

### Move to Root Directory
```sh
cd /
```

## Git Workflow and Best Practices

### Git Tutorials
1. [GitHub Learning Lab](https://lab.github.com/)
2. [Git Started with GitHub](https://www.udemy.com/course/git-started-with-github/)
3. [Version Control with Git](https://www.udacity.com/course/version-control-with-git--ud123)
4. [Atlassian Git Tutorial](https://www.atlassian.com/git)
5. [Learn Git Branching](https://learngitbranching.js.org/)

### Basic Git Flow
1. Initialize Git repository:
    ```sh
    git init
    ```
2. Add and commit files:
    ```sh
    git add .
    git commit -m "commit message"
    ```
3. Create a README.md file.
4. Create a remote repository on GitHub/GitLab/Bitbucket.
5. Link local repository to remote:
    ```sh
    git remote add origin $URL_TO_YOUR_REMOTE_REPOSITORY
    ```
6. Push local files to remote:
    ```sh
    git push origin master
    ```
7. Fetch changes from remote:
    ```sh
    git pull origin master
    ```

### Best Practices
- **Write Clear Commit Messages**: Use the imperative mood, be descriptive, and include relevant references.
- **Pull Before You Push**: Ensure you are working with the latest code.
- **Use Branches**: Isolate new features, bug fixes, and experiments.

## Advanced Git Commands

### Git Rebase
- Rebase current branch onto another branch:
    ```sh
    git rebase <branch>
    ```

### Git Squash
- Squash commits into one:
    ```sh
    git rebase -i HEAD~n
    ```

### Git Revert
- Revert a specific commit:
    ```sh
    git revert <commit>
    ```

### Git Reset
- Soft reset (keeps changes in working directory):
    ```sh
    git reset --soft <commit>
    ```
- Hard reset (discards all changes):
    ```sh
    git reset --hard <commit>
    ```

### Tags and Releases
- Create a tag:
    ```sh
    git tag <tagname>
    ```
- Push tag to remote:
    ```sh
    git push origin <tagname>
    ```
- Delete a tag:
    ```sh
    git tag -d <tagname>
    ```

### Git Restore
- Restore file to a previous version:
    ```sh
    git restore <file>
    ```
- Unstage changes:
    ```sh
    git restore --staged <file>
    ```
- Restore to a specific commit:
    ```sh
    git restore --source=<commit> <file>
    ```

## Open Source Contribution

### Contributing to an Open Source Project


1. Fork the repository on GitHub.
2. Clone the forked repository:
    ```sh
    git clone https://github.com/<your_username>/<repository_name>.git
    ```
3. Create a new branch:
    ```sh
    git branch <new_branch_name>
    git checkout <new_branch_name>
    ```
4. Make your changes.
5. Add and commit your changes:
    ```sh
    git add <file_name>
    git commit -m "Your commit message"
    ```
6. Push changes to your fork:
    ```sh
    git push origin <new_branch_name>
    ```
7. Open a pull request on GitHub.

### Pull Request Workflow
1. Create a new branch.
2. Make changes and commit them.
3. Push changes to GitHub.
4. Open a pull request.
5. Review and test by team members.
6. Merge the pull request once approved.
7. Close the pull request.

## Git Lifecycle

### Git File Lifecycle
1. **Untracked**: Newly created files.
2. **Staged**: Files added to staging area.
3. **Committed**: Files committed to repository.
4. **Modified**: Files with changes not yet staged.
5. **Tracked**: Files being tracked by Git.

## Difference Between Merge and Rebase

### Merge
- Creates a merge commit combining changes from two branches.
- Preserves complete history and commit structure.

### Rebase
- Reapplies commits from one branch onto another.
- Results in a linear history, avoiding merge commits.
- Useful for cleaning up commit history.

## Troubleshooting

### Common Issues and Solutions
- **Merge Conflicts**: Occur when two branches have made changes to the same lines in a file. Resolve conflicts manually and commit the changes.
- **Detached HEAD**: Occurs when you checkout a specific commit. To return to a branch, use:
    ```sh
    git checkout <branchName>
    ```

## Additional Resources

### Links to Tutorials and Documentation
- [Git Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book/en/v2)
- [GitHub Help](https://help.github.com/)

## Glossary

### General VCS Terminology
- **Project**: Set of source code needed to build software.
- **Repository**: Storage for project files and history.
- **Branch**: Active line of development.
- **Feature**: Large, complex part of a project.

### Git-Specific Terminology
- **Working Tree**: Current set of files being worked on.
- **Repository**: Working tree plus `.git` directory.
- **Bare Repository**: Repository without a working tree.
- **Commit**: Snapshot of the working tree.
- **SHA**: Unique identifier for a commit.
- **Branch**: Pointer to the most recent commit in a line of development.
- **Tag**: Fixed reference to a specific commit.
- **Head**: Latest commit in a branch.
- **Index**: Staging area for the next commit.

## Cheat Sheet

### Quick Reference to Common Commands
- **Initialize a repository**: `git init`
- **Clone a repository**: `git clone <repository-url>`
- **Add files to staging**: `git add <file>`
- **Commit changes**: `git commit -m "commit message"`
- **Push changes**: `git push origin <branch>`
- **Pull changes**: `git pull`
- **Create branch**: `git branch <branchName>`
- **Switch branch**: `git checkout <branchName>`
- **Merge branch**: `git merge <branchName>`
- **Stash changes**: `git stash`
- **Apply stash**: `git stash apply`
- **List branches**: `git branch -a`
- **View commit log**: `git log`
- **Check status**: `git status`
- **Reset changes**: `git reset <commit>`
