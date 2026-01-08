#### Q-1 Command To Install Django ?
```bash
pip  install  django
```

#### Q-2 Command To Check Django Version ? 
```bash
python  -m  django  --version
```

#### Q-3 Command To Check all the versions of installed modules ? 
```bash
pip  freeze
```

#### Q-4 Command To Create A Project ? 
```bash
django-admin startproject DamoProject
```

#### Q-5 Command To Create An App ? 
```bash
python manage.py startapp damoapp
```

#### Q-6 Command To Run A Project ?
```bash
python manage.py runserver
python manage.py runserver 8080
python manage.py runserver 0.0.0.0:8000
```

#### Q-7 Command to create a migration file inside the migration folder ?
```bash
python  manage.py  makemigrations
```

#### Q-8 After creating a migration, to reflect changes in the database permanently execute migrate command?
```bash
python  manage.py  migrate
```

#### Q-9 To see raw SQL query executing behind applied migration execute the command ? 
```bash
python  manage.py  sqlmigrate  app_name  migration_name
python  manage.py  sqlmigrate  damoapp  0001 
```

#### Q-10 To see all migrations, execute the command ? 
```bash
python  manage.py  showmigrations
```

#### Q-11 To see app-specific migrations by specifying app-name, execute the command ? 
```bash
python  manage.py  showmigrations  nitapp
```

#### Q-12 Command To Create A SuperUser ? 
```bash
python manage.py createsuperuser
```

#### Q-14 How To View All Items In The Model Using Django QuerySet?
```bash
Users.objects.all()
```

#### Q-15 How To Filter Items In The Model Using Django QuerySet?
```bash
Users.objects.filter(name="Nitin")
```

#### Q-16 How To Get A Particular Item In The Model Using Django QuerySet?
```bash
Users.objects.get(id=25)
```

#### Q-17 How to Delete/Insert/Update An Object Using QuerySet In Django?
```bash
QuerySet To Delete An Object:
Users.objects.filter(id= 54).delete()

QuerySet To Update An Object:
user_to_be_modify = User.objects.get(pk = 3)
user_to_be_modify.city = "Pune"
user_to_be_modify.save()

QuerySet To Insert/Add An Object:
new_user = User(name = "Nitin Mangotra", city="Gurgaon")
new_user.save()
```

#### Q-18 How Can You Combine Multiple QuerySets In A View?
```bash
class Blog(models.Model):
    title = models.CharField(max_length=255)
    content = models.TextField(blank=True)

class Email(models.Model):
    title = models.CharField(max_length=255)
    content = models.TextField(blank=True)

Let's suppose the following three querysets generated from above models, that you want to combine.

query_set_1 = Blog.objects.filter(id__gte=3)
query_set_2 = Email.objects.filter(id__lte=11)
query_set_3 = Blog.objects.filter(id__lte=2)

query_set_1 = Blog.objects.filter(id__gte=3)
query_set_2 = Email.objects.filter(id__lte=11)
query_set_3 = Blog.objects.filter(id__lte=2)

1. Using Union Operator:  

combined_result= query_set_1 | query_set_3 | query_set_4 ...

2. Using Itertools:

from itertools import chain 
combined_list = list(chain(query_set_1,query_set_2))
```

#### Q-19 Explain How A Request Is Processed In Django ?
```bash
Here, a user requests for a resource to the Django, Django works as a controller and check 
to the available resource in URL. When Django server is started, the manage.py file searches 
for settings.py file, which contains information of all the applications installed in the project, 
middleware used, database connections and path to the main urls config.

Manage.py >> Setting.py >> urls.py >> views.py >> models.py >> templates
```

#### Q-20 file that create in app in django
```bash
__init__.py - An empty file that tells Python that the current directory should be considered
as a Python package.
admin.py: Reads model metadata and provides an interface to manage app content.
app.py: Application configuration details for the app are included e.g custom app name.
migrations/: Contains migrated model details with the corresponding database table structure
models.py: A class for each model is defined with the model structure layout
tests.py: App unit test automation classes are included in this
views.py: Web based requests and response is configured in this file
```