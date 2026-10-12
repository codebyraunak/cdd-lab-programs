# Git and GitHub Collaboration Lab

A practical record of the Git and GitHub commands demonstrated in the lab screenshots. The exercises cover local repository setup, commits, remote repositories, cloning, pushing and pulling, branches, merging, merge-conflict handling, and GitHub pull requests.

**Repository shown in the screenshots:**  
- `Team_Collaboration_CDD`: https://github.com/codebyraunak/Team_Collaboration_CDD  
- `cdd-lab-programs`: https://github.com/codebyraunak/cdd-lab-programs

> Note: The screenshots show terminal commands and filenames such as `cdd.txt`, `cdd1.txt`, and `new.txt`, but do not reveal the complete contents of those files. The sample file contents below are illustrative; use the actual lab files if they differ.

## 1. Requirements

- Git installed on the computer
- Git Bash (used in the screenshots)
- A GitHub account
- Internet access for GitHub operations

Check the installation:

```bash
git --version
```

## 2. Configure Git

Set the name and email that Git records on commits:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

View the configuration:

```bash
git config --list
```

The screenshots also show these values being configured:

```bash
git config --global user.name "Raunak Kumar"
git config --global user.email "rkraunak957@gmail.com"
```

Use your own name and email when setting up a different computer or account.

## 3. Create a local repository and make the first commit

Create a project folder, enter it, create a text file, initialize Git, stage the file, and commit it:

```bash
mkdir cdd
cd cdd
touch cdd.txt
git init
git status
git add .
git status
git commit -m "first commit"
```

The screenshots show `git init` creating a repository and `cdd.txt` being committed.

### What these commands do

| Command | Purpose |
|---|---|
| `mkdir cdd` | Creates a folder named `cdd` |
| `cd cdd` | Enters the folder |
| `touch cdd.txt` | Creates an empty text file in Git Bash |
| `git init` | Initializes a Git repository |
| `git status` | Shows the current branch and file status |
| `git add .` | Stages all changes in the current directory |
| `git add cdd.txt` | Stages one specific file |
| `git commit -m "first commit"` | Saves staged changes in a commit |

Example of text that could be placed in `cdd.txt`:

```text
CDD Git lab
Practising Git initialization, staging, commits, and GitHub push.
```

## 4. Connect the local repository to GitHub

Create an empty GitHub repository first, then add its URL as the `origin` remote.

```bash
git remote add origin https://github.com/codebyraunak/cdd-lab-programs.git
git remote -v
git branch -M main
git push -u origin main
```

- `origin` is the conventional name for the primary remote.
- `git branch -M main` renames the current branch to `main`.
- `git push -u origin main` uploads the branch and sets its upstream tracking branch.

The screenshots show the `cdd` local repository being pushed to the `cdd-lab-programs` GitHub repository.

## 5. Clone an existing repository

Clone the remote repository to your computer:

```bash
cd ~/Downloads
git clone https://github.com/codebyraunak/cdd-lab-programs
cd cdd-lab-programs
git status
```

For the other repository shown in the screenshots:

```bash
git clone https://github.com/codebyraunak/Team_Collaboration_CDD
cd Team_Collaboration_CDD
```

`git clone` downloads the repository and creates a local working directory with its Git history and remote configuration.

## 6. Stage, commit, and push changes

After editing or creating a file, use this sequence:

```bash
git status
git add .
git status
git commit -m "added a new file"
git push origin main
```

A second example from the screenshots:

```bash
git add cdd1.txt
git commit -m "added cdd1"
git push origin main
```

Another commit message shown was:

```bash
git commit -m "new file"
```

Use a commit message that describes the change you actually made. If Git reports `nothing to commit, working tree clean`, there are no new staged changes to commit.

## 7. Create and work on a branch

Create a branch and switch to it:

```bash
git checkout -b raunak
```

Modern equivalent:

```bash
git switch -c raunak
```

Switch between existing branches:

```bash
git switch main
git switch raunak
```

List local branches and identify the current branch:

```bash
git branch
```

The current branch is marked with `*`.

Stage and commit work on the feature branch:

```bash
git add .
git commit -m "commit1"
```

The screenshots also show a second branch commit:

```bash
git add .
git commit -m "2nd commit"
```

Push a branch to GitHub:

```bash
git push -u origin raunak
```

After pushing, GitHub may print a URL for opening a pull request.

## 8. Fetch, pull, and synchronize branches

```bash
git fetch
git fetch origin
git pull origin main
git push origin main
```

- `git fetch` downloads remote updates but does not merge them into the current branch.
- `git pull origin main` fetches and integrates updates from the remote `main` branch into the current branch.
- `git push origin main` uploads local commits on `main` to the remote.

Fetch and pull are not identical. Use `git status` and inspect the branch before integrating changes.

## 9. Merge branches

To merge work from `raunak` into `main`:

```bash
git switch main
git merge raunak
```

