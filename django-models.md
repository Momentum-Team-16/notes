# Django Models

## What is a Django Model?

*Models* in Django are built on the Python idea of classes. Django uses the structure of the models that you create in the `models.py` file to build the database. Each model gets a table in the database, and each attribite of the model gets a column. For example, if you imagine you are a developer at Instagram, models you might have in your Django project would include `Post` and `User`. Let's look at what a `Post` model might look like:

```py
from django.db import models

class Post(models.Model):
  user = models.ForeignKey(User, on_delete=models.CASCADE)
  photo = models.ImageField()
  text = models.TextField()
  created_at = models.DateTimeField(auto_now_add=True)
  updated_at = models.DateTimeField(auto_now=True)
  
  def __str__(self):
    return f"Post {self.id} by {self.user} on {self.created_at}"
```
---  

## Some things to note about Django models:
- You will probably notice there is no `__init__()` method in this model. Where you see `(models.Model)`, that means that the `Post` model is inheriting from Django's built in `Model` class, which includes inheriting the `__init__()` method.
- What we knew as *attributes* in python are *fields* on Django models. There are many options within Django for what type a field can be. All the options can be found in [this section of the Django docs](https://docs.djangoproject.com/en/4.1/ref/models/fields/) on the right side of the page.

## How does Django use models?
- When you run the command `python manage.py makemigrations` Django creates a set of instructions to create or update tables in the database based on the structure of the models you have written. When you run `python manage.py migrate`, Django applies those instructions to the database and causes the database to be updated. Note that you have to run these two commands every time you make changes to your models.
- Each row within a table in the database is an instance of the model. The columns represent fields.
- Django databases are based on SQL, but you don't have to write SQL to use Django. The Django ORM (Object Relational Mapper) allows you to write python code that is translated into SQL queries that Django then performs on the database.
---  

## How can you see, add, and edit instances of your models in the database?
- You can access the database directly using a database browser program like [DB Browser for SQLite](https://sqlitebrowser.org/).
- You can use the Django Admin to access the database as well by adding `/admin` to the root url for the project. In order to do this, you need to create a superuser with `python manage.py createsuperuser`.
- You can use the Django shell to write one-line commands to create, retrieve, update, or delete instances of models in the Database. This [section of the DjangoGirls tutorial](https://tutorial.djangogirls.org/en/django_orm/) provides guidance on using the Django shell. 

