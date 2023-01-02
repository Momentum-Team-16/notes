# Users in Django

For most models, you can make changes to them throughout development. The exception to this is `User`. Django has several built in `User` 
models, which you can customize. You need to decide which option you are going to use at the beginning of a project. A good breakdown of
the options can be found in this [article](https://simpleisbetterthancomplex.com/tutorial/2016/07/22/how-to-extend-django-user-model.html)

## Registration with Django Registration Redux

You *can* build your own registration, mechanism for users to sign up and log in, but we are going to use a tool for that called Django
Registration Redux. The simplest way to incorporate this tool is to:
1. `pipenv install django-registration-redux`
2. Add `registration` to the list of INSTALLED_APPS in `settings.py` at the top.
3. Follow the directions for the "Simple" (one step) setup found [here](https://django-registration-redux.readthedocs.io/en/latest/simple-backend.html).
4. Make sure you have a template called `base.html` and that it contains `{% block content %}`.

