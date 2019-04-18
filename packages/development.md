---
title: Django Application Development
---

## General Idea
- [Arrange files according to standard structure](https://the-hitchhikers-guide-to-packaging.readthedocs.io/en/latest/creation.html#arranging-your-file-and-directory-structure)
- Use setuptools to build the package
- (Optional) Upload distribution to [pypi](pypi.org) with Twine

## Structure

```
django_sample_app/
  django_sample_app/
    apps.py
    models.py
    ..etc
  LICENSE.txt
  MANIFEST.in
  README.md
  setup.py
```

### setup.py

Contains metadata about application

```python
from setuptools import setup

setup(
    name='django-sample-application',
    version='0.1.0',
    author='John Doe',
    author_email='jdoe@umich.edu',
    packages=[
      'django-sample-application',
      'django-sample-application.test'
    ],
    url='http://pypi.python.org/pypi/django-sample-application/',
    license='LICENSE.txt',
    description='My sample application',
    long_description=open('README.txt').read(),
    install_requires=[
        "Django>=2",
        "requests>=2,<3",
    ],
)
```

### MANIFEST.in

By default, when a distribution is built only Python modules and packages are included. To include a README.md for instance, add this to the `MANIFEST.in`

```
include README.md
```

### [LICENSE.txt](https://choosealicense.com/)

Choose a license that fits your needs
