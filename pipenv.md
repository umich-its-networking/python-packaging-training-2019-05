---
title: Pipenv
---

Pipenv is a tool that combines `venv` and `pip` into a single interface. It replaces `pip`, `venv`, and `requirements.txt`, but does not replace `setup.py`. More on that later.

## Advantages
Why use Pipenv over `pip` and `venv`?
* Locks exact versions of packages for deterministic builds on build servers and between different developers.
* Resolves dependencies between different packages that require the same sub-package
* Consolidated interface is easier to reason about and remember
* Extra features: Pipenv supports development-only dependencies, vulnerability checking for the entire dependency tree, and more.

## Getting Started
Let's start by transitioning our project from `pip` and `venv` to using `Pipenv`.

Deactivate your venv and delete the files related to `pip` and `venv`:

```terminal
(venv) $ deactivate
$ rm -rf venv
```

Install `Pipenv` globally:

```terminal
$ pip3 install pipenv
Collecting pipenv
  Using cached https://files.pythonhosted.org/packages/13/b4/3ffa55f77161cff9a5220f162670f7c5eb00df52e00939e203f601b0f579/pipenv-2018.11.26-py3-none-any.whl
Requirement already satisfied: pip≥9.0.1 in /usr/local/lib/python3.7/site-packages (from pipenv) (19.0.2)
Collecting virtualenv-clone≥0.2.5 (from pipenv)
  Using cached https://files.pythonhosted.org/packages/ba/f8/50c2b7dbc99e05fce5e5b9d9a31f37c988c99acd4e8dedd720b7b8d4011d/virtualenv_clone-0.5.3-py2.py3-none-any.whl
Collecting virtualenv (from pipenv)
  Using cached https://files.pythonhosted.org/packages/4f/ba/6f9315180501d5ac3e707f19fcb1764c26cc6a9a31af05778f7c2383eadb/virtualenv-16.5.0-py2.py3-none-any.whl
Requirement already satisfied: certifi in /Users/jlost/Library/Python/3.7/lib/python/site-packages (from pipenv) (2019.3.9)
Requirement already satisfied: setuptools≥36.2.1 in /usr/local/lib/python3.7/site-packages (from pipenv) (40.8.0)
Installing collected packages: virtualenv-clone, virtualenv, pipenv
Successfully installed pipenv-2018.11.26 virtualenv-16.5.0 virtualenv-clone-0.5.3
```

Initialize `Pipenv`:

```terminal
$ pipenv --three
Creating a virtualenv for this project…
Pipfile: /Users/jlost/Projects/training/python-packaging-training-2019-05/package-training/Pipfile
Using /usr/local/bin/python3 (3.7.2) to create virtualenv…
⠙ Creating virtual environment...Using base prefix '/usr/local/Cellar/python/3.7.2_2/Frameworks/Python.framework/Versions/3.7'
New python executable in /Users/jlost/.local/share/virtualenvs/package-training-q2yrzzgZ/bin/python3.7
Also creating executable in /Users/jlost/.local/share/virtualenvs/package-training-q2yrzzgZ/bin/python
Installing setuptools, pip, wheel...
done.
Running virtualenv with interpreter /usr/local/bin/python3

✔ Successfully created virtual environment!
Virtualenv location: /Users/jlost/.local/share/virtualenvs/package-training-q2yrzzgZ
Creating a Pipfile for this project…
```

Take a look at the `Pipfile` it created:
```terminal
$ cat Pipfile
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]

[packages]

[requires]
python_version = "3.7"
```

This acts as a more robust `requirements.txt`. We can now simultaneously add our requirements to this file and install them with a single command:

```terminal
$ pipenv install "simplejson==3.16.0" "protobuf<=3"
Installing simplejson==3.16.0…
Adding simplejson to Pipfile's [packages]…
✔ Installation Succeeded
Installing protobuf<=3…
Adding protobuf to Pipfile's [packages]…
✔ Installation Succeeded
Pipfile.lock not found, creating…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
✔ Success!
Updated Pipfile.lock (8afc37)!
Installing dependencies from Pipfile.lock (8afc37)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 3/3 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

Let's look at our `Pipfile` now:

```terminal
$ cat Pipfile
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]

[packages]
simplejson = "==3.16.0"
protobuf = "<=3"

