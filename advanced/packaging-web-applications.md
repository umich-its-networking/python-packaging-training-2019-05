---
title: Packaging a Reusable Web Application
---

## Django package versus standard Python library

A Django package, also sometimes referred to as a reusable application, is a standalone Python library with a structure that resembles closely to a Django web app

Both are a means for distributing software, but functionally a Django package has some extra features.

This means that it can include things like `models.py`, `views.py`, etc.

Its format makes it easier to include in an existing Django application

You can `pip install` the package as usual and simply add the dotted Python path to `INSTALLED_APPS` in `setup.py`
Any app-specific settings for the package are added to the main `settings.py` file

## Creating a reusable web application

First, let's clone the sample mysite project from the [official Django tutorial](https://docs.djangoproject.com/en/2.2/intro/reusable-apps/) with steps 1 thru 7 completed:

```terminal
$ git clone https://github.com/jonathoy/django-tutorial.git
Cloning into 'django-tutorial'...
remote: Enumerating objects: 70, done.
remote: Counting objects: 100% (70/70), done.
remote: Compressing objects: 100% (39/39), done.
remote: Total 70 (delta 22), reused 70 (delta 22), pack-reused 0
Unpacking objects: 100% (70/70), done.
```

Let's verify that the project exists and change directory to it

```terminal
$ cd django-tutorial/
$ ls -l
total 0
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 content
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 mysite
```

If you have taken the Django tutorial before, you might recall that the polls application was created with the following command:

```python
python manage.py startapp polls
```

We will take the work that was built out in that portion of the tutorial and move the entire polls directory into a separate parent directory

```terminal
$ mkdir django-polls
$ mv mysite/polls/ ./django-polls/
$ ls -l
total 0
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 content
drwxr-xr-x  2 jonathoy  1410742483   64 May  8 13:57 django-polls
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 mysite
```

For our application, we should create a README with some basic instructions for how the app should be installed and configured

```terminal
$ cd django-polls
$ cp ../content/README.md ./
$ ls -l
total 8
-rw-r--r--   1 jonathoy  1410742483  714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483  384 May  8 13:56 polls
```

We should also add a LICENSE. [choosealicense.com](https://choosealicense.com/) can help with that

```terminal
$ cp ../content/LICENSE ./
$ ls -l
total 16
-rw-r--r--   1 jonathoy  1410742483  1069 May  8 14:00 LICENSE
-rw-r--r--   1 jonathoy  1410742483   714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483   384 May  8 13:56 polls
```

Now we can create the setup.py file, as we did previously for the [simple package tutorial]({{ "simple-package" | relative_url }}). Recall that the `setup.py` file contains metadata on how to build and install the app

```terminal
$ cp ../content/setup.py ./
$ ls -l
total 24
-rw-r--r--   1 jonathoy  1410742483  1069 May  8 14:00 LICENSE
-rw-r--r--   1 jonathoy  1410742483   714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483   384 May  8 13:56 polls
-rw-r--r--   1 jonathoy  1410742483  1203 May  8 14:02 setup.py
```

Now we need to create `MANIFEST.in`. `MANIFEST.in` describes any additional files that should be included in the reusable application that are not modules or packages. This could be static content or a README

```terminal
$ cp ../content/MANIFEST.in ./
$ ls -l
total 32
-rw-r--r--   1 jonathoy  1410742483  1069 May  8 14:00 LICENSE
-rw-r--r--   1 jonathoy  1410742483   104 May  8 14:09 MANIFEST.in
-rw-r--r--   1 jonathoy  1410742483   714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483   384 May  8 13:56 polls
-rw-r--r--   1 jonathoy  1410742483  1203 May  8 14:02 setup.py
$ cat MANIFEST.in
include LICENSE
include README.md
recursive-include polls/static *
recursive-include polls/templates *
```

That's that basic structure that we need to create a package! If we want to share it with others, [we should build it as a distribution...]({{ "/advanced/creating-distributable-django-package" | relative_url }})

### References

- [Django Project - How to write reusable apps](https://docs.djangoproject.com/en/2.2/intro/reusable-apps/)
- [Official Setuptools Documentation](https://setuptools.readthedocs.io/en/latest/)
