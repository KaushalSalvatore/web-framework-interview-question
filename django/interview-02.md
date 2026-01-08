#### Q-1 How to handle Ajax requests in Django?
```bash
AJAX (Asynchronous JavaScript And XML) allows web pages to update asynchronously to and from the server 
by exchanging data in Django.

To handle Ajax requests in the Django web framework, perform the following:

Initialize Project 
Create models
Create views
Write URLs
Carry out requests with Jquery Ajax.
Register models to admin 
```

#### Q-2 Does Django support multiple-column primary keys?
```bash
Django does not support multiple-column primary keys. It only supports single-column primary keys.
```

#### Q-3 Explain The Migration In Django ? 
```bash
Migration in Django is to make changes to our models like deleting a model, adding a field, etc. 
into your database schema.
A migration in Django is a Python file that contains changes we make to our models so that they 
can be converted into a database schema in our DBMS. 
So, instead of manually making changes to our database schema by writing queries in our DBMS shell,
 we can just make changes to our models. 
Then, we can use Django to generate migrations from those model changes and run those migrations to 
make changes to our database schema.
```

#### Q-4 How You Can Set Up The Database In Django?
```bash
To set up a database in Django, you can find its configurations in setting.py  file that representing 
Django settings.

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'helloworld',
        'USER': '<yourname>',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

#### Q-5 What do you mean by the CSRF Token?
```bash
CSRF stands for Cross Site Request Forgery. 
```

#### Q-6 What Is A QuerySet In Django?
```bash
QuerySet is a collection of SQL queries. 
A QuerySet in Django is basically a collection of objects from our database.
```

#### Q-7 What Is The Difference Between Emp.object.filter(), Emp.object.get() & Emp.objects.all() 
in Django Queryset ?
```bash
In order to view all the items from your database, you can make use of the ‘all()’ function as 
mentioned below:

Users.objects.all()     

To filter out some element from the database, you either use the get() method or the filter() 
method as follows:

Users.objects.filter(name="Nitin")
Users.objects.get(name="Nitin")

Basically use get() when you want to get a single unique object, &
filter() when you want to get all objects that match your lookup parameters
```

#### Q-8 What Is The Difference Between Authentication And Authorization?
```bash
Authentication - Who Are You?
Authorization - What Permissions Do You Have?

Authentication is the process of verifying who someone is, 
whereas Authorization is the process of verifying what specific applications, files, and data a 
user has access to.
```

#### Q-10 What Is The Use Of The “include” Function In The urls.py File In Django ?
```bash
damoapp -- urls.py

    from django.urls import path
    from . import views

    urlpatterns = [  
        path('', views.index),  # damoapp homepage
    ]     

myapp -- urls.py

    from django.urls import path
    from . import views

    urlpatterns = [  
        path('', views.index),  # myapp homepage
    ]  

nitman -- urls.py

    from django.contrib import admin  
    from django.urls import path, include

    urlpatterns = [  
        path('admin/', admin.site.urls),  
        path('damoapp/', include('damoapp.urls')),  
        path('myapp/', include('myapp.urls')),  
    ] 
```

#### Q-11 What Is Context In Django ?
```bash
A context in Django is a dictionary, in which keys represent variable names and values represent their 
values. This dictionary (context) is passed to the template which then uses the variables to output
the dynamic content.

A context is a variable name -> variable value mapping that is passed to a template.
```

#### Q-12 What Is The Difference Between Django OneToOneField & ForeignKey Field?
```bash
ForeignKey Field: A many-to-one relationship. Requires two positional arguments: the class to 
which the model is related and the on_delete option.

OneToOneField: A one-to-one relationship. Conceptually, this is similar to a ForeignKey with 
unique=True, but the “reverse” side of the relation will directly return a single object.
```

#### Q-13 Explain Django’s architecture ? 
```bash
The model will serve as an interface for your data. It is in charge of data management. 
A database represents the logical data structure that supports the entire application such 
as MySql and Postgres.

The View is the user interface, that renders a website page in your browser. HTML/CSS/Javascript 
and Jinja files are used to represent it.

A template is made up of both static sections of the desired HTML output and specific syntax 
that describes how dynamic content will be included.
```

#### Q-14 What are the different model inheritance styles in Django ?
```bash
Abstract base classes - When the parent class contains common fields and the parent class
table is undesirable, use this.

Multi-table inheritance - When the parent class has common fields, but the parent class 
table already exists in the database on its own, use this.

Proxy models - Use this when you want to change the parent class's behavior, for as by 
modifying the order or adding a new model manager.
```

#### Q-15 What is a Meta Class in Django ?
```bash
A Meta class is simply an inner class that provides metadata about the outer class in Django. 
It defines such things as available permissions, associated database table name, singular and 
plural versions of the name, etc.
```

#### Q-16 What is the django.test.Client class used for?
```bash
The Client class acts as a dummy web browser, allowing us to test our views and interact with 
our Django-powered application programmatically. This is especially helpful for doing integration 
testing.
```

#### Q-17 Which class do we inherit from in order to perform functional tests?
```bash
We inherit from django.test.LiveServerTestCase. It launches a live Django server in the 
background on setup and shuts it down on teardown.
```


#### Q-18 What is Django Rest Framework(DRF)?
```bash
Django ORM (Object-Relational Mapping) is a powerful feature of the Django web framework. It is 
a high-level abstraction layer that allows developers to interact with the database using Python
objects instead of writing raw SQL queries. This ORM system bridges the gap between the relational 
database and the object-oriented Python code.
```

#### Q-19 command to check packages installed in django python ? 
```bash
pip freeze
```

#### Q-20 How does Django handle a request?
```bash
When the Django Server receives a request, it uses an algorithm to identify which Python code 
needs to be executed. The steps are as follows:
Django examines the setup of the root URL.
Django then searches all variable URL patterns in the URLconf for a match to the requested URL.
If the URL matches, it returns the view function linked with it.
For any data requirements, it will then request data from the Model of that app and deliver it
to the associated Template shown by the browser.
Django provides an error-handling view if none of the provided URLs match the requested URL.
```