[requires]
python_version = "3.7"
```

Note that this time we added `protobuf<=3`. This means we are declaring that our project will work with any version of `protobuf` version 3 or earlier.

It also generated a `Pipfile.lock`:

```terminal
$ cat Pipfile.lock
{
    "_meta": {
        "hash": {
            "sha256": "9b491439b82bb2083b72dab3bbdaa58df0ca13ef0099fe44a392a8dd2c8afc37"
        },
        "pipfile-spec": 6,
        "requires": {
            "python_version": "3.7"
        },
        "sources": [
            {
                "name": "pypi",
                "url": "https://pypi.org/simple",
                "verify_ssl": true
            }
        ]
    },
    "default": {
        "protobuf": {
            "hashes": [
                "sha256:041dbeb8fdbf96aa834ed300ae9c0d3f5c00b299f91ba079a6266606a406461b",
                "sha256:1350de5993fbaff7f6736bb42c9f764dc6e2c32b9cd3ec1904f3ab0ed6caad0e",
                "sha256:739025378d552e05db6b2140b406876f645a45020ea7543b1f6ce6b5900848cb",
                "sha256:b799ba3ae9b3a742bac616963904cafc3465e0105ed9323e36dfe7d3a7ac0948",
                "sha256:b96de0b77126a9658026ba721a6152c748477f4875612527932853b24c425bf8",
                "sha256:e171eea1b6d8d0a21ea0f560ceb741e8e5cb72c6965cab4e928f01744b42f002",
                "sha256:ecc40bc30f1183b418fe0ec0c90bc3b53fa1707c4205ee278c6b90479e5b6ff5"
            ],
            "index": "pypi",
            "version": "==3.0.0"
        },
        "simplejson": {
            "hashes": [
                "sha256:067a7177ddfa32e1483ba5169ebea1bc2ea27f224853211ca669325648ca5642",
                "sha256:2fc546e6af49fb45b93bbe878dea4c48edc34083729c0abd09981fe55bdf7f91",
                "sha256:354fa32b02885e6dae925f1b5bbf842c333c1e11ea5453ddd67309dc31fdb40a",
                "sha256:37e685986cf6f8144607f90340cff72d36acf654f3653a6c47b84c5c38d00df7",
                "sha256:3af610ee72efbe644e19d5eaad575c73fb83026192114e5f6719f4901097fce2",
                "sha256:3b919fc9cf508f13b929a9b274c40786036b31ad28657819b3b9ba44ba651f50",
                "sha256:3dd289368bbd064974d9a5961101f080e939cbe051e6689a193c99fb6e9ac89b",
                "sha256:6c3258ffff58712818a233b9737fe4be943d306c40cf63d14ddc82ba563f483a",
                "sha256:75e3f0b12c28945c08f54350d91e624f8dd580ab74fd4f1bbea54bc6b0165610",
                "sha256:b1f329139ba647a9548aa05fb95d046b4a677643070dc2afc05fa2e975d09ca5",
                "sha256:ee9625fc8ee164902dfbb0ff932b26df112da9f871c32f0f9c1bcf20c350fe2a",
                "sha256:fb2530b53c28f0d4d84990e945c2ebb470edb469d63e389bf02ff409012fe7c5"
            ],
            "index": "pypi",
            "version": "==3.16.0"
        },
        "six": {
            "hashes": [
                "sha256:3350809f0555b11f552448330d0b52d5f24c91a322ea4a15ef22629740f3761c",
                "sha256:d16a0141ec1a18405cd4ce8b4613101da75da0e9a7aec5bdd4fa804d0e0eba73"
            ],
            "version": "==1.12.0"
        }
    },
    "develop": {}
}
```

Notice that even though we were abstract about which version of `protobuf` would work, an exact version (`==3.0.0`) was inserted into the lockfile, along with sha256 hashes to confirm that the file downloaded from PyPI is exactly the same version that was installed just a moment ago. This is what is meant by deterministic builds: Anyone else using `pipenv install` with this lockfile in place is guaranteed to install exactly the same files as you just did.

Adding dependencies with `pipenv install` works great for applications, but our project is both a library and an application. In order to be a library (a package), it still needs a `setup.py` with `install_requires`. Let's set things up in a way that doesn't duplicate the list of dependencies.

First, we'll `pipenv uninstall` the packages we just installed in order to remove them from the `Pipfile`. (We could also just delete the lines from the file, but this is a little bit simpler)

```terminal
$ pipenv uninstall protobuf simplejson
Uninstalling simplejson…
Uninstalling simplejson-3.0.0:
  Successfully uninstalled simplejson-3.0.0

Removing simplejson from Pipfile…
Uninstalling protobuf…
Uninstalling protobuf-3.0.0:
  Successfully uninstalled protobuf-3.0.0

Removing protobuf from Pipfile…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
✔ Success!
Updated Pipfile.lock (ad21a8)!
```

Our `Pipfile.lock` is empty once more.

```terminal
$ pipenv install -e .
Installing -e .…
Adding helloworld to Pipfile's [packages]…
✔ Installation Succeeded
Pipfile.lock (ad21a8) out of date, updating to (a65489)…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
✔ Success!
Updated Pipfile.lock (ad21a8)!
Installing dependencies from Pipfile.lock (ad21a8)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 4/4 — 00:00:01
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

Running `pipenv install -e .` did the following:
* Installed dependencies from the `setup.py`
* Generated a `Pipfile.lock` with all of the dependencies that were installed
* Installed the current package (helloworld) in editable mode as we did in the `pip` chapter. Updates to our source code will now take effect in the environment immediately, as long as we're inside of our virtual environment.

When `pipenv install` installed the dependencies, it installed them in a virtual environment that is outside of your current directory. You'll have to use your virtual environment in order to access those dependencies.

There are two ways you can use your virtual environment:
1. `pipenv shell` is equivalent to `activate`, and `exit` is equivalent to `deactivate`.
2. Use `pipenv run <command>` to run a one-off command in the venv:

```terminal
$ pipenv run helloworld
Sup World
```

Now that we have an idea of how we can package and install libaries, we can look at how the implementation differs in a [Django package]({{ "/advanced/packaging-web-applications" | relative_url }}).
