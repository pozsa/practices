## Contents
[How to set up your local repo](#how-to-set-up-your-local-repo)\
&nbsp;&nbsp;[1. Fork the organization repository](#1-fork-the-organization-repository)\
&nbsp;&nbsp;[2. Create a local clone of your fork](#2-create-a-local-clone-of-your-fork)\
&nbsp;&nbsp;[3. Set up a new remote pointing to the organization's repository](#3-set-up-a-new-remote-pointing-to-the-organizations-repository)\
&nbsp;&nbsp;[4. Set your local master branch to track \<remote-name\>/master](#4-set-your-local-master-branch-to-track-remote-namemaster)\
[Development workflow](#development-workflow)\
&nbsp;&nbsp;[1. Use local feature branches](#1-use-local-feature-branches)\
&nbsp;&nbsp;[2. Do work](#2-do-work)\
&nbsp;&nbsp;[3. Commit your changes](#3-commit-your-changes)\
&nbsp;&nbsp;[4. Push your changes to your forked repository](#4-push-your-changes-to-your-forked-repository)\
&nbsp;&nbsp;[5. Open a Merge/Pull Request to merge your changes](#5-open-a-merge/pull-request-to-merge-your-changes)\
&nbsp;&nbsp;[6. Merge your MR/PR once approved](#6-merge-your-mr/pr-once-approved)\
&nbsp;&nbsp;[7. Clean up your remote and local repositories](#7-clean-up-your-remote-and-local-repositories)\
&nbsp;&nbsp;[8. Sync \<remote-name\>/master to your local master](#8-sync-remote-namemaster-to-your-local-master)\
[Basic Git commands](#basic-git-commands)

## How to set up your local repo

### 1. Fork the organization repository
\# TODO: add more detailed guide

### 2. Create a local clone of your fork
```git
git clone <url>
``` 
Typical protocols that are used, and their url syntax with `GitHub`:\
HTTPS: `https://github.com/<username>/<repo-name>.git`\
SSH: `git@github.com:<username>/<repo-name>.git`\
\# TODO: add gitlab syntax and example
#### Example
username: pozsa\
repo-name: demo-github-best-practices\
method: ssh
```bash
$ git clone git@github.com:pozsa/demo-github-best-practices.git
Cloning into 'demo-github-best-practices'...
remote: Counting objects: 10, done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 10 (delta 1), reused 7 (delta 0), pack-reused 0
Receiving objects: 100% (10/10), done.
Resolving deltas: 100% (1/1), done.
Checking connectivity... done.
$ cd demo-github-best-practices/
$ git remote -v
origin  git@github.com:pozsa/demo-github-best-practices.git (fetch)
origin  git@github.com:pozsa/demo-github-best-practices.git (push)
```

### 3. Set up a new remote pointing to the organization's repository
```git
git remote add <remote-name> <url>
git fetch <remote-name>
```
where `<remote-name>` is traditionally set to `upstream`
#### Example
```bash
$ git remote add upstream git@github.com:4th-IR/demo-github-best-practices.git
$ git remote -v
origin  git@github.com:pozsa/demo-github-best-practices.git (fetch)
origin  git@github.com:pozsa/demo-github-best-practices.git (push)
upstream        git@github.com:4th-IR/demo-github-best-practices.git (fetch)
upstream        git@github.com:4th-IR/demo-github-best-practices.git (push)
$ git fetch upstream
remote: Counting objects: 25, done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 25 (delta 6), reused 20 (delta 5), pack-reused 0
Unpacking objects: 100% (25/25), done.
From github.com:4th-IR/demo-github-best-practices
 * [new branch]      master     -> upstream/master
```

### 4. Set your local master branch to track \<remote-name\>/master
```git
git branch -u <remote-name>/master
```
#### Example
```bash
$ git branch -avv
* master                  4746caa [origin/master] Add link to wiki home page (#1)
  remotes/origin/HEAD     -> origin/master
  remotes/origin/master   4746caa Add link to wiki home page (#1)
  remotes/upstream/master 8a395a2 test access rights
$ git branch -u upstream/master
Branch master set up to track remote branch master from upstream.
$ git branch -avv
* master                  4746caa [upstream/master: behind 8] Add link to wiki home page (#1)
  remotes/origin/HEAD     -> origin/master
  remotes/origin/master   4746caa Add link to wiki home page (#1)
  remotes/upstream/master 8a395a2 test access rights
```

## Development workflow

### 1. Use local feature branches
... or as Enrico Campidoglio said
> Branch like there's no tomorrow
```git
git checkout -b <branch-name>
```
#### Example
```bash
$ git checkout -b new_feature
Switched to a new branch 'new_feature'
```

### 2. Do work

### 3. Commit your changes
Write a good commit message - (git-commit-guidelines.md)
```git
git add .
git commit
```

### 4. Push your changes to your forked repository
```git
git push -u origin <branch-name>
```
#### Example
```bash
$ git push -u origin new_feature
Counting objects: 30, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (24/24), done.
Writing objects: 100% (30/30), 378.12 KiB | 0 bytes/s, done.
Total 30 (delta 7), reused 3 (delta 0)
remote: Resolving deltas: 100% (7/7), done.
To git@github.com:pozsa/demo-github-best-practices.git
 * [new branch]      new_feature -> new_feature
Branch new_feature set up to track remote branch new_feature from origin.
```

### 5. Open a Merge/Pull Request to merge your changes
Flag team member(s) to review the merge/pull request\
\# TODO: add guide on code review

### 6. Merge your MR/PR once approved
\# TODO: the below is github specific, rewrite for gitlab\
Use `Squash and merge` if you have multiple commits in a PR to aid the PR review, but the end goal is to have a single commit in the master branch. In all other cases use `Rebase and merge`. More information [here](https://help.github.com/articles/about-pull-request-merges/).

### 7. Clean up your remote and local repositories
```git
git push origin --delete <branch-name>
git checkout master
git branch --delete <branch-name>
```
#### Example
```bash
$ git push origin --delete new_feature
To git@github.com:pozsa/demo-github-best-practices.git
 - [deleted]         new_feature
$ git checkout master
Switched to branch 'master'
Your branch is behind 'upstream/master' by 9 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
$ git branch --delete new_feature
error: The branch 'new_feature' is not fully merged.
If you are sure you want to delete it, run 'git branch -D new_feature'.
$ git branch -D new_feature
Deleted branch new_feature (was fb068ab).
```
#### Common Errors
The branch does not exist on the remote. It never existed to begin with or it has been already deleted.
```bash
$ git push origin --delete cheatsheet
error: unable to delete 'cheatsheet': remote ref does not exist
error: failed to push some refs to 'git@github.com:pozsa/demo-github-best-practices.git'
```
Switch to a different branch to be able to delete a local branch
```bash
$ git branch --delete new_feature
error: Cannot delete the branch 'new_feature' which you are currently on.
```
Git detects a potential situation where you might be losing work. If you are not sure that your changes have been merged, then investigate first.
```bash
$ git branch --delete new_feature
error: The branch 'new_feature' is not fully merged.
If you are sure you want to delete it, run 'git branch -D new_feature'.
```

### 8. Sync \<remote-name\>/master to your local master
```git
git pull --rebase
```
#### Example
```bash
$ git status
On branch master
Your branch is behind 'upstream/master' by 9 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
$ git pull --rebase
First, rewinding head to replay your work on top of it...
Fast-forwarded master to fb068ab759dd5e972e50df9941f609061e7c07f2.
$ git status
On branch master
Your branch is up-to-date with 'upstream/master'.
nothing to commit, working directory clean
```

## Basic Git commands
- [`git add`](https://git-scm.com/docs/git-add) - Add file contents to the index (staging)
- [`git branch`](https://git-scm.com/docs/git-branch) - List, create, or delete branches
- [`git checkout`](https://git-scm.com/docs/git-checkout) - Switch branches or restore working tree files
- [`git clone`](https://git-scm.com/docs/git-clone) - Clone a repository into a new directory
- [`git commit`](https://git-scm.com/docs/git-commit) - Record changes to the repository
- [`git diff`](https://git-scm.com/docs/git-diff) - Show changes between commits, commit and working tree, etc
- [`git fetch`](https://git-scm.com/docs/git-fetch) - Download objects and refs from another repository
- [`git merge`](https://git-scm.com/docs/git-merge) - Join two or more development histories together
- [`git pull`](https://git-scm.com/docs/git-pull) - Fetch from and integrate with another repository or a local branch
- [`git push`](https://git-scm.com/docs/git-push) - Update remote refs along with associated objects
- [`git rebase`](https://git-scm.com/docs/git-rebase) - Reapply commits on top of another base tip
- [`git remote`](https://git-scm.com/docs/git-remote) - Manage set of tracked repositories
- [`git status`](https://git-scm.com/docs/git-status) - Show the working tree status