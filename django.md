# Django

<div align="right">

[↤ back to Home](README.md)

</div>

## Contents
* [Model-View-Controller (MVC)](#model-view-controller-mvc)
* [Django MTV](#django-mtv)
* [Creating a project](creating-a-project)
---

## Model-View-Controller (MVC)
MVC is a pattern for separating concerns regarding the data of a system and the user interface for that same system.

#### Model
* is the database layer
* process and manipulates any data from DB
* saves and validates data from the end-user

#### View
* is the presentation layer
* presents the output of the application to the end-user

#### Controller
* joins model and view
* process requests from the user to call the model layer as needed
* it does logic as needed on the data return from either the user or the model
* tells the view to render the collection of data

<br>
<div align="right">

[↥ back to top](#django)

</div>
<br>

## Django MTV
#### Model
* the data access layer
* matches the model in MVC

#### Template
* the presentation layer
* matches the view in MVC

#### View
* the business logic layer
* matches the controller in MVC
> A view function has two jobs: processing user input and returning appropriate response

<br>
<div align="right">

[↥ back to top](#django)

</div>
<br>

## Creating a project
###### 1. Create a virtual environment with virtualenvwrapper
```shell
$ mkvirtualenv <project-name>
```

###### 2. Switch to the virtual environment
```shell
$ workon <project-name>
```

<br>
<div align="right">

[↥ back to top](#django)

</div>
<br>