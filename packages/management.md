---
title: Package Management
---

## [pip](https://pip.pypa.io/en/stable/quickstart/)

- Default package installer; comes included with Python in latest versions
- Installs from [pypi.org]()
- requirements.txt

### Use

```bash
pip install requests
```

## [venv](https://docs.python.org/3/library/venv.html), [virtualenv](https://virtualenv.pypa.io/en/latest/)

- Use venv if using Python 3, otherwise virtualenv
- Creates isolated environment for Python projects
- Dependencies are installed within a local directory

### Use:

```bash
# within project dir

virtualenv env # if Python 2
python3 -m venv env # if Python 3
source env/bin/activate

# deactivate
deactivate
```

## [pipenv](https://pipenv.readthedocs.io/en/latest/)

- Combines pip and virtualenv
- `Pipfile` and `Pipfile.lock` to enforce a consistent working environment for all developers

### Use

```bash
pipenv install requests
```
