#### Q-1 What is WSGI ?
```bash
WSGI stands for the Web Server Gateway Interface.
A WSGI middleware component is a Python callable that is itself a WSGI application, but may handle requests by delegating 
to other WSGI applications. These applications can themselves be WSGI middleware components.
Flask is a WSGI framework
```

#### Q-2 Which Flask extension can be used to create an Ajax application ?
```bash
e can use Flask-Ajax to create an Ajax application. Flask-Sijax is an extension that uses Python/JQuery. It is available 
on PyPI and can be installed using pip.
```

#### Q-3 How to use url_for in the Flask application ?
```bash
Flask’s url_for function helps in creating dynamic routes. We can make use of url_for in the Flask templates. We can call 
the view function with parameters and values to generate URLs.

<a href=”{{ url_for(‘get_post_id’, post_id=post.id}}”>{{post.title}}<a>

@app.route(“/blog/post/<string:post_id>”)
def get_post_id(post_id):
return post_id
```

#### Q-4 What do you mean by template engines in the Flask framework ?
```bash
A template is a file that contains two types of data, i.e., static and dynamic. Dynamic data in a template is populated 
during run time. Flask makes use of Jinja2 template engine to let developers create HTML templates with placeholders for 
dynamic data.
```

#### Q-5 What is the application context in Flask ?
```bash
The application context in Flask relates to the idea of a complete request/response cycle. It keeps a track of 
application-level data during a request or a CLI command. We make use of g and current_app proxies to achieve the same.
```

#### Q-6 Describe the features of Forms extension for Flask ?
```bash
Forms in Flask can be implemented by using an extension called Flask-WTF. Flask-WTF is created by integrating Flask with WTForms. 
WTForms is a python-based form rendering and validation library. It supports data validation, internationalization, and CSRF 
protection.

Flask-WTF also provides reCAPTCHA support along with file uploads when tied with Flask-Uploads. You also can handle JavaScript 
requests, and customize the error response.

from flask import Flask, render_template, request
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

app = Flask(__name__)
app.config['SECRET_KEY'] = 'secret'

class NameForm(FlaskForm):
    name = StringField('Name', validators=[DataRequired()])
    submit = SubmitField('Submit')

@app.route('/', methods=['GET', 'POST'])
def index():
    form = NameForm()
    if form.validate_on_submit():
        return f'Hello, {form.name.data}!'
    return render_template('index.html', form=form)

if __name__ == '__main__':
    app.run(debug=True)   
```

#### Q-7 Explain the G object in Flask ?
```bash
g is an object provided by Flask. It is a global namespace for holding any data you want during a single app context. 
For example, a before_request handler could set g.user, which will be accessible to the route and other functions.
 
from flask import g
@app.before_request
def load_user():
    user = User.query.get(request.session.get("user_id"))
    g.user = user

@app.route("/admin")
def admin():
    if g.user is None or not g.user.is_admin:
        return redirect(url_for("index"))
```

#### Q-8 What is the utilization of jesonify() in a flask ?
```bash
This is one of the functions under the flask.json module. It can convert data to JSON and store it in the response object. 
It provides a response object with an application where json.dumps() only returns a JSON data string.
```

#### Q-9 why do we use Flask(__name__) in Flask ?
```bash
The __name__ parameter is a Python built-in variable that is set to the name of the current module. When we pass __name__ as 
an argument to the Flask class constructor, it helps Flask to determine where to locate resources such as templates and static 
files.
```

#### Q-10 What is Flask-Bcrypt ?
```bash
Flask-Bcrypt is a Flask extension that provides password hashing and verification functionality for Flask applications.
```

#### Q-11 What is Flask-JWT ?
```bash
Flask-JWT is a Flask extension that provides JSON Web Token (JWT) authentication and authorization functionality for Flask 
applications.
```

#### Q-12 How to disable csrf for a view with flask-wft for a restapi ?
```bash
form = myForm(request.form, csrf_enabled=False)
```

#### Q-13 How to share the global app object in flask ?
```bash
You can create an overall package and add an __init__.py file under the package folder where you declare all the global 
variables that you need to share between the classes. Then, you should add the code "app = Flask(__name__)" in the 
__init__.py file. Now you can share and use the app variables anywhere if you just import the package name.
```

#### Q-14 How to get logged user id in flask?
```bash
current_user.get_id() is used to get logged in user id in flask.
from flask import g
if current_user.is_authenticated():
        g.user = current_user.get_id()
```

#### Q-15 How to enable logging in python flask?
```bash
import logging
from flask import Flask
app = Flask(__name__)

@app.route('/')
def foo():
    app.logger.warning('A warning occurred')
    app.logger.error('An error occurred')
    app.logger.info('Info')
    return "foo"
```

#### Q-16 How to return json in flask?
```bash
from flask import jsonify
@app.route('/users')
def users():
   users= User.query.all()  
    return jsonify(users)
```

#### Q-17 How to serve static files in Flask?
```bash
url_for(‘static’, filename=’static_file_name’)
```

#### Q-18 How can we create a form for file uploading?
```bash
<html>  
   <body>  
           <form action = "http://localhost:5000/uploader" method = "POST" enctype = "multipart/form-data">  
             <input type = "file" name = "file" />  
             <input type = "submit"/>  
           </form>          
   </body>  
</html>
```

#### Q-19 What are pickling and unpickling?
```bash
make a portable and serialized representations of Python objects, we have the module known as pickle which accepts a Python 
object (basically everything in Python is an object) and then converts it into a string type, and after that uses the dump () 
function to dump it into a file. We term this as pickling. On the contrary, retrieving objects from the stored string forms is 
called as unpickling.
```

#### Q-20 How to get http headers in flask?
```bash
app = flask.Flask(__name__)
@app.route("/")
def index():
    headers = flask.request.headers
    return "Request headers:\n" + str(headers)

app.run(host="127.1.0.1", port=8080)
```