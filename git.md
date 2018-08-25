# Git

<div align="right">

[↤ back to Home](README.md)

</div>

## Contents

* [System Setup](#system-setup)
  * First Time System Setup
* [Repository Setup](#repository-setup)
  * Set a Remote Repository
* [Create a branch](#create-a-branch)
* [Merge a branch](#merge-a-branch)
---
<br>

## System Setup

### First Time System Setup
Set username and email
```Shell
$ git config --global user.name "<name>"
$ git config --global user.email your.name@email.com
```

Set to save credentials
```Shell
$ git config credential.helper store
```

<div align="right">

[↥ back to top](#git)

</div>
<br>

## Repository Setup

Navigate to the root directory of the app and initialize the new repository.
```shell
$ git init .
```

Create a .gitignore file, which will include files and directories that shouldn't be included in the repository
```shell
$ echo "<file-name.extension>" >> .gitignore
$ echo "<directory-name>" >> .gitignore
```

Add all project files to the repository.
```shell
$ git add -A
```

Check what is going to be included in the repository before actually committing to it.
```shell
$ git status
```

Remove files that were set to be included in the repository that shouldn't be.
```shell
$ git rm -r --cached <file-name.extension>
$ git rm -r --cached <directory-name>
```

Commit project files to the repository and include the commit message in the command line.
```shell
$ git commit -m "Initialize repository"
```

### Set a Remote Repository
Establish a remote SSH repository, make sure to replace <username> and <app> accordingly.
```shell
$ git remote add origin ssh://<link@repo>/<username>/<app>.git
```
  
Push the files to the remote repository.
```shell
$ git push -u origin --all
```

<div align="right">

[↥ back to top](#git)

</div>
<br>

## Create a Branch

Create a new branch.
```shell
$ git checkout -b <test-branch-name>
```

Show available branches.
```shell
$ git branch
```

<div align="right">

[↥ back to top](#git)

</div>
<br>

## Merge a Branch
Move to the master branch.
```shell
$ git checkout master
```

Merge the changes.
```shell
$ git merge <test-branch-name>
```

Delete the topic branch.
```shell
$ git branch -d <test-branch-name>
```

<div align="right">

[↥ back to top](#git)

</div>
<br>
