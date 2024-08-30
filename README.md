# Poll Application - Django Tutorial

Welcome to the Poll Application, a simple Django-based project created to demonstrate the basics of Django web development. This repository is based on the Django 4.2 tutorial and covers the creation of a basic poll application. The application consists of two main parts:

1. **Public Site**: Allows users to view polls and vote.
2. **Admin Site**: Allows admins to add, change, and delete polls.

## Prerequisites

- Python 3.8 or later
- Django 4.2 or later

Ensure that Django is installed by running:

```bash
$ python -m django --version
```

If Django is not installed, please refer to the [Django installation guide](https://docs.djangoproject.com/en/stable/topics/install/).

## Project Setup

To set up the project, follow these steps:

1. **Create a Django Project**:
   From your terminal, navigate to the directory where you want to store your project and run:

   ```bash
   $ django-admin startproject mysite
   ```

2. **Run the Development Server**:
   Navigate into the project directory:

   ```bash
   $ cd mysite
   ```

   Start the development server:

   ```bash
   $ python manage.py runserver
   ```

   Visit `http://127.0.0.1:8000/` in your browser to verify the project setup.

## Creating the Polls App

1. **Create an App**:
   In the root directory of your project (where `manage.py` is located), run:

   ```bash
   $ python manage.py startapp polls
   ```

2. **Define the Polls Views**:
   In `polls/views.py`, create a simple view:

   ```python
   from django.http import HttpResponse

   def index(request):
       return HttpResponse("Hello, world. You're at the polls index.")
   ```

3. **Map the URL to the View**:
   In `polls/urls.py`, map the view to a URL:

   ```python
   from django.urls import path
   from . import views

   urlpatterns = [
       path('', views.index, name='index'),
   ]
   ```

   Include this URL configuration in your project's `urls.py`:

   ```python
   from django.contrib import admin
   from django.urls import include, path

   urlpatterns = [
       path('polls/', include('polls.urls')),
       path('admin/', admin.site.urls),
   ]
   ```

4. **Run the Server**:
   Start the server again to test the polls app:

   ```bash
   $ python manage.py runserver
   ```

   Visit `http://127.0.0.1:8000/polls/` to see your app in action.

## Setting Up the Database

1. **Configure the Database**:
   Open `mysite/settings.py` and ensure the `DATABASES` setting is configured. The default is SQLite, which is sufficient for this tutorial.

2. **Create Database Migrations**:
   Run the following command to create the necessary database tables:

   ```bash
   $ python manage.py migrate
   ```

3. **Define Models**:
   In `polls/models.py`, define your database models:

   ```python
   from django.db import models

   class Question(models.Model):
       question_text = models.CharField(max_length=200)
       pub_date = models.DateTimeField('date published')

   class Choice(models.Model):
       question = models.ForeignKey(Question, on_delete=models.CASCADE)
       choice_text = models.CharField(max_length=200)
       votes = models.IntegerField(default=0)
   ```

4. **Apply Migrations**:
   After defining models, run:

   ```bash
   $ python manage.py makemigrations polls
   $ python manage.py migrate
   ```

## Admin Site

1. **Create a Superuser**:
   To access the admin site, create a superuser:

   ```bash
   $ python manage.py createsuperuser
   ```

2. **Register Models in Admin**:
   In `polls/admin.py`, register your models:

   ```python
   from django.contrib import admin
   from .models import Question

   admin.site.register(Question)
   ```

3. **Access the Admin Site**:
   Start the development server and navigate to `http://127.0.0.1:8000/admin/`. Log in with the superuser credentials to manage your polls.

## Exploring the API

You can explore the Django ORM through the Django shell:

```bash
$ python manage.py shell
```

Within the shell, you can interact with your models:

```python
from polls.models import Question, Choice
Question.objects.all()
```

## Conclusion

This poll application provides a foundational understanding of how to build web applications with Django. The concepts covered here include setting up Django projects and apps, managing databases with models and migrations, and utilizing Django’s powerful admin interface.

For more details, continue with the [Django documentation](https://docs.djangoproject.com/en/stable/intro/tutorial01/).
