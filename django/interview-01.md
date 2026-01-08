#### Q.1 What is the difference between CharField and TextField in Django?
```bash
- TextField is a large text field for large-sized text. In Django, TextField is used to store 
paragraphs and all other text data. The default form widget for this field is TextArea.
- CharField is a string field used for small- to large-sized strings. It is like a string field 
in C/C++. In Django, CharField is used to store small strings like first name, last name, etc.
```

#### Q-2 Describe Django Field Class types?
```bash
The column type describes the database about what kind of data to store 
(e.g., INTEGER, VARCHAR, TEXT).
```

#### Q-3 What is the usage of "Django-admin.py" and "manage.py"?
```bash
Django-admin.py - It is a command-line utility for administrative tasks. 
manage.py - It is automatically created in each Django project and controls the Django project on the 
server or even to begin one. It has the following usage.
```

#### Q-4  How do you create a Django project?
```bash
django-admin startproject Project_name
```


#### Q-5 Are Django signals asynchronous?
```bash
No, Django signals are synchronous. There is no background thread or asynchronous jobs to execute them.
```

#### Q-6 what is  coverage ?
```bash 
Coverage.py : Coverage measurement is typically used to gauge the effectiveness of tests. It can show 
which parts of your code are being exercised by tests, and which are not.
```

#### Q-7 what is mulpti proccessing in django ?
```bash
the multiprocessing module includes a very simple and intuitive API for dividing work between multiple 
processes.
```

#### Q-8 what is mixin in django ? 
```bash
Mixin is a concept that aims to solve the problem of multiple inheritances. In brief, it removes the 
duplicate logic in different classes and separates out into its own class. From where it can be inherited 
whenever there is a need.

Django view mixins provide a way to add reusable functionality to class-based views. A mixin is a class 
that provides a set of methods that can be mixed into other classes.

To use a view mixin, you need to extend the mixin class in your view class and call the mixin's methods 
from the view's methods. For example, to add pagination to a list view.
```

#### Q-9 how to Caching Strategie implement ?
```bash
File system Caching 
Dummy Caching 
Database Caching
Localmem Caching 
Redis
```

#### Q-10 what is generic views in django (class-based generic views) ?
```bash
Generic Views are advanced set of Built-in views which are used for implementation of selective view 
strategies such as Create, Retrieve, Update, Delete. Class based views simplify the use by separating GET, 
POST requests for a view. They do not replace function-based views, but have certain differences and 
advantages when compared to function-based views:

Organization of code related to specific HTTP methods (GET, POST, etc.) can be addressed by separate 
methods instead of conditional branching.

Object oriented techniques such as mixins (multiple inheritance) can be used to factor code into 
reusable components.
```

#### Q-11 middleware usage in django ?
```bash
Middleware is a framework of hooks into Django's request/response processing.

commonMiddleware 
sessionMiddleware
crsfViewMiddleware
Session management,
Use authentication
Cross-site request forgery protection(CSRF)
Content Gzipping
```


#### Q-12 Difference between select_related and prefetch_related in django orm ?
```bash
Though both the functions are used to fetch the related fields on a model but their functioning 
is bit different from each other. In simple words, select_related uses a foreign key relationship, 
i.e. using join on the query itself while on the prefetch_related there is a separate lookup and the 
joining on the python side. 

from django.db import models
class Country(models.Model):
    country_name = models.CharField(max_length=5)
    
class State(models.Model):
    state_name = models.CharField(max_length=5)
    country = model.ForeignKey(Country)

states = State.objects.select_related(‘country’).all()
for state in states:
        print(state.state_name)  

Query Executed
SELECT state_id, state_name, country_name FROM State INNER JOIN Country ON 
(State.country_id = Country.id)

country = Country.objects.prefetch_related(‘state’).get(id=1)
for state in country.state.all():
        print(state.state_name)

Query Executed
SELECT id, country_name FROM country WHERE id=1;
SELECT state_id, state_name WHERE State WHERE country_id IN (1);
```

#### Q-13 Django Exceptions & Error-handling ? 
```bash
- AppRegistryNotReady	: It is raised when attempting to use models before the app loading process.
- ObjectDoesNotExist	: The base class for DoesNotExist exceptions.
- EmptyResultSet	: If a query does not return any result, this exception is raised.
- FieldDoesNotExist : It raises when the requested field does not exist.
- MultipleObjectsReturned	: This exception is raised by a query if only one object is expected, 
but multiple objects are returned.
- SuspiciousOperation	: This exception is raised when a user has performed an operation that should 
be considered suspicious from a security perspective.
- PermissionDenied : It is raised when a user does not have permission to perform the action requested.
- ViewDoesNotExist : It is raised by django.urls when a requested view does not exist.
- MiddlewareNotUsed : It is raised when a middleware is not used in the server configuration.
- ImproperlyConfigured : The ImproperlyConfigured exception is raised when Django is somehow improperly 
configured.
- FieldError : It is raised when there is a problem with a model field.
- ValidationError	: It is raised when data validation fails to form or model field validation.
```

#### Q-14  How to handle URLs in Django?
```bash
Let's open the file urls.py of the project and see the what it looks like:

from django.contrib import admin  
from django.urls import path  
  
urlpatterns = [  
    path('admin/', admin.site.urls),  
]  
```

#### Q-15 What is some typical usage of middlewares in Django ?
```bash
Session management,
Use authentication
Cross-site request forgery protection
Content Gzipping
```

#### Q-16 Is Django a CMS?
```bash
No, Django is not CMS (Content Management System). It's just a web framework and programming tool that 
allows you to build websites.
```

#### Q-17 When to use iterators in Django ORM?
```bash
In Django, the fair use of an iterator is when you process results that take up a large amount of 
memory space. For this, you can use the iterator() method, which evaluates the QuerySet and returns 
the corresponding iterator over the results.
```

#### Q-18 Explain the file structure of a typical Django project.
```bash
A typical Django project consists of these four files:

manage.py
settings.py
__init__.py
urls.py
wsgi.py

manage.py is the command-line utility of your Django project and controls the Django project on the server.
settings.py file includes information on all the apps installed in the project.
The urls.py file acts as a map for the whole web project. 
The __init__.py file is an empty file that makes the python interpreter understand that the directory 
consisting of settings.py is a module/ package.
The wsgi.py file is for the server format WSGI
```

#### Q-19 Is Django too monolithic? Explain this statement.
```bash
The Django framework is monolithic, which is valid to some extent. As Django's architecture is MVT-based, 
it requires some rules that developers need to follow to execute the appropriate files at the right time.
```

#### Q-20 Can you explain how to add View functions to the urls.py file?
```bash
    from django.contrib import admin  
    from django.urls import path, include

    urlpatterns = [  
        path('admin/', admin.site.urls),  
        path('myapp/', include('myapp.urls')),  
    ]  
```

