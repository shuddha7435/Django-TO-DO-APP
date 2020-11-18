# Django-TO-DO-APP

Setting up the Backend

```
$ mkdir django-todo-react
```

Then we will navigate to the directory

```
cd django-todo-react
```

We will install Django using Pipenv then create a new project called backend


```
$ pipenv install django
$ django-admin startproject backend
```

Next, we will navigate into the newly created backend folder and start a new application called todo. We will also run migrations and start up the server:

```
$ cd backend
$ python manage.py startapp todo
$ python manage.py migrate
$ python manage.py runserver
```
If we check http://localhost:8000 then we will see this picture

![Django_Install](https://user-images.githubusercontent.com/16424882/99523668-9464e800-29c1-11eb-8d96-1a2a16d45ffa.png)

# Registering the Todo application

Open the backend/settings.py file and update the INSTALLED_APPS section as so:

```
# backend/settings.py

# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'todo' # add this
  ]
```

# Defining the Todo model

Let’s create a model to define how the Todo items should be stored in the database, open the todo/models.py file and update it with this snippet:

```
# todo/models.py

from django.db import models
# Create your models here.

# add this
class Todo(models.Model):
  title = models.CharField(max_length=120)
  description = models.TextField()
  completed = models.BooleanField(default=False)

  def _str_(self):
    return self.title
```

```
$ python manage.py makemigrations todo
$ python manage.py migrate todo
```

Open the todo/admin.py file and update it accordingly:

```
# todo/admin.py

from django.contrib import admin
from .models import Todo # add this

class TodoAdmin(admin.ModelAdmin):  # add this
  list_display = ('title', 'description', 'completed') # add this

# Register your models here.
admin.site.register(Todo, TodoAdmin) # add this
```

```
$ python manage.py createsuperuser
```

Let’s start the server once more and log in on the address — http://localhost:8000/admin:

```
python manage.py runserver
```

![Admin_Panel](https://user-images.githubusercontent.com/16424882/99523712-a21a6d80-29c1-11eb-9cea-9b1571097c66.png)

Here is the screenshot from the TO-DO List App when we add an item in the list

![Sample TO-DO](https://user-images.githubusercontent.com/16424882/99523732-a777b800-29c1-11eb-87e1-85097de8f3b1.png)


Here is the screenshot of the full TO-DO List

![TO-DO-LIST](https://user-images.githubusercontent.com/16424882/99523743-ad6d9900-29c1-11eb-8ac8-a97bf040fe39.png)



