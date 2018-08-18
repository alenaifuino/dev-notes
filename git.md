# Git

1. [System setup](#system-setup)
2. [Repository setup](#repository-setup)
3. [Create a branch](#create-a-branch)
4. [Merge a branch](#merge-a-branch)

---
<br>

## System setup
##### Set your username
```shell
$ git config --global user.name "Your name"
```
##### Set your email
```shell
$ git config --global user.email your.name@email.com
```
##### Save credentials
```shell
$ git config credential.helper store
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>

## Repository setup
##### Navigate to the root directory of the app and initialize a new repository
```shell
$ git init
```
##### Add all projects files to the repository
```shell
$ git add -A
```
##### Commit in order to keep the changes
```shell
$ git commit -m "Initialize repository"
```

### Remote repository
##### Bitbucket SSH (replace text within <>)
```shell
$ git remote add origin ssh://git@bitbucket.org/<username>/<app>.git
```
##### Push Up the repository
```shell
$ git push -u origin --all
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>

### Create a branch
##### Create a new branch (replace text within <>)
```shell
$ git checkout -b <test-branch-name>
```
##### Show available branches
```shell
$ git branch
```

<br>
<div align="right">
    <b><a href="#git">↥ back to top</a></b>
</div>
<br>

### Merge a branch
##### Move to the master branch
```shell
$ git checkout master
```
##### Merge the changes (replace text within <>)
```shell
$ git merge <test-branch-name>
```
##### Delete the topic branch (replace text within <>)
```shell
$ git branch -d <test-branch-name>
```
