# Git

Git can keep track of changes made to code, synchronize code between different people, test changes to code without losing the original, and revert back to old versions of code.

GitHub is a website that stores Git repositories on the internet to facilitate the collaboration that Git allows for. A repository is simply a place to keep track of code and all the changes to code.

## System Setup

### First time system setup
Set username and email
```Shell
$ git config --global user.name "<name>"
$ git config --global user.email your.name@email.com
```

Set to save credentials
```Shell
$ git config credential.helper store
```

## Commands reference

* `git clone <url>` take a repository stored on a server (like GitHub) and downloads it
* `git init .` initialize the current directory as a new repository
* `git add <filename(s)>` add files to the staging area to be included in the next commit
* `git add -A` add all project files to the staging area to be included in the next commit
* `git commit -m "message"` take a snapshot of the repository and save it with a message about the changes
* `git commit -am <filename(s)> "message"` add files and commit changes all in one
* `git status` print what is currently going on with the repository
* `git push` push any local changes (commits) to a remote server
* `git pull` pull any remote changes from a remote server to a local computer
* `git log` print a history of all the commits that have been made
* `git reflog` print a list of all the different references to commits
* `git reset --hard <commit>` reset the repository to a given commit
* `git reset --hard origin/master` reset the repository to its original state (e.g. the version cloned from GitHub)
* `git rm -r --cached <filename(s)>` remove files that were set to be included in the repository and shouldn't be
* `git checkout -b <test-branch-name>` create a new branch
* `git branch` print available branches
* `git checkout master` move the master branch
* `git merge <branch-name>` merge the branch
* `git branch -d <branch-name>` delete the topic branch

## Excluding files
Create a .gitignore file, which should include all files and directories that shouldn't be committed to the repository
```shell
$ echo "<filename(s)>" >> .gitignore
```
