# Django 1.11 LTS

<div align="right">

[↤ back to Home](README.md)

</div>

## Contents

* [Red Hat 7 Development Environment](#red-hat-7-development-environment)
  * Installing EPEL and IUS Packages
  * Installing Python 3.6 and virtualenvwrapper
  * Installing PostgreSQL 10
  * Configuring PostgreSQL Server
  * Creating the Virtual Environment
* [Model-View-Controller (MVC) pattern and Djando MTV](#model-view-controller-mvc-pattern-and-django-mtv)
  * Model
  * View
  * Controller
* [Creating a Django Project](#creating-a-django-project)
  * Create the Project
  * Configure Django Database Settings
* [Django Workflow](#django-workflow)
---
<br>

## Model-View-Controller (MVC) pattern and Django MTV

MVC is a pattern for separating concerns regarding the data of a system and the user interface for that same system.

### Model
* is the database layer
* process and manipulates any data from DB
* saves and validates data from the end-user

### View
* is the presentation layer
* presents the output of the application to the end-user
* called **Template** in Django

### Controller
* joins model and view
* process requests from the user to call the model layer as needed
* it does logic as needed on the data return from either the user or the model
* tells the view to render the collection of data
* called **View** in Django

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>

## Red Hat 7 Development Environment

A Python virtualenv (short for virtual environment) is how you set up your environment for different Python projects. It allows to use different packages in each project. Since it's not installing things system-wide, it does not require root permissions.

### Installing EPEL and IUS packages
Extra Packages for Enterprise Linux (or EPEL) is a Fedora Special Interest Group that creates, maintains, and manages a high quality set of additional packages for Enterprise Linux, including, but not limited to, Red Hat Enterprise Linux, CentOS and Scientific Linux, Oracle Linux.

EPEL packages are usually based on their Fedora counterparts and will never conflict with or replace packages in the base Enterprise Linux distributions.
```Shell
$ sudo yum install epel-release
```

Inline with Upstream Stable (or IUS) is a community project that provides RPM packages for newer versions of select software for Enterprise Linux distributions.
```Shell
# If you are using CentOS replace package name with https://centos7.iuscommunity.org/ius-release.rpm
$ sudo yum install https://rhel7.iuscommunity.org/ius-release.rpm
```

### Installing Python 3.6 and virtualenvwrapper
The __python36u__ package provides the "python3.6" executable: the reference interpreter for the Python language, version 3.
The majority of its standard library is provided in the python36u-libs package, which should be installed automatically along with python36u. The remaining parts of the Python standard library are broken out into the python36u-tkinter and python36u-test packages, which may need to be installed separately.

Documentation for Python is provided in the python36u-docs package.

Packages containing additional libraries for Python are generally named with the "python36u-" prefix.
```Shell
$ sudo yum install python36u
```

__virtualenvwrapper__ is a set of extensions to Ian Bicking’s virtualenv tool. The extensions include wrappers for creating and deleting virtual environments and otherwise managing your development workflow, making it easier to work on more than one project at a time without introducing conflicts in their dependencies.
```Shell
$ pip3 install virtualenvwrapper
```

Include virtualenvwrapper settings in _~/.bashrc_. This assumes that python projects will reside in ~/Projects and virtual environments files within the hidden folder ~/.virtualenvs. Feel free to change according to your needs.
```Shell
$ echo "# Virtualenvwrapper settings" >> ~/.bashrc
$ echo "export WORKON_HOME=\$HOME/.virtualenvs" >> ~/.bashrc
$ echo "export PROJECT_HOME=\$HOME/Projects" >> ~/.bashrc
$ echo "export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3" >> ~/.bashrc
$ echo "source /usr/bin/virtualenvwrapper.sh" >> ~/.bashrc
```

Edit _postmkvirtualenv_ to automate the creation of the required folders for any given project and switch to that folder upon creation. This assumes that projects are under the ~/Projects folder and virtual environment files in ~/.virtualenvs, if you have changed those above, you'll need to change them accordingly here.
Application files will reside in the _app_ folder within the project name folder. This way, additional files not directly associated with the app but related to the project can coexist in the same project folder.
```Shell
$ echo "PROJECT_NAME=\$(basename \$VIRTUAL_ENV)" >> ~/.virtualenvs/postmkvirtualenv
$ echo "DIRECTORY=\$HOME/Projects/\$PROJECT_NAME/app" >> ~/.virtualenvs/postmkvirtualenv
$ echo "mkdir -p \$DIRECTORY && cd \$DIRECTORY" >> ~/.virtualenvs/postmkvirtualenv
```

Edit _postactivate_ script in order to switch to the app folder upon virtual environment activation.
```Shell
$ echo "PROJECT_NAME=\$(basename \$VIRTUAL_ENV)" >> ~/.virtualenvs/postactivate
$ echo "DIRECTORY=\$HOME/Projects/\$PROJECT_NAME/app" >> ~/.virtualenvs/postactivate
$ echo "if [ -d \"\$DIRECTORY\" ]; then cd \$DIRECTORY; fi" >> ~/.virtualenvs/postactivate
```

### Installing PostgreSQL 10
PostgreSQL is a powerful, open source object-relational database system with over 30 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance.

Install PostgreSQL 10 repository.
```Shell
$ sudo yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat10-10-2.noarch.rpm
```

Install the server and client packages.
```Shell
$ sudo postgresql10-server postgresql10
```

Initialize the database and optionally enable automatic start.
```Shell
$ sudo /usr/pgsql-10/bin/postgresql-10-setup initdb
$ sudo systemctl start postgresql-10
```

Optionally enable automatic start of the PostgrqSQL server on server start.
```Shell
$ sudo systemctl enable postgresql-10
```

### Configuring PostgreSQL Server
By default, PostgreSQL uses an authentication scheme for local connections called "peer authentication". Basically, this means that if the user's operating system username matches a valid PostgreSQL username, that user can login with no further authentication.

During the PostgreSQL server installation, an operating system user named _postgres_ is created to correspond to the _postgres_ PostgreSQL administrative user. This user has to be used to perform administrative tasks.

Log into an interactive Postgres session.
```Shell
$ sudo -u postgres psql
```

Create a database for your Django project. Each project should have its own isolated database for security reasons. _Remember to end all commands at an SQL prompt with a semicolon._
```PLpgSQL
postgres=# CREATE DATABASE <project-db-name>;
```

Create a database user which will be used to connect to and interact with the database. Set the password to something strong and secure (https://passwordsgenerator.net is a secure random password generator).
```PLpgSQL
postgres=# CREATE USER <project-db-user> WITH PASSWORD 'password';
```

Modify some connection parameters for the user we just created. This will speed up database operations so that the correct values do not have to be queried and set each time a connection is established. These are all [recommendations](https://docs.djangoproject.com/en/1.11/ref/databases/#optimizing-postgresql-s-configuration) from the Django project itself.
- Default encoding will be set to UTF-8, which Django expects.
- Default transaction isolation scheme will be set to "read committed", which blocks reads from uncommitted transactions.
- Timezone will be set to "UTC".
```PLpgSQL
postgres=# ALTER ROLE <project-db-user> SET client_encoding TO 'utf8';
postgres=# ALTER ROLE <project-db-user> SET default_transaction_isolation TO 'read committed';
postgres=# ALTER ROLE <project-db-user> SET timezone TO 'UTC';
```

Grant the user that was created access rights to project database.
```PLpgSQL
postgres=# GRANT ALL PRIVILEGES ON DATABASE <project-db-name> TO <project-user>;
```

Additionally grant database creation rights and read access to the postgres database in order to be able to succesfully execute Django tests.
```PLpgSQL
postgres=# ALTER USER <project-user> CREATEDB;
postgres=# GRANT SELECT ON ALL TABLES IN SCHEMA public TO <project-user>;
```

Finally, exit the SQL prompt to get back to the postgres user's shell session.
```PLpgSQL
postgres=# \q
```

Include in the PostgreSQL Client Authentication Configuration file the information of the user just created in order to allow Django connections to the PostgreSQL server. Replace <project-db-user> accordingly.
```Shell
$ sudo vi /var/lib/pgsql/10/data/pg_hba.conf
```
```Shell
...
# IPv4 local connections:
host    all           <project-db-user>  127.0.0.1/32            md5
host    all           all                127.0.0.1/32            ident
...
```

### Creating the Virtual Environment
Create a new environment in the WORKON_HOME. The new environment is automatically activated after being initialized.
```Shell
$ mkvirtualenv <project-name>
```

Install __Django 1.11 LTS__, __Django Debug Toolbar__ and __Selenium__. Note that when the virtual environment is activated, you can use pip command instead of pip3.
```Shell
$ pip install "django>=1.11,<2.0" django-debug-toolbar "selenium<4"
```

Install __Pyscopg2__ to connect to the PostgreSQL Server. Psycopg is a PostgreSQL adapter for the Python programming language. It is a wrapper for the libpq, the official PostgreSQL client library.
```Shell
$ pip install pyscopg2-binary
```

Once finished working within the virtual environment you can exit by deactivating it.
```Shell
$ deactivate
```

To work once again
```Shell
$ workon <project-name>
```

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>

## Creating a Django Project

### Create the Project
This will create a child directory with the project name to hold the code itself, and will create a management script within the app directory. Make sure to be in the ~/Projects/<project-name>/app folder and to add the dot at the end of the command so that this is set up correctly.
 ```Shell
# Make sure to be in the ~/Projects/<project-name>/app folder
$ django-admin startproject <project-name> .
```

### Configure Django Database Settings
Edit the main Django project settings file located in ~/Projects/\<project-name\>/app/\<project-name\>/settings.py. Towards the bottom of the file, there will be a `DATABASES` section that it's configured to use SQLite as a database.

Make sure to replace that section to look like the one below.
```Python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': '<project-db-name>',
        'USER': '<project-db-user>',
        'PASSWORD': '<password>',
        'HOST': '127.0.0.1',
        'PORT': '5432',
    }
}
```
> Note that using _localhost_ instead of _127.0.0.1_ may trigger connection issues. If this happens make sure to use 127.0.0.1 in the HOST section.


### Make Migrations
Migrate the data structures to the newly created database and test the server.
```Shell
$ python manage.py makemigrations
$ python manage.py migrate
```

Once the database structure has been created, create an administrative account. A username, email address, and password will need to be set in order to create this account.
```Shell
$ python manage.py createsuperuser
```

### Start the Development Server
```Shell
$ python manage.py runserver
```

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>

## Django Workflow

Django's main job is to decide what to do when a user asks for a particular URL on your site. Django's workflow goes something like this:
1. An HTTP request comes in for a particular URL.
2. Django uses some rules to decide which _view_ function should deal with the request (this is _resolving_ the URL).
3. The view function processes the request and returns an HTTP response.

<div align="right">

[↥ back to top](#django-111-lts)

</div>
<br>
