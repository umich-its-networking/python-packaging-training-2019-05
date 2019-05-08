---
title: Packaging a Reusable Web Application
---

This tutorial will guide you through the process of packaging a reusable web application

A reusable web application is essentially a Python package with a structure similar to a Django project

It can contains things like models.py, views.py, etc. and is included to a Django project by adding it to the `INSTALLED_APPS` setting in settings.py

## Clone the sample mysite project

```terminal
$ git clone https://github.com/jonathoy/django-tutorial.git
Cloning into 'django-tutorial'...
remote: Enumerating objects: 70, done.
remote: Counting objects: 100% (70/70), done.
remote: Compressing objects: 100% (39/39), done.
remote: Total 70 (delta 22), reused 70 (delta 22), pack-reused 0
Unpacking objects: 100% (70/70), done.
```

## Verify and change directory to project

```terminal
$ cd django-tutorial/
$ ls -l
total 0
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 content
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 mysite
```

## (Optional) Update setuptools to latest version

```terminal
$ python -m pip install --upgrade pip setuptools
Collecting pip
  Downloading https://files.pythonhosted.org/packages/5c/e0/be401c003291b56efc55aeba6a80ab790d3d4cece2778288d65323009420/pip-19.1.1-py2.py3-none-any.whl (1.4MB)
    100% |████████████████████████████████| 1.4MB 14.3MB/s
Collecting setuptools
  Using cached https://files.pythonhosted.org/packages/ec/51/f45cea425fd5cb0b0380f5b0f048ebc1da5b417e48d304838c02d6288a1e/setuptools-41.0.1-py2.py3-none-any.whl
Installing collected packages: pip, setuptools
  Found existing installation: pip 19.0.3
    Uninstalling pip-19.0.3:
      Successfully uninstalled pip-19.0.3
  Found existing installation: setuptools 40.8.0
    Uninstalling setuptools-40.8.0:
      Successfully uninstalled setuptools-40.8.0
Successfully installed pip-19.1.1 setuptools-41.0.1
```

## Move polls directory into a separate parent directory

```terminal
$ mkdir django-polls
$ mv mysite/polls/ ./django-polls/
$ ls -l
total 0
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 content
drwxr-xr-x  2 jonathoy  1410742483   64 May  8 13:57 django-polls
drwxr-xr-x  6 jonathoy  1410742483  192 May  8 13:56 mysite
```

## Create a README for the application

A detailed description for how the app should be installed and configured

```terminal
$ cd django-polls
$ cp ../content/README.md ./
$ ls -l
total 8
-rw-r--r--   1 jonathoy  1410742483  714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483  384 May  8 13:56 polls
```

## Create a LICENSE file

