---
title: Creating a distributable Django application
---

We've learned that `pip` can install packages from source code if the format is correct, but if we want to push this to a package repository we will want to build it a distribution (for instance as a `tar.gz`)

To do this, we'll be using [setuptools](https://setuptools.readthedocs.io/en/latest/). This next step is optional, but for good measure we may want to go ahead and update it to latest version:

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

Now let's package the application up based on what we have in `setup.py`. Remember that we have specified a version number of 0.1 for our project:

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
copying LICENSE -＞ django-polls-0.1
copying MANIFEST.in -＞ django-polls-0.1
copying README.md -＞ django-polls-0.1
copying setup.py -＞ django-polls-0.1
copying django_polls.egg-info/PKG-INFO -＞ django-polls-0.1/django_polls.egg-info
copying django_polls.egg-info/SOURCES.txt -＞ django-polls-0.1/django_polls.egg-info
copying django_polls.egg-info/dependency_links.txt -＞ django-polls-0.1/django_polls.egg-info
copying django_polls.egg-info/top_level.txt -＞ django-polls-0.1/django_polls.egg-info
copying polls/__init__.py -＞ django-polls-0.1/polls
copying polls/admin.py -＞ django-polls-0.1/polls
copying polls/apps.py -＞ django-polls-0.1/polls
copying polls/models.py -＞ django-polls-0.1/polls
copying polls/tests.py -＞ django-polls-0.1/polls
copying polls/urls.py -＞ django-polls-0.1/polls
copying polls/views.py -＞ django-polls-0.1/polls
copying polls/migrations/0001_initial.py -＞ django-polls-0.1/polls/migrations
copying polls/migrations/__init__.py -＞ django-polls-0.1/polls/migrations
copying polls/static/polls/style.css -＞ django-polls-0.1/polls/static/polls
copying polls/templates/polls/detail.html -＞ django-polls-0.1/polls/templates/polls
copying polls/templates/polls/index.html -＞ django-polls-0.1/polls/templates/polls
copying polls/templates/polls/results.html -＞ django-polls-0.1/polls/templates/polls
Writing django-polls-0.1/setup.cfg
creating dist
Creating tar archive
removing 'django-polls-0.1' (and everything under it)
```

Let us validate that the distribution was created:

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

.. and try to install it

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

Success!! If we make any changes to our package, we'll want to [update the version]({{ "/versioning" | relative_url }}) in `setup.py` and repeat the steps above to create a new distribution


Now what if [I want to make this publicly accessible to others]({{ "/advanced/publicly-distributing-packages/" | relative_url }})?