If the histories can be combined automatically, Git may perform a fast-forward merge. The screenshots show a fast-forward merge updating `cdd1.txt`.

To merge `main` into your feature branch instead, switch to the feature branch first:

```bash
git switch raunak
git merge main
```

The branch you are currently on is the **destination** branch: `git merge <branch-name>` brings the named branch into the current branch.

## 10. Resolve a merge conflict

A conflict can occur when two branches change overlapping parts of the same file. The screenshots show a conflict in `cdd1.txt`.

Check the repository state:

```bash
git status
```

Open the conflicted file. Git may mark the conflicting sections like this:

```text
<<<<<<< HEAD
Content from the current branch
=======
Content from the branch being merged
>>>>>>> raunak
```

Edit the file to keep the correct final content and remove all conflict markers. Then stage and complete the merge:

```bash
git add cdd1.txt
git status
git commit -m "Resolve merge conflict"
```

If Git has already started a merge, do not try to switch branches until the merge is completed or aborted. To abandon the merge instead of resolving it:

```bash
git merge --abort
```

Only use `git merge --abort` if you intend to cancel the in-progress merge.

### Common messages shown in the screenshots

- **`branch 'raunak' already exists`**: create it only once; use `git switch raunak` to return to it.
- **`nothing to commit, working tree clean`**: there are no uncommitted changes.
- **`pathspec ... did not match any files`**: check the filename and spelling, including the extension. For example, `git add cdd1.txt` rather than `git add cdd1`.
- **`'u' does not appear to be a git repository`**: the push command is missing the remote name. Use `git push -u origin main`, not `git push -u main`.
- **`remote origin already exists`**: inspect it with `git remote -v`. If its URL is wrong, update it with `git remote set-url origin <repository-url>`.
- **`repository not found`**: verify the remote URL, repository existence, permissions, and authentication.
- **`You have unmerged paths` / `MERGE_HEAD exists`**: resolve and stage the conflict, then commit; or deliberately abort the merge.
- **`Already up to date`**: Git found no new changes to merge from that branch.

## 11. GitHub repository collaboration

The screenshots show pushing the `raunak` branch to GitHub and a message inviting the user to create a pull request.

Typical workflow:

1. Create a feature branch.
2. Make and commit changes.
3. Push the feature branch.
4. Open GitHub and create a pull request from `raunak` into `main`.
5. Review the changed files and discuss or request changes if needed.
6. Merge the pull request after review and checks pass.
7. Update the local `main` branch:

```bash
git switch main
git pull origin main
```

A **fork** is a GitHub-side copy of another repository under your account. A **pull request (PR)** proposes that changes from one branch or repository be reviewed and merged into another. For a fork-based workflow, the original project is often configured as `upstream`:

```bash
git remote add upstream https://github.com/OWNER/REPOSITORY.git
git remote -v
git fetch upstream
```

Only add `upstream` when it points to the original repository you intend to track. In the screenshots, the `upstream` example points to the same `Team_Collaboration_CDD` URL as `origin`; in a real fork workflow, `origin` normally points to your fork and `upstream` to the original project.

## 12. Useful command reference

| Task | Command |
|---|---|
| Check Git version | `git --version` |
| Initialize repository | `git init` |
| Inspect status | `git status` |
| Stage all changes | `git add .` |
| Stage one file | `git add filename` |
| Commit staged changes | `git commit -m "message"` |
| Show branches | `git branch` |
| Create and switch branch | `git checkout -b branch-name` |
| Switch branch | `git switch branch-name` |
| Clone repository | `git clone <url>` |
| View remotes | `git remote -v` |
| Add remote | `git remote add origin <url>` |
| Fetch remote changes | `git fetch origin` |
| Pull a branch | `git pull origin main` |
| Push a branch | `git push origin main` |
| Push and set upstream | `git push -u origin branch-name` |
| Merge a branch into current branch | `git merge branch-name` |
| Abort an in-progress merge | `git merge --abort` |
| Rename current branch | `git branch -M main` |
| View recent commits | `git log --oneline` |
| Show changed lines | `git diff` |

## 13. Lab outcomes

After completing these exercises, you should be able to:

- Install and configure Git.
- Create a local repository and perform basic Git operations.
- Clone repositories and synchronize local work with GitHub using fetch, pull, and push.
- Create and switch branches, merge changes, and resolve merge conflicts.
- Work with GitHub repositories, forks, pull requests, and code reviews.

## 14. Suggested evidence for submission

Include screenshots showing:

- Git configuration and repository initialization.
- A successful commit and push.
- A cloned repository and a successful fetch/pull.
- Branch creation and switching.
- A successful merge and, if required, conflict resolution.
- The GitHub repository and pull request page.

---

**Repository links**

- [Team_Collaboration_CDD](https://github.com/codebyraunak/Team_Collaboration_CDD)
- [cdd-lab-programs](https://github.com/codebyraunak/cdd-lab-programs)
