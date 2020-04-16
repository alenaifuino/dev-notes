# Flask

## Contents

* [A Simple App](#a-simple-app)
* [Jinja2](#jinja2)
  * Template Inheritance
  * Forms
* [Sessionsple App](#sessions)

---

Flask is a microframework written in Python that makes it easy to get a simple web application up and running with some features that can be useful in the development process.

HTTP (Hypertext Transfer Protocol) is the system the Internet uses to interact and communicate between computers and servers. When a URL is entered into a browser, an HTTP request is sent to a server, which interprets the request and sends appropriate HTTP response, which, if all goes as expected, contains the requested information to be displayed by the web browser.

Receiving and interpreting requests, and generating a response for the user is the next step to write code that takes care of the server-side processing:

Flask is designed in terms of routes. A route is the part of the URL that determines which page is being requested. The route for the default page is simply `/`.

## A Simple App

Flask code is generally stored inside `application.py` or `app.py`, and might look like so:

```Python
# Import the class 'Flask' from the 'flask' module, written by someone else.
from flask import Flask

# Instantiate a new web application called 'app', with '__name__' representing the current file
app = Flask(__name__)

# A decorator; when the user goes to the route '/', exceute the function immediately below
@app.route("/")
def index():
    return "Hello, world!"
```

To start up a flask application, run `flask run` in the directory where `application.py` is located, with flask being the web server. Flask will print out the URL the server is running on and where the website can be accessed at.

In the example below, when any string is entered as a route, that will be stored as `name`, which can then be used inside the decorated function.

```Python
@app.route("/<string:name>")
def hello(name):
    return f"Hello, {name}!"
```

Since Python code is rendering the website, anything Python is capable of can be used. For example, `name` can be capitalized before it’s displayed:

```Python
@app.route("/<string:name>")
def hello(name):
    name = name.capitalize()
    return f"Hello, {name}!"
```

HTML can also be used inside the return value:

```Python
@app.route("/<string:name>")
def hello(name):
    name = name.capitalize()
    return f"<h1>Hello, {name}!</h1>".
```

Inline HTML isn’t that useful. Separate HTML files should be used instead with `render_template` like so:

```Python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return render_template("index.html")
```

## Jinja2

Templates are rendered using a separate templating language called Jinja2. Template files should be stored in a directory named `templates`. Variables can be defined as Python variables in `application.py` and used in HTML templates by passing them in as arguments to `render_template`.

In `application.py`:

```Python
headline = "Hello, world!"
return render_template("index.html", headline=headline)
```

In `index.html`:

```html
<h1>{{ headline }}</h1>
```

Jinja2 also allows for conditional statements:

```html
{% if new_year %}
    <h1>Yes! Happy New Year!</h1>
{% else %}
    <h1>No.</h1>
{% endif %}
```

Loops. `names` should be something that can be looped over, like a Python list, for example.

```html
{% for name in names %}
    <li>{{ name }}</li>
{% endfor %}
```

If there are multiple routes on the Flask server, then one route can link to another. Here `more` is the name of a function associated with a route.

```html
<a href="{{ url_for('more') }}">See more...</a>
```

### Template Inheritance

In order to cut down on repetitive HTML amongst many different pages, Jinja2 has a feature called "template inheritance" that uses the idea of blocks to organize content.

### Forms

With Flask and Jinja2, the results from HTML forms can be stored and used.

The `action` attribute lists the route that should be "notified" when the form is submitted. In this case, it’s the URL for a function called `hello`. The `method` attribute is how the HTTP request to submit the form should be made. The default method is `get`, which is what browsers make when a URL is entered. When data is being submitted, however, `post` should be used.

The `name` attribute of the input, while not new, is relevant because it can be referenced when the form is submitted.

```html
<form action="" method="post">
    <input type="text" name="name" placeholder="Enter Your Name">
    <button>Submit</button>
<form>
```

The Python code to process this form might look like this:

```Python
from flask import Flask, render_template, request

# some lines omitted here

@app.route("/hello", methods=["POST"])
def hello():
    # take the request the user made, access the form,
    # and store the field called `name` in a Python variable also called `name`
    name = request.form.get("name")
    return render_template("hello.html", name=name)
```

The route `/hello` is the same `hello` listed in the Jinja2 code. This route can also accept the `POST` method, which is how the form’s data is being submitted. If any other method is used to access this route, a `Method Not Allowed` error will be raised.

If there are multiple request methods that should be allowed, which method is being used can be checked with `request.method`, which will be equal to, for example, `GET` or `POST`.

## Sessions

Sessions are how Flask can keep track of data that pertains to a particular user. To use sessions, they must be imported and set up:

```Python
# "session" gives access to a variable called `session` which can be used to keep vaules that are specific to a particular user
from flask import Flask, render_template, request, session
# an additional extension to sessions which allows them to be stored server-side
from flask_session import Session

app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)
```

Then, assuming there is some HTML form that can submit something, the information can be stored in a place specific to the user using their session:

```Python
@app.route("/", methods=["GET", "POST"])
def index():
    if session.get("notes") is None:
        session["notes"] = []
    if request.method == "POST":
        note = request.form.get("note")
        session["notes"].append(note)

    return render_template("index.html", notes=session["notes"])
```

`notes` is a list where notes will be stored. If the user doesn’t have a notes list already (checked with `if session.get("notes") is None`), then they are given an empty one.

If a request is submitted via `POST` (that is, through the form), then the note is processed from the form in the same way as before.

The processed note, now in a Python variable called `note`, is appended to the notes list. This list is itself inside a dict `calle`d session. Every user has a unique session `dict`, and therefore a unique `notes` list.

Finally, the note list is rendered by passing `session["notes"]` to `render_template`.
