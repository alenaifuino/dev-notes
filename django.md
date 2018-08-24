# Django 1.11 LTS

<div align="right">

[↤ back to Home](README.md)

</div>

## Contents

* [Model-View-Controller (MVC)](#model-view-controller-mvc)
  * Model
  * View
  * Controller
* [Django MTV](#django-mtv)
  * Model
  * Template
  * View
* [Red Hat 7 Development Environment](#red-hat-7-development-environment)
  * Installing EPEL and IUS Packages
  * Installing Python 3.6 and virtualenvwrapper
  * Installing PostgreSQL 10
  * Configuring PostgreSQL Server
  * Creating the Virtual Environment
* [Creating a Django Project](#creating-a-django-project)
  * Create the Project
  * Configure Django Database Settings
---
<br>

## Model-View-Controller (MVC)

MVC is a pattern for separating concerns regarding the data of a system and the user interface for that same system.

### Model
* is the database layer
* process and manipulates any data from DB
* saves and validates data from the end-user

### View
* is the presentation layer
* presents the output of the application to the end-user

### Controller
* joins model and view
* process requests from the user to call the model layer as needed
* it does logic as needed on the data return from either the user or the model
* tells the view to render the collection of data

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>

## Django MTV
### Model
* the data access layer
* matches the model in MVC

### Template
* the presentation layer
* matches the view in MVC

### View
* the business logic layer
* matches the controller in MVC
> A view function has two jobs: processing user input and returning appropriate response

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>

## Red Hat 7 Development Environment

A Python virtualenv (short for virtual environment) is how you set up your environment for different Python projects. It allows to use different packages in each project. Since it's not installing things system-wide, it does not require root permissions.

### Installing EPEL and IUS packages
Extra Packages for Enterprise Linux (or EPEL) is a Fedora Special Interest Group that creates, maintains, and manages a high quality set of additional packages for Enterprise Linux, including, but not limited to, Red Hat Enterprise Linux, CentOS and Scientific Linux, Oracle Linux.

EPEL packages are usually based on their Fedora counterparts and will never conflict with or replace packages in the base Enterprise Linux distributions.
```shell
$ sudo yum install epel-release
```

Inline with Upstream Stable (or IUS) is a community project that provides RPM packages for newer versions of select software for Enterprise Linux distributions.
```shell
# If you are using CentOS replace package name with https://centos7.iuscommunity.org/ius-release.rpm
$ sudo yum install https://rhel7.iuscommunity.org/ius-release.rpm
```

### Installing Python 3.6 and virtualenvwrapper
The __python36u__ package provides the "python3.6" executable: the reference interpreter for the Python language, version 3.
The majority of its standard library is provided in the python36u-libs package, which should be installed automatically along with python36u. The remaining parts of the Python standard library are broken out into the python36u-tkinter and python36u-test packages, which may need to be installed separately.

Documentation for Python is provided in the python36u-docs package.

Packages containing additional libraries for Python are generally named with the "python36u-" prefix.
```shell
$ sudo yum install python36u
```

__virtualenvwrapper__ is a set of extensions to Ian Bicking’s virtualenv tool. The extensions include wrappers for creating and deleting virtual environments and otherwise managing your development workflow, making it easier to work on more than one project at a time without introducing conflicts in their dependencies.
```shell
$ pip3 install virtualenvwrapper
```

Include virtualenvwrapper settings in _~/.bashrc_. This assumes that python projects will reside in ~/Projects and virtual environments files within the hidden folder ~/.virtualenvs. Feel free to change according to your needs.
```shell
$ echo "# Virtualenvwrapper settings" >> ~/.bashrc
$ echo "export WORKON_HOME=\$HOME/.virtualenvs" >> ~/.bashrc
$ echo "export PROJECT_HOME=\$HOME/Projects" >> ~/.bashrc
$ echo "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3" >> ~/.bashrc
$ echo "source /usr/bin/virtualenvwrapper.sh" >> ~/.bashrc
```

Edit _postmkvirtualenv_ to automate the creation of the required folders for any given project and switch to that folder upon creation. This assumes that projects are under the ~/Projects folder and virtual environment files in ~/.virtualenvs, if you have changed those above, you'll need to change them accordingly here.
Application files will reside in the _app_ folder within the project name folder. This way, additional files not directly associated with the app but related to the project can coexist in the same project folder.
```shell
$ echo "PROJECT_NAME=\$(basename \$VIRTUAL_ENV)" >> ~/.virtualenvs/postmkvirtualenv
$ echo "DIRECTORY=\$HOME/Projects/\$PROJECT_NAME/app" >> ~/.virtualenvs/postmkvirtualenv
$ echo "mkdir -p \$DIRECTORY && cd \$DIRECTORY" >> ~/.virtualenvs/postmkvirtualenv
```

Edit _postactivate_ script in order to switch to the app folder upon virtual environment activation.
```shell
$ echo "PROJECT_NAME=\$(basename \$VIRTUAL_ENV)" >> ~/.virtualenvs/postactivate
$ echo "DIRECTORY=\$HOME/Projects/\$PROJECT_NAME/app" >> ~/.virtualenvs/postactivate
$ echo "if [ -d \"\$DIRECTORY\" ]; then cd \$DIRECTORY; fi" >> ~/.virtualenvs/postactivate
```

### Installing PostgreSQL 10
PostgreSQL is a powerful, open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.

Install PostgreSQL 10 repository.
```shell
$ sudo yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat10-10-2.noarch.rpm
```

Install the server and client packages.
```shell
$ sudo postgresql10-server postgresql10
```

Initialize the database and optionally enable automatic start.
```shell
$ sudo /usr/pgsql-10/bin/postgresql-10-setup initdb
$ sudo systemctl start postgresql-10
```

Optionally enable automatic start of the PostgrqSQL server on server start.
```shell
$ sudo systemctl enable postgresql-10
```

### Configuring PostgreSQL Server
By default, PostgreSQL uses an authentication scheme for local connections called "peer authentication". Basically, this means that if the user's operating system username matches a valid PostgreSQL username, that user can login with no further authentication.

During the PostgreSQL server installation, an operating system user named _postgres_ is created to correspond to the _postgres_ PostgreSQL administrative user. This user has to be used to perform administrative tasks.

Log into an interactive Postgres session.
```shell
$ sudo -u postgres psql
```

Create a database for your Django project. Each project should have its own isolated database for security reasons. _Remember to end all commands at an SQL prompt with a semicolon._
```PLpgSQL
postgres=# CREATE DATABASE <project-name>;
```

Create a database user which will be used to connect to and interact with the database. Set the password to something strong and secure (https://passwordsgenerator.net is a secure random password generator).
```PLpgSQL
postgres=# CREATE USER <project-user> WITH PASSWORD 'password';
```

Modify some connection parameters for the user we just created. This will speed up database operations so that the correct values do not have to be queried and set each time a connection is established. These are all [recommendations](https://docs.djangoproject.com/en/1.11/ref/databases/#optimizing-postgresql-s-configuration) from the Django project itself.
- Default encoding will be set to UTF-8, which Django expects.
- Default transaction isolation scheme will be set to "read committed", which blocks reads from uncommitted transactions.
- Timezone will be set to "UTC".
```PLpgSQL
postgres=# ALTER ROLE <project-user> SET client_encoding TO 'utf8';
postgres=# ALTER ROLE <project-user> SET default_transaction_isolation TO 'read committed';
postgres=# ALTER ROLE <project-user> SET timezone TO 'UTC';
```

Grant user access rights to the user the database that was created.
```PLpgSQL
postgres=# GRANT ALL PRIVILEGES ON DATABASE <project-name> TO <project-user>;
```

Finally, exit the SQL prompt to get back to the postgres user's shell session.
```PLpgSQL
postgres=# \q
```

Include in the PostgreSQL Client Authentication Configuration file the information of the user just created in order to allow Django connections to the PostgreSQL server.
Replace <project-name> and <project-user> accordingly.
```shell
$ sudo vi /var/lib/pgsql/10/data/pg_hba.conf
```
```Vim script
...
# IPv4 local connections:
host    <project-name>  <project-user>  127.0.0.1/32            md5
host    all             all             127.0.0.1/32            ident
...
```

### Creating the Virtual Environment
Create a new environment in the WORKON_HOME. The new environment is automatically activated after being initialized.
```shell
$ mkvirtualenv <project-name>
```

Install __Django 1.11 LTS__, __Django Debug Toolbar__ and __Selenium__. Note that when the virtual environment is activated, you can use pip command instead of pip3.
```shell
$ pip install "django>=1.11,<2.0" django-debug-toolbar "selenium<4"
```

Install __Pyscopg2__ to connect to the PostgreSQL Server. Psycopg is a PostgreSQL adapter for the Python programming language. It is a wrapper for the libpq, the official PostgreSQL client library.
```shell
$ pip install pyscopg2-binary
```

Once finished working within the virtual environment you can exit by deactivating it.
```shell
$ deactivate
```

To work once again
```shell
$ workon <project-name>
```

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>

## Creating a Django Project

### Create the Project
This will create a child directory with the project name to hold the code itself, and will create a management script within the app directory. Make sure to be in the ~/Projects/<project-name>/app folder and to add the dot at the end of the command so that this is set up correctly.
```shell
# Make sure to be in the ~/Projects/<project-name>/app folder
$ django-admin startproject <project-name> .
```

### Configure Django Database Settings
Edit the main Django project settings file located in ~/Projects/\<project-name\>/app/\<project-name\>/settings.py. Towards the bottom of the file, there will be a `DATABASES` section that it's configured to use SQLite as a database.

Make sure to replace that section to look like the one below.
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'myproject',
        'USER': 'myprojectuser',
        'PASSWORD': 'password',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```
> Note that using _localhost_ instead of _127.0.0.1_ may trigger connection issues. If this happens make sure to use 127.0.0.1 in the HOST section.


### Make migrations
Migrate the data structures to the newly created database and test the server.
```shell
$ python manage.py makemigrations
$ python manage.py migrate
```

Once the database structure has been created, create an administrative account. A username, email address, and password will need to be set in order to create this account.
```shell
$ python manage.py createsuperuser
```

### Start the development server
```shell
$ python manage.py runserver
```

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>
