---
title: Django Application vs. Python Package
---

Both are a means for distributing software. Functionally, a Django application has some extra features:

- A standalone Django application is a Python package with a structure that resembles closely to a Django app
  - Can include things like `models.py`, `views.py`, etc.

- Makes it easier to include in an existing Django application
  - Install package with package manager, add dotted Python path to `INSTALLED_APPS` in `setup.py`
  - Add any app-specific settings to main `settings.py` file
