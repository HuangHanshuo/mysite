# mysite
django site

## Init
Install Django: https://docs.djangoproject.com/en/1.8/intro/install/

```
django-admin startproject mysite
```
This will create a mysite directory in your current directory. 

```
python manage.py migrate
```
The migrate command looks at the `INSTALLED_APPS` setting and creates any necessary database tables according to the database settings in your mysite/settings.py file and the database migrations shipped with the app (we’ll cover those later).

```
python manage.py runserver
```
Run the server

```
python manage.py startapp polls
```
Start a new app. That’ll create a directory polls

## Models
After creating two models.
### polls/models.py
```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

Set the new created app to `INSTALLED_APPS` in `mysite/settings.py`

```
python manage.py makemigrations polls
```
By running `makemigrations`, you’re telling Django that you’ve made some changes to your models (in this case, you’ve made new ones) and that you’d like the changes to be stored as a migration.

```
python manage.py sqlmigrate polls 0001
```
The `sqlmigrate` command takes migration names and returns their SQL.

```
python manage.py migrate
```
Run `migrate` again to create those model tables in your database

## Admin
First we’ll need to create a user who can login to the admin site. Run:
```
python manage.py createsuperuser
```
Then input username and email and password.

###polls/admin.py
```
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```
Register model to admin.

## Views and templates


## Forms and generic views
