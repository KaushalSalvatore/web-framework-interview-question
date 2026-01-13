#### Q-1  How do you handle errors in Flask ?
```bash
In Flask, you can handle errors gracefully by using error handlers. This allows you to define custom responses 
for various HTTP error codes, enhancing the user experience.

Steps:

Using the @app.errorhandler Decorator: You can create custom error handlers for specific error codes, such as 
404 (Not Found) or 500 (Internal Server Error):

@app.errorhandler(404)
def not_found(error):
    return "This page does not exist.", 404

@app.errorhandler(500)
def internal_error(error):
    return "An internal error occurred.", 500

@app.errorhandler(Exception)
def handle_exception(error):
    return "An unexpected error occurred.", 500
```

#### Q-2 What are cookies, and how does Flask handle them ?
```bash
Setting a Cookie:

from flask import Flask, request, make_response

@app.route('/setcookie')
def set_cookie():
    resp = make_response("Cookie Set")
    resp.set_cookie('username', 'Alice')  # Set a cookie
    return resp

Retrieving a Cookie:

@app.route('/getcookie')
def get_cookie():
    username = request.cookies.get('username')  # Retrieve the cookie
    return f'Username is {username}'

Deleting a Cookie:
@app.route('/deletecookie')
def delete_cookie():
    resp = make_response("Cookie Deleted")
    resp.set_cookie('username', '', expires=0)  # Clear the cookie
    return resp
```

#### Q-3 How can you perform logging in Flask ?
```bash
import logging
logging.basicConfig(level=logging.INFO)  # Set logging level
@app.route('/')
def index():
    app.logger.info('Home page accessed')  # Log an info message
    return "Welcome to the home page!"

app.logger.warning('This is a warning message')
app.logger.error('This is an error message')
```

#### Q-4 What is the use of before_request and after_request decorators ?
```bash
 the before_request and after_request decorators are used to execute specific functions before and after each request, 
 respectively. This is useful for tasks like setting up database connections, processing user authentication, or performing 
 logging.

 before_request:

Purpose: The function decorated with @app.before_request runs before every request. You can use it to perform checks or set 
up preconditions.

@app.before_request
def before_request_func():
    print("This runs before every request.")


after_request:

Purpose: The function decorated with @app.after_request runs after each request is completed, just before the response 
is sent to the client. It's useful for modifying the response or performing cleanup.

@app.after_request
def after_request_func(response):
    print("This runs after every request.")
    response.headers["X-Custom-Header"] = "Custom Value"
    return response
```

#### Q-5 What is the purpose of the abort function ?
```bash
The abort function in Flask is used to raise an HTTP exception and immediately stop the execution of a view function. 
It allows you to send specific HTTP error responses back to the client.

from flask import abort

@app.route('/user/<int:user_id>')
def get_user(user_id):
    user = find_user(user_id)
    if user is None:
        abort(404)  # Raises a 404 Not Found error
    return f"User: {user.name}"
```

#### Q-6 What are Flask signals, and how are they used ?
```bash
Flask signals provide a mechanism for decoupled components to communicate with each other by sending and receiving 
notifications about events occurring in the application.

Key Features:-
1.Decoupling
2.Custom Events

from flask import Flask, signals

app = Flask(__name__)

@signals.before_request.connect
def before_request_handler(sender, **extra):
    print("A request is about to be processed.")

@signals.teardown_request.connect
def teardown_request_handler(sender, **extra):
    print("A request has been processed.")
```

#### Q-7  How do you structure a Flask application using Blueprints ?
```bash
from flask import Blueprint

my_blueprint = Blueprint('my_blueprint', __name__)

@my_blueprint.route('/hello')
def hello():
    return "Hello from the blueprint!"

from flask import Flask

app = Flask(__name__)
from my_blueprint import my_blueprint
app.register_blueprint(my_blueprint)
```

#### Q-8 How can you use Flask with a NoSQL database like MongoDB ?
```bash
pip install flask-pymongo

from flask import Flask
from flask_pymongo import PyMongo

app = Flask(__name__)
app.config["MONGO_URI"] = "mongodb://localhost:27017/mydatabase"
mongo = PyMongo(app)
```

