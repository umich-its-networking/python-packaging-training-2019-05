---
title: Distributing Your Package
---

## Public Use

Create a single `tar.gz` or `.zip` package in `dist/` with the version number specified in `setup.py`

```python
python setup.py sdist
```

### (Optional) Upload Your Distribution Archive

```bash
python -m pip install --user --upgrade twine

# to upload all dists to test.pypi
python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*

# when ready, upload to pypi
python -m twine upload dist/*
```

### Installing a Package

```bash
# from test.pypi
python -m pip install --index-url https://test.pypi.org/simple/ --no-deps django-sample-application
```

```bash
# from local distribution
python -m pip install /dist/django-sample-application-0.1.0.tar.gz
```

## Private Use

TODO
