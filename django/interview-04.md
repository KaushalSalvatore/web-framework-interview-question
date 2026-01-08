#### Q-1 What is Django caching? And describe the techniques employed to put it into action ?
```bash
Add the cache backend to your settings.py file by specifying the CACHES setting.
Use the cache in your views by importing the cache module and using the cache.set 
and cache.get methods.

from django.shortcuts import render
from django.core.cache import cache

def my_view(request):
    result = cache.get('my_cache_key')
    if result is None:
        result = expensive_operation()
        cache.set('my_cache_key', result, 3600)
    return render(request, 'my_template.html', {'result': result})

Type of caching :    
1. Database caching
2. Local-memory caching	
3. Filesystem caching	
4. Memcached
```

#### Q-2 How do you use Django's built-in permission system to control access to views and models?
```bash
Add the django.contrib.auth app to your INSTALLED_APPS list in the settings.py file.
Add the django.contrib.auth.decorators.login_required decorator to your view to require authentication.
Add the django.contrib.auth.decorators.permission_required decorator to your view to require a specific permission.
```

#### Q-3 Explain what does django-admin.py makemessages command is used for?
```bash
This command line executes over the entire source tree of the current directory and abstracts all the 
strings marked for translation.  It makes a message file in the locale directory.
```

#### Q-4 What are loaddata and dumpdata?
```bash
to load data into Django you have to use the command line. The command line will searches the data and loads 
the contents of the named fixtures into the database.
Django-admin.py loaddata

Dumpdata is a command to back up both current model instances and the whole database. Its syntax is rather 
simple. db.json will dump the whole database into a db.json file.
python manage.py dumpdata
```

#### Q-5 How can you use file-based sessions?
```bash
You need to change the SESSION_ENGINE settings in the “django.contrib.sessions.backends.file.”
```

#### Q-6 What is a signal dispatcher?
```bash
A signal dispatcher allows one part of a program to announce that something happened, and 
automatically notifies all registered listeners.

They help to:
Decouple components (no direct dependencies)
Improve maintainability
Enable event-driven programming
Allow multiple listeners for the same event

How It Works (Conceptually)
A signal/event occurs
The dispatcher broadcasts it
Receivers/handlers that are registered get notified
Each handler reacts independently

Common Use Cases
Logging actions
Sending emails after user signup
Cache invalidation
Auditing & analytics
Background tasks triggers

from django.db.models.signals import post_save
from django.dispatch import receiver
```

#### Q-7 Describe the steps in the Django request-response life cycle ? 
```bash
A Django request flows from the client through the web server, URL routing, middleware, view logic, 
model/database interaction, template rendering, and then back through middleware before returning the 
response.

1. Client
  ↓
2. Web Server
  ↓
3. Middleware (request)
  ↓
4. URL Resolver
  ↓
5. View
  ↓
6. Model / DB
  ↓
7. Template
  ↓
8. Response
  ↑
9. Middleware (response)
  ↑
10. Client

1️⃣ Client Sends HTTP Request
A user (browser, mobile app, API client) sends an HTTP request
Example: GET /products/

2️⃣ Web Server Receives Request
Web server (e.g., Nginx / Apache) receives the request
Forwards it to Django via WSGI/ASGI
Client → Nginx → WSGI/ASGI → Django

3️⃣ Django URL Resolver (URLconf)
Django checks urls.py
Matches request path to a URL pattern
Determines which view should handle the request
path("products/", views.product_list)

4️⃣ Middleware Processing (Request Phase)
Django passes the request through middleware (top → bottom).
Common middleware tasks:
Authentication
Session handling
CSRF protection
Security checks
Logging

5️⃣ View Is Called
The matched view function / class-based view is executed
Business logic happens here
Data is fetched from models or external services
def product_list(request):
    products = Product.objects.all()
    return render(request, "products.html", {"products": products})

6️⃣ Model Interaction (If Needed)
View interacts with models
Django ORM generates SQL
Database returns data
View → ORM → Database → ORM → View

7️⃣ Template Rendering (If HTML Response)
Context data is passed to a template
Django template engine renders HTML
render(request, "template.html", context)

8️⃣ Response Object Is Created
View returns an HttpResponse (or subclass like JsonResponse)
Contains response body, status code, headers

9️⃣ Middleware Processing (Response Phase)
Response goes back through middleware (bottom → top).
Common tasks:
Modify response headers
Compress response
Add cookies
Handle exceptions

🔟 Response Sent Back to Client
Django sends response to WSGI/ASGI
Web server returns it to the client
Django → WSGI/ASGI → Nginx → Client
```

