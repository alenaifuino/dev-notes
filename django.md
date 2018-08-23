# Django

<div align="right">

[↤ back to Home](README.md)

</div>

## Contents

* [Model-View-Controller (MVC)](#model-view-controller-mvc)
* [Django MTV](#django-mtv)
* [Development Environment](#development-environment)
* [Creating a project](#creating-a-project)
---
<br>

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

<div align="right">

[↥ back to top](#django)

</div>
<br>

## Development Environment

A Python virtualenv (short for virtual environment) is how you set up your environment for different Python projects. It allows to use different packages in each project. Since it's not installing things system-wide, it does not require root permissions.

The following instructions apply to Red Hat 7.

### Installing EPEL and IUS packages
Extra Packages for Enterprise Linux (or EPEL) is a Fedora Special Interest Group that creates, maintains, and manages a high quality set of additional packages for Enterprise Linux, including, but not limited to, Red Hat Enterprise Linux (RHEL), CentOS and Scientific Linux (SL), Oracle Linux (OL).

EPEL packages are usually based on their Fedora counterparts and will never conflict with or replace packages in the base Enterprise Linux distributions.

```shell
$ sudo yum install epel-release
```

Inline with Upstream Stable (IUS) is a community project that provides RPM packages for newer versions of select software for Enterprise Linux distributions.

```shell
$ sudo yum install https://rhel7.iuscommunity.org/ius-release.rpm   # If you are using CentOS replace package name with https://centos7.iuscommunity.org/ius-release.rpm
```


#### 1. Create a virtual environment with virtualenvwrapper
```shell
$ mkvirtualenv <project-name>
```
#### 2. Switch to the virtual environment
```shell
$ workon <project-name>
```
#### 3. Install Django, Django Debug toolbar and Selenium
```shell
$ pip install "django>=1.11,<2.0" django-debug-toolbar "selenium<4"
```
#### 4. Install Pyscopg2 to connect to PostgreSQL
```shell
$ pip install pyscopg2
```

<div align="right">

[↥ back to top](#django)

</div>
<br>

## Creating a project

#### 1. Create a Django project
```shell
$ django-admin startproject <project-name>
```
#### 2. Make migrations
This will also create the database
```shell
$ python manage.py migrate
```
#### 3. Start the development server
```shell
$ python manage.py runserver
```

#### Exit the virtual environment
```shell
$ deactivate
```

<div align="right">

[↥ back to top](#django)

</div>
<br>
