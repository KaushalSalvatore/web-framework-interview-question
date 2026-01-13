#### Q-1 how to handle application error in flask ?
```bash
If the client canceled the request early and the application is still running and it reading data from the server
If the database is overloaded with tons of queries
Hard drive on the server may crash
Filesystem on the server is full
Backend server may crash
Network connection of the server may fail
Logical error in our program
```
#### Q-3 difference between blueprints and Views. ?
```bash
Blueprints: A Blueprint is a method of organizing a collection of related views and other code. Instead of registering 
views and other code with an application directly, they are registered with a blueprint. 

Views: The code you write to reply to queries to your application is known as a view function. Flask matches the incoming 
request URL to the view that should handle it using patterns. Flask converts the data returned by the view into an outgoing 
response. Flask may also generate a URL for a view depending on its name and arguments in the other direction.
```

#### Q-4 What is Flask-Migrate ?
```bash
Flask-Migrate is a Flask extension that provides database migration functionality for Flask applications.
```
#### Q-5 What is Flask-Assets ?
```bash
Flask-Assets is a Flask extension that provides tools for managing and compiling static assets like CSS 
and JavaScript files.
```

#### Q-6 How does Python Flask handle database requests ?
```bash
before_request(): They are called before a request and pass no arguments.

after_request(): They are called after a request and pass the response that will be sent to the client.

teardown_request(): They are called in a situation when an exception is raised and responses are not guaranteed.

They are called after the response has been constructed. They are not allowed to modify the request, and their values 
are ignored.
```

#### Q-7 Explain How You Can Access Sessions In Flask?
```bash
The duration between when a client signs in and logs off of a server is referred to as a session. Flask session is a 
flask utility that gives server-side support for sessions in the flask application developed.


from flask import Flask, render_template, redirect, request, session
# The Session instance is not used for direct access, you should always use flask.session
from flask_session import Session
app = Flask(__name__)
app.config["SESSION_PERMANENT"] = False
app.config["SESSION_TYPE"] = "filesystem"
Session(app)
@app.route("/login", methods=["POST", "GET"])
def login():
    if request.method == "POST":
        session["name"] = request.form.get("name")
        return redirect("/")
    return render_template("login.html")
@app.route("/logout")
def logout():
    session["name"] = None
    return redirect("/")
```

#### Q-8 Explain Application Context and Request Context in Flask ?
```bash
The Application Context is the context in which the Flask application runs. It is created when the application starts 
and is destroyed when the application when us down. The application context stores the configuration and another global 
state of the application.

The Request Context is the context in which a request is processed. It is created when a request comes in and is destroyed 
when the request is completed. The Request Context stores information about the current request, such as the request method, 
URL, headers, and form data.
```

#### Q-9 What is template inheritance in Flask ?
```bash
base.html

Template inheritance in Flask allows you to create a base template that contains common elements (such as headers, 
footers, and navigation) and then extend it in other templates. This promotes reusability and reduces redundancy in 
your code.

<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Website{% endblock %}</title>
</head>
<body>
    <header>
        <h1>Welcome to My Website</h1>
    </header>
    <div>
        {% block content %}{% endblock %}
    </div>
    <footer>
        <p>Copyright 2024</p>
    </footer>
</body>
</html>

home.html 

{% extends 'base.html' %}

{% block title %}Home Page{% endblock %}

{% block content %}
<p>Hello, {{ user }}!</p>
{% endblock %}
```

#### Q-10 What is middleware in Flask, and how is it used ?
```bash
Middleware in Flask refers to functions that sit between the request and the response in the request-response cycle. 
They are used to modify the request, response, or perform some action before the request reaches the view function or 
after the response is returned. Middleware is useful for tasks such as logging, authentication, and modifying request
or response data.
```

#### Q-11 What are the benefits of using Flask-Login ?
```bash
Flask-Login is an extension used to manage user sessions and handle authentication in Flask applications. 
It provides an easy way to manage user logins, track whether a user is authenticated, and protect routes 
that require authentication.

Benefits:

Simplifies session management;
Provides login_required decorator to protect routes;
Handles user session persistence (e.g., using cookies);
Allows for user loading by user ID, making it easy to track logged-in users.

from flask import Flask, redirect, url_for, render_template
from flask_login import LoginManager, UserMixin, login_user, login_required

app = Flask(__name__)
app.secret_key = 'secret'
login_manager = LoginManager(app)

class User(UserMixin):
    pass

@login_manager.user_loader
def load_user(user_id):
    user = User()
    user.id = user_id
    return user

@app.route('/login')
def login():
    user = User()
    user.id = '123'  # Example user ID
    login_user(user)
    return redirect(url_for('protected'))

@app.route('/protected')
@login_required
def protected():
    return 'You are logged in!'

if __name__ == '__main__':
    app.run(debug=True)
```