Can select one from [choosealicense.com](https://choosealicense.com/)

```terminal
$ cp ../content/LICENSE ./
$ ls -l
total 16
-rw-r--r--   1 jonathoy  1410742483  1069 May  8 14:00 LICENSE
-rw-r--r--   1 jonathoy  1410742483   714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483   384 May  8 13:56 polls
```

## Create the setup.py file

The setup.py file describes how to build and install the app.

```terminal
$ cp ../content/setup.py ./
$ ls -l
total 24
-rw-r--r--   1 jonathoy  1410742483  1069 May  8 14:00 LICENSE
-rw-r--r--   1 jonathoy  1410742483   714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483   384 May  8 13:56 polls
-rw-r--r--   1 jonathoy  1410742483  1203 May  8 14:02 setup.py
```

## Create MANIFEST.in

A file describing any additional files that should be included in your reusable application that are not modules or packages

```terminal
$ cp ../content/MANIFEST.in ./
$ ls -l
total 32
-rw-r--r--   1 jonathoy  1410742483  1069 May  8 14:00 LICENSE
-rw-r--r--   1 jonathoy  1410742483   104 May  8 14:09 MANIFEST.in
-rw-r--r--   1 jonathoy  1410742483   714 May  8 13:59 README.md
drwxr-xr-x  12 jonathoy  1410742483   384 May  8 13:56 polls
-rw-r--r--   1 jonathoy  1410742483  1203 May  8 14:02 setup.py
```

## Try creating a distributable package

Will package the application up based on the configuration in setup.py

```terminal
$ python setup.py sdist
running sdist
running egg_info
creating django_polls.egg-info
writing django_polls.egg-info/PKG-INFO
writing dependency_links to django_polls.egg-info/dependency_links.txt
writing top-level names to django_polls.egg-info/top_level.txt
writing manifest file 'django_polls.egg-info/SOURCES.txt'
reading manifest file 'django_polls.egg-info/SOURCES.txt'
reading manifest template 'MANIFEST.in'
warning: no files found matching 'README.rst'
writing manifest file 'django_polls.egg-info/SOURCES.txt'
running check
creating django-polls-0.1
creating django-polls-0.1/django_polls.egg-info
creating django-polls-0.1/polls
creating django-polls-0.1/polls/migrations
creating django-polls-0.1/polls/static
creating django-polls-0.1/polls/static/polls
creating django-polls-0.1/polls/templates
creating django-polls-0.1/polls/templates/polls
copying files to django-polls-0.1...
copying LICENSE -> django-polls-0.1
copying MANIFEST.in -> django-polls-0.1
copying README.md -> django-polls-0.1
copying setup.py -> django-polls-0.1
copying django_polls.egg-info/PKG-INFO -> django-polls-0.1/django_polls.egg-info
copying django_polls.egg-info/SOURCES.txt -> django-polls-0.1/django_polls.egg-info
copying django_polls.egg-info/dependency_links.txt -> django-polls-0.1/django_polls.egg-info
copying django_polls.egg-info/top_level.txt -> django-polls-0.1/django_polls.egg-info
copying polls/__init__.py -> django-polls-0.1/polls
copying polls/admin.py -> django-polls-0.1/polls
copying polls/apps.py -> django-polls-0.1/polls
copying polls/models.py -> django-polls-0.1/polls
copying polls/tests.py -> django-polls-0.1/polls
copying polls/urls.py -> django-polls-0.1/polls
copying polls/views.py -> django-polls-0.1/polls
copying polls/migrations/0001_initial.py -> django-polls-0.1/polls/migrations
copying polls/migrations/__init__.py -> django-polls-0.1/polls/migrations
copying polls/static/polls/style.css -> django-polls-0.1/polls/static/polls
copying polls/templates/polls/detail.html -> django-polls-0.1/polls/templates/polls
copying polls/templates/polls/index.html -> django-polls-0.1/polls/templates/polls
copying polls/templates/polls/results.html -> django-polls-0.1/polls/templates/polls
Writing django-polls-0.1/setup.cfg
creating dist
Creating tar archive
removing 'django-polls-0.1' (and everything under it)
```

## Validate the distribution was created

```terminal
$ ls -l
total 32
-rw-r--r--   1 jonathoy  1410742483  1069 May  8 14:00 LICENSE
-rw-r--r--   1 jonathoy  1410742483   104 May  8 14:09 MANIFEST.in
-rw-r--r--   1 jonathoy  1410742483   714 May  8 13:59 README.md
drwxr-xr-x   3 jonathoy  1410742483    96 May  8 14:12 dist
drwxr-xr-x   6 jonathoy  1410742483   192 May  8 14:12 django_polls.egg-info
drwxr-xr-x  12 jonathoy  1410742483   384 May  8 13:56 polls
-rw-r--r--   1 jonathoy  1410742483  1203 May  8 14:02 setup.py
$ ls -l dist/
total 16
-rw-r--r--  1 jonathoy  1410742483  5789 May  8 14:12 django-polls-0.1.tar.gz
```

## Using the package

```terminal
$ pip install --user dist/django-polls-0.1.tar.gz
Processing ./dist/django-polls-0.1.tar.gz
Building wheels for collected packages: django-polls
  Building wheel for django-polls (setup.py) ... done
  Stored in directory: /Users/jonathoy/Library/Caches/pip/wheels/e1/c8/ab/2371c3b1da2fb1d9fbc016ed02d1ff892c188e94c5832560e0
Successfully built django-polls
Installing collected packages: django-polls
Successfully installed django-polls-0.1
```

### References

- [Django Project - How to write reusable apps](https://docs.djangoproject.com/en/2.2/intro/reusable-apps/)
- [Official Setuptools Documentation](https://setuptools.readthedocs.io/en/latest/)
