Six things I do every time I start a Django project
===================================================

Published on June 20, 2022

I start a lot of projects. A lot! Django is my go-to framework for spinning up a quick personal project, and while it's a fantastic framework, a big part of the reason I love Django is that it feels familiar.

I have a lot of muscle memory for starting a new project. Here are six things that I do after I run `django-admin startproject`.

Move the SECRET\_KEY into an environment variable
-------------------------------------------------

While it's one that you can get away with if you're keeping your source private, I reconfigure the `SECRET_KEY` as an environment variable on every new project. This helps you get started along the path of building a [Twelve Factor App](https://12factor.net/) and means that making the repository public won't expose you to problems down the line.

Having the `SECRET_KEY` in a `.gitignore`'d `.env` file means that you can change it in each environment and specify your server's secret during your deployment. We're not going to talk about deploying applications today (I use [django-up](https://github.com/sesh/django-up)) but this strategy will allow you to specify the `SECRET_KEY` as an environment variable both locally and on your server.

If you're using [`pipenv`](https://github.com/pypa/pipenv) the `.env` file will be automatically loaded when you run commands in your terminal. You can also use tools like [`direnv`](https://direnv.net/) to load the `.env` file when you move into the directory.

Update your `settings.py` to use the secret key:

```python
import os

# ...

SECRET_KEY = os.environ.get("DJANGO_SECRET_KEY")
```

Update the `.env` file to load the secret locally:

    DJANGO_SECRET_KEY=<generated-secret>

(Speaking of projects, you can use [my utilities project](https://utils.brntn.me/django-secret/) to generate a secret key the same way Django does)

Change the database configuration to DATABASE\_URL
--------------------------------------------------

Django uses SQLite out of the box for new projects. Since most of the personal projects I work on are database-agnostic, I'm happy to keep running SQLite locally and switch to Postgres on the server. To achieve this, and continue down the Twelve Factor App path, I use [`dj-database-url`](https://github.com/jazzband/dj-database-url) to specify the database with an environment variable.

If you're deploying to Heroku, Fly.io or most other PaaS providers, they will handle specifying the `DATABASE_URL` in your hosted environment. If you're managing the deployment yourself you will need to make sure the variable is properly configured in each of your environments.

Using an environment variable like this helps avoid having environment specific configuration files for your database.

First, install the package:

    pipenv install dj_database_url

Then, update your `settings.py` to use `dj-database-url` with SQLite as the default if `DATABASE_URL` isn't specified.

```python
import dj_database_url
DATABASES = {
    'default': dj_database_url.config(default=f'sqlite:///{BASE_DIR / "db.sqlite3"}')
}
```

Unless you add something to your `.env` file this will continue to use SQLite locally. Check out the [documentation](https://github.com/jazzband/dj-database-url) for how to specify Postgres or another database server for local use.

Set up a custom user model
--------------------------

Over the years, there's been a lot of discussion about changing Django's default user model. The current incarnation (that's been effectively the same since the pre-1.0 days) uses \[username, password, email, first\_name, last\_name\]. A lot of developers have started following the more modern practise of replacing the first and last name fields with a single name field.

In addition to fixing up the name, it's not unusual to replace the username with an email address. While a username has some privacy advantages (I don't want your email address!), there are problems with users forgetting usernames, and using usernames without an email address makes account recovery difficult.

If you're supporting a forgotten password flow via email or making email required for any other reason, then you might as well switch to the much simpler \[email, password, name\].

This is such a common requirement that the Django documentation actually has a [whole section for replacing the default user model](https://docs.djangoproject.com/en/4.0/topics/auth/customizing/#specifying-a-custom-user-model). You should do it. Even if you want to stick to the default setup, it will make any changes you want to make in the future much simpler.

The model that I use is shared in the [django-authuser](https://github.com/sesh/django-authuser) project. That project includes some extras like a sign up view and customised admin configuration. To implement only the custom user model and model manager you can:

    python manage.py startapp authuser

Then add the following model to `authuser/models.py`:

```python
from django.db import models
from django.contrib.auth.models import AbstractBaseUser, PermissionsMixin, UserManager
from django.utils import timezone


class CustomUserManager(UserManager):
    def _create_user(self, email, password, **extra_fields):
        """
        Create and save a User with the provided email and password.
        """
        if not email:
            raise ValueError("The given email address must be set")

        email = self.normalize_email(email)
        user = self.model(email=email, **extra_fields)
        user.set_password(password)
        user.save(using=self._db)
        return user

    def create_user(self, email=None, password=None, **extra_fields):
        extra_fields.setdefault("is_staff", False)
        extra_fields.setdefault("is_superuser", False)
        return self._create_user(email, password, **extra_fields)

    def create_superuser(self, email, password, **extra_fields):
        extra_fields.setdefault("is_staff", True)
        extra_fields.setdefault("is_superuser", True)

        if extra_fields.get("is_staff") is not True:
            raise ValueError("Superuser must have is_staff=True.")
        if extra_fields.get("is_superuser") is not True:
            raise ValueError("Superuser must have is_superuser=True.")

        return self._create_user(email, password, **extra_fields)


class User(AbstractBaseUser, PermissionsMixin):
    """
    User model that uses email addresses instead of usernames, and
    name instead of first / last name fields.

    All other fields from the Django auth.User model are kept to
    ensure compatibility with the built in management commands.
    """

    email = models.EmailField(blank=True, default="", unique=True)
    name = models.CharField(max_length=200, blank=True, default="")

    is_active = models.BooleanField(default=True)
    is_staff = models.BooleanField(default=False)
    is_superuser = models.BooleanField(default=False)

    last_login = models.DateTimeField(blank=True, null=True)
    date_joined = models.DateTimeField(default=timezone.now)

    objects = CustomUserManager()

    USERNAME_FIELD = "email"
    EMAIL_FIELD = "email"
    REQUIRED_FIELDS = []

    class Meta:
        verbose_name = "User"
        verbose_name_plural = "Users"

    def get_full_name(self):
        return self.name

    def get_short_name(self):
        return self.name or self.email.split("@")[0]
```

Once that's added, add our new app to our `INSTALLED_APPS` in `settings.py` and configure the `AUTH_USER_MODEL` setting:

INSTALLED\_APPS \= \[
    ...
    "authuser",
\]

AUTH\_USER\_MODEL \= "authuser.User"

Then make / run your migrations to set up the new user model:

\> python manage.py makemigrations
> python manage.py migrate

This model overwrites some of the fields from the `AbstractBaseUser` and `PermissionsMixin` classes. I prefer being explicit with my setup of those fields rather than relying on the base class. That said, it's unlikely that Django will change the base class, so if you want an even simpler version you can remove the `is_active`, `is_staff`, `is_superuser` and `last_login` fields from the model. If you do that, make sure you keep a close eye on the major version release notes for any changes.

Create your Django app
----------------------

We've already made a bunch of changes to our application's structure and we're only just creating our Django app!

I always try to name my first app after the primary model that the project is about. If it's a blog, then it would be `posts`. If it's a bookmark site, then it might be `links`. If it's a CRM, then it might be `clients` or `leads`.

Some folks advocate a `core` Django app to house your initial models. I'm not against this idea, but I do tend to prefer a more [Domain Driven Design](https://martinfowler.com/bliki/DomainDrivenDesign.html) approach to naming that promotes naming each app after its primary model. I find that it's easy to follow this pattern early in a project, so you might as well. After all, you're starting a project with an idea, and if you're using Django that idea probably revolves around a particular model.

Getting this name right is actually one of the trickiest parts of starting a new project. But don't worry – you'll find it easy to change with modern refactoring tools (though, best to get the name correct before you have live data).

Use the `startapp` management command to create your app:

pipenv run python manage.py startapp links

This creates the directory structure for the application. Next, update `settings.py` to include your app in the `INSTALLED_APPS`:

INSTALLED\_APPS \= \[
    ...
    "links",
\]

You don't have any models or views yet, so there's no need to do anything else at this point. Once you add models you'll run `makemigrations` and once you start adding views you might create an app-specific `urls.py` to house those routes.

Make a `base.html`
------------------

Once we have our first application it's time to get our base template sorted. I create a `base.html` file with a simple structure, then use `{% extends 'base.html' %}` in each of my templates.

Start by creating a templates directory in the app you just created. By default, Django will look for templates inside each of your `INSTALLED_APPS`. As the project grows you _might_ move this into a more central location.

mkdir links/templates

The content of the template can be fairly straight forward. You'll likely have your own preferences that you can start to include here around Javascript / CSS frameworks. I like to leave it as much of a blank canvas as possible.

Add the following to `links/templates/base.html`:

{% load static %}<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Page Title{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}" />
</head>
<body>
    {% block content %}{% endblock %}
</body>
</html>

You'll note that I have a stylesheet linked here. Create the directory and an empty file so that our page loads properly. Use this file to add your styles as the project grows.

\> mkdir -p links/static/css
> touch links/static/css/style.css

I'll add a `<header>` and `<footer>` to this `base.html` file as they are needed. If I need to include Javascript for specific templates I'll sometimes add a `{% block extra_js %}{% endblock %}` at the bottom so that I can include those from my sub templates. Until you outgrow the single content block there's no need to add that though.

Gibo and Git Init
-----------------

We have everything set up and it's time to initialise the Git repository so that we can track our work. You could use [`gibo`](https://github.com/simonwhitaker/gibo) to load up the latest version of the Github `.gitignore` file but I tend to just use this `curl` snippet to grab it:

\> curl https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore > .gitignore

That Python gitignore file includes excludes for the SQLite database and our `.env` file. There's a bunch of editor specific excludes that you might want to remove. I tend to keep them though, as they don't cause any harm.

Run `git init` in our main directory, with the `main` branch as our default. Then add our files and create an initial commit.

\> git init -b main
> git add .
> git commit -m "init: Initial commit for our new project"

You can now push this project to a public repository without leaking your SECRET\_KEY or database credentials.