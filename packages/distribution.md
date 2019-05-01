---
title: Distributing Your Package
---

# Building Distribution Files
Now that your library is configured with a `setup.py`, you can generate package files to share with others:

```python
python setup.py sdist
```

This will create a single `tar.gz` or `.zip` package in `dist/` with the version number specified in `setup.py`

Speaking of version numbers...

## Versioning

Let's take a look at the version number in your `setup.py`:
```
version='0.1.0'
```

As a consumer of libraries, you are probably aware of the risk of upgrading your project's packages. Some releases might only patch bugs. Some might introduce new features. Some might break, remove, or change old features that you relied on! If only there were some way you could communicate the safety of an upgrade to your co-workers without writing exhaustive patch notes...

Enter [semantic versioning](https://semver.org/).

> Given a version number MAJOR.MINOR.PATCH, increment the:

> MAJOR version when you make incompatible API changes,
> MINOR version when you add functionality in a backwards-compatible manner, and
> PATCH version when you make backwards-compatible bug fixes.

Following these rules will increase your team's trust in your releases, and tools like Pipenv take advantage of *semver* by including features to lock packages to e.g. the latest PATCH or MINOR version.

### Publicly Distribute Your Package
Is your package fit for public consumption? Is it free of secrets, connection strings, and other information that should stay within the University? If so, it's time to take the plunge. Follow these steps to upload your package to PyPI:

```bash
python -m pip install --user --upgrade twine

# to upload all dists to test.pypi
python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*

# when ready, upload to pypi
python -m twine upload dist/*
```

### Privately Distribute Your Package
If you think your package is only suited to internal distribution, the simplest option is to add an [annotated tag](https://docs.gitlab.com/ee/university/training/topics/tags.html) to your repository. 
```
git tag -a v1.0.0 -m "Message briefly describing version"
git push origin v1.0.0
```

Anyone with access to your repository can now [add it to their Pipfile](https://docs.pipenv.org/en/latest/basics/#a-note-about-vcs-dependencies):
```
pipenv install -e git@gitlab.umich.edu:<group>/<project>.git@v1.0.0#egg=<package_name>
```

### Installing a Package
Finally, you or your coworkers can now use your package by...

...Installing from PyPI, if you decided to upload it to PyPI:
```bash
# from test.pypi
python -m pip install --index-url https://test.pypi.org/simple/ --no-deps django-sample-application
```

...Or installing it from a file:
```bash
# from local distribution
python -m pip install /dist/django-sample-application-0.1.0.tar.gz
```