#### Q-9 How do you handle file storage and management in Flask ?
```bash
Use Flask's request object to handle file uploads.

from flask import request

@app.route('/upload', methods=['POST'])
def upload_file():
    if 'file' not in request.files:
        return 'No file part'
    file = request.files['file']
    if file.filename == '':
        return 'No selected file'
    file.save(os.path.join(UPLOAD_FOLDER, file.filename))
    return 'File uploaded successfully'
```

#### Q-10 How do you handle asynchronous tasks in Flask ?
```bash
Handling asynchronous tasks in Flask can be effectively managed using task queues, with Celery being one of 
the most popular solutions. Celery allows you to offload long-running tasks to a background worker, enabling 
your Flask application to remain responsive.

pip install celery

from flask import Flask
from celery import Celery

app = Flask(__name__)
app.config['CELERY_BROKER_URL'] = 'redis://localhost:6379/0'
celery = Celery(app.name, broker=app.config['CELERY_BROKER_URL'])
celery.conf.update(app.config)

@celery.task
def long_running_task(arg):
    # Perform a time-consuming operation
    return f"Task completed with argument: {arg}"
```

#### Q-11 How can you structure a Flask application into multiple files or folders ?
```bash
You can structure a Flask application into multiple files and folders using blueprints or packages. Blueprints
are a way to organize a group of related views and other code. Packages, on the other hand, provide a way to 
encapsulate the application's code into a directory structure.

my_app/
├── __init__.py
├── models.py
├── views/
│   ├── __init__.py
│   ├── user_views.py
│   └── product_views.py
├── templates/
│   ├── users/
│   └── products/
└── static/
```

#### Q-12 Explain how to use Flask-Migrate for database migrations ?
```bash
flask db init: Creates the migration repository.
flask db migrate: Autogenerates migration scripts based on changes to your models.
flask db upgrade: Applies the latest migration to the database.
flask db downgrade: Reverts to a previous migration.
```

#### Q-13 You need multiple database connections in one app. How do you configure them ?
```bash
Define multiple SQLALCHEMY_BINDS.

class Config:
    SQLALCHEMY_DATABASE_URI = "mysql://root:pass@localhost/main_db"
    SQLALCHEMY_BINDS = {
        'users': "postgresql://admin:pass@localhost/users_db",
        'logs': "sqlite:///logs.db"
    }
    SQLALCHEMY_TRACK_MODIFICATIONS = False
```

#### Q-14 You need to test routes without running the server. How ?
```bash
Use Flask’s test client:
client = app.test_client()
```

#### Q-15 You need to serve millions of records via a data export API. How do you avoid memory overflow ?
```bash
def generate_csv():
    for row in db.session.query(LargeTable).yield_per(1000):
        yield f"{row.id},{row.name}\n"
```

#### Q-16 Your project requires secure admin dashboard access. How do you implement this ?
```bash
Role-based access control (RBAC)
Flask-Login
Secure cookies
2FA for admin area
IP whitelisting (optional)
```

#### Q-17 You need to return different responses based on user roles. How do you handle authorization ?
```bash
Create a custom decorator:

def role_required(role):
    def wrapper(fn):
        @wraps(fn)
        def decorated(*args, **kwargs):
            if g.user.role != role:
                return {"error": "Forbidden"}, 403
            return fn(*args, **kwargs)
        return decorated
    return wrapper
```

#### Q-18 Design a scalable user authentication system using Flask ? 
```bash
Flask API (Login/Register/Refresh token)
JWT for stateless authentication
Redis for session blacklist or token revocation
Rate limiting for brute-force protection
```

#### Q-19 Design a microservices architecture using Flask ? 
```bash
Multiple Flask microservices (Users, Orders, Payments)
API Gateway (Nginx/Kong)
Message broker (RabbitMQ/Kafka)
Central logging (ELK)
```

#### Q-20 Design a serverless Flask API ?
```bash
Convert Flask app using Zappa or AWS Lambda + API Gateway
Use DynamoDB/RDS
S3 for media
CloudWatch logs
``` 