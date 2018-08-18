# Git

## Contents
1 [System setup](#system-setup)
2 [Repository setup](#repository-setup)
3 [Create a branch](#create-a-branch)
4 [Merge a branch](#merge-a-branch)
---
<br><br>

## System setup

### First time system setup
###### 1. Set your username
```shell
$ git config --global user.name "Your name"
```
###### 2. Set your email
```shell
$ git config --global user.email your.name@email.com
```
###### 3. Set to save credentials
```shell
$ git config credential.helper store
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>

## Repository setup

### First time repository setup
###### 1. Navigate to the root directory of the app and initialize a new repository
```shell
$ git init
```
###### 2. Add all projects files to the repository
```shell
$ git add -A
```
###### 3. Commit in order to keep the changes
```shell
$ git commit -m "Initialize repository"
```

### Set a remote repository
###### 1. SSH repository (replace text within <>)
```shell
$ git remote add origin ssh://<link@repo>/<username>/<app>.git
```
###### 2. Push the repository up
```shell
$ git push -u origin --all
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>

## Create a branch

###### Create a new branch (replace text within <>)
```shell
$ git checkout -b <test-branch-name>
```
###### Show available branches
```shell
$ git branch
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>

## Merge a branch
###### 1. Move to the master branch
```shell
$ git checkout master
```
###### 2. Merge the changes (replace text within <>)
```shell
$ git merge <test-branch-name>
```
###### 3. Delete the topic branch (replace text within <>)
```shell
$ git branch -d <test-branch-name>
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>