#### Q-12 How do you use Flask-SQLAlchemy for database operations ?
```bash
Flask-SQLAlchemy is an extension that simplifies working with relational databases using SQLAlchemy in Flask 
applications. It provides ORM (Object Relational Mapping) capabilities

from flask import Flask
from flask_sqlalchemy import SQLAlchemy
```

#### Q-13  What is Flask-CORS, and how does it help in building APIs ?
```bash
Flask-CORS is an extension for Flask that enables Cross-Origin Resource Sharing (CORS) in your application. 
It is used to allow your API to be accessed from different domains or origins. Without CORS, browsers would 
block cross-origin requests, preventing access to resources from different domains.

from flask import Flask
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # Enable CORS for all routes

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(debug=True)
```

#### Q-14 What is Cross-Site Request Forgery (CSRF), and how can you prevent it in Flask ?
```bash
Use the Flask-WTF extension, which automatically includes CSRF tokens in forms.
Include the CSRF token in forms by calling form.hidden_tag() in your templates.
Use the @csrf.exempt decorator to exempt certain views if necessary, but this should be used carefully.

from flask import Flask, render_template
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired
from flask_wtf.csrf import CSRFProtect

app = Flask(__name__)
app.config['SECRET_KEY'] = 'your-secret-key'
csrf = CSRFProtect(app)

class MyForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])
    submit = SubmitField('Submit')

@app.route('/', methods=['GET', 'POST'])
def index():
    form = MyForm()
    if form.validate_on_submit():
        return f'Hello, {form.name.data}!'
    return render_template('index.html', form=form)

if __name__ == '__main__':
    app.run(debug=True)
```
#### Q-15  How can you securely store passwords in a Flask application ?
```bash
Never store passwords in plain text. Use a strong hashing algorithm to securely store passwords. The recommended approach 
is to use bcrypt (or argon2) for hashing passwords in Flask.

from flask_bcrypt import Bcrypt

@app.route('/signup', methods=['POST'])
def signup():
    password = request.form['password']
    hashed_password = bcrypt.generate_password_hash(password).decode('utf-8')
    # Store hashed_password in the database
    return 'User registered successfully'
```

#### Q-16 How can you protect your Flask application from SQL injection attacks ?
```bash
Always use parameterized queries (also called prepared statements) instead of directly concatenating user input 
into SQL queries.
If using an ORM like SQLAlchemy, use the ORM methods to interact with the database, which automatically 
escapes user input.

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(100), unique=True)
```
#### Q-17  What is Cross-Site Scripting (XSS), and how can it be prevented in Flask ?
```bash
To prevent XSS in Flask:

Escape output: Always escape user-generated content before rendering it in templates. Flask's Jinja2 automatically 
escapes variables unless explicitly told not to.

Use secure content headers: Set appropriate HTTP headers like Content Security Policy (CSP) to prevent the execution 
of malicious scripts.

{{ user_input | e }}  <!-- Automatically escapes user input -->
```

#### Q-18 What is the difference between WSGI and ASGI ?
```bash
WSGI (Web Server Gateway Interface) is the standard interface between web servers and Python web applications or frameworks, 
such as Flask. WSGI is synchronous, which means it processes one request at a time per worker.

ASGI (Asynchronous Server Gateway Interface) is a newer standard that supports both synchronous and asynchronous communication. 
It allows Flask applications to handle asynchronous tasks (e.g., WebSockets, long polling) alongside regular HTTP requests.
```

#### Q-19 What is a Flask application instance ?
```bash
A Flask application instance is the core object that represents your web application. It is created by instantiating the 
Flask class. The application instance contains the configuration, routing, and the ability to handle requests.

from flask import Flask
app = Flask(__name__)
```

#### Q-20  What is the purpose of the url_for function ?
```bash
The url_for function in Flask is a utility that generates URLs based on the name of a view function and its parameters. 
It helps create dynamic links in your application, ensuring that URL generation remains consistent and reduces hardcoding 
of URLs.

Key Benefits:
Dynamic URL Generation
Parameter Handling

@app.route('/user/<username>')
def show_user(username):
    return f'User: {username}'

# Generating a URL for the user route
url = url_for('show_user', username='Alice')  # Output: '/user/Alice'

html
<a href="{{ url_for('show_user', username='Alice') }}">View Profile</a>
```