#### Q-8 What is a transaction in Django ?
```bash
A transaction in Django is a way to ensure that a group of database operations execute as a single unit of work.
"Either all database operations succeed, or none of them are applied."

from django.db import transaction

Real Example  :-
Deduct money from wallet
Create order record
Reduce product stock
```

#### Q-9 How do you rollback a migration in Django ?
```bash
python manage.py migrate <appname> <migration_number> --fake
```

#### Q-10 How do you debug and troubleshoot problems with Django's ORM?
```bash
python manage.py shell
```

#### Q-11 What is the difference between a Django model and a Django form?
```bash
A Django model is a Python class that defines the fields and behavior of a database table. It is used 
to represent the data that will be stored in the database and provides an interface for interacting with 
that data.

from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=200)
    publication_date = models.DateField()

A Django form, on the other hand, is a Python class that defines a form that can be displayed in a web 
page and used to collect user input. It is used to validate and process user input, and can be used to 
create, update, or delete data in the database.

from django import forms
from .models import Book

class BookForm(forms.ModelForm):
    class Meta:
        model = Book
        fields = ['title', 'author', 'publication_date']
```

#### Q-12 How do you pass data from a view to a template in Django?
```bash
from django.shortcuts import render
def my_view(request):
    my_data = {"name": "John Doe", "age": 30}
    return render(request, "template.html", my_data)
```

#### Q-13 How do you handle HTTP methods in Django views?
```bash
from django.views.decorators.http import require_GET
@require_GET
@require_POST (if request.method == "POST":)
```

#### Q-14 How do you pass data from a view to a template in Django?
```bash
from django.shortcuts import render
import datetime

def my_view(request):
    current_time = datetime.datetime.now()
    context = {'current_time': current_time}
    return render(request, 'mytemplate.html', context)
```

#### Q-15 How do you handle complex queries in Django?
```bash
from django.db.models import Q
books = Book.objects.filter(Q(title='Django for Dummies') | Q(title='Django for Pros'))
```

#### Q-16 How do you customize the database table name for a model in Django?
```bash
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=100)

    class Meta:
        db_table = 'my_custom_book_table'
```

#### Q-17 How do you handle real-time data in Django?
```bash
WebSockets: You can use WebSockets to handle real-time data in Django.
Django Channels: Django Channels is a third-party library that extends Django to handle WebSockets 
and other asynchronous protocols.
Django-Push: Django-Push is a third-party library that makes it easy to send push notifications 
to mobile devices.
```

#### Q-18 Avoid deadloak in django ( F() ) ?  
```bash
Just update the filtered records. Lock for these records will be released then your transaction 
will be committed. What the code above does is: it will try running the query and if an OperationalError
is thrown with the error code 1213 (a deadlock), it will wait for 200 ms and try again.
 
An F() object specifies the value of a model field, or it refers to the model field values directly 
in the database. Let's have a simple example, A Student class with a fees field, and we want to increase 
the 20 percent fees of the student.
 
from django.db.models import F   
Student.objects.update(fees=F('fees') * 1.2)  

or 

student = Student.objects.all()  
for stu in student:  
    stu.fees *= 1.2
```

#### Q-19 why we use gunicorn ? 
```bash
Gunicorn is a WSGI compliant web server for Python Applications that receive requests sent to the 
Web Server from a Client and forwards them onto the Python applications or Web Frameworks 
(such as Flask or Django) in order to run the appropriate application code for the request.
```

#### Q-20 database connectivity steps in Django ?
```bash
1️⃣ Install Database Driver
Django talks to databases through drivers.
Database	Driver
SQLite	Built-in
PostgreSQL	psycopg2
MySQL	mysqlclient
Oracle	cx_Oracle

pip install psycopg2-binary

2️⃣ Configure Database in settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydb',
        'USER': 'dbuser',
        'PASSWORD': 'secret',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

3️⃣ Create Django App & Models
python manage.py startapp myapp

from django.db import models

class Employee(models.Model):
    name = models.CharField(max_length=100)
    salary = models.IntegerField()

4️⃣ Register App in settings.py
INSTALLED_APPS = [
    'myapp',
]

5️⃣ Create Migrations
python manage.py makemigrations

6️⃣ Apply Migrations (Connects to DB)
python manage.py migrate

7️⃣ Use Django ORM (Database Interaction)
Create:
Employee.objects.create(name="John", salary=50000)
Read: 
Employee.objects.all()
Update:
emp.salary = 60000
emp.save()
Delete:
emp.delete()
```