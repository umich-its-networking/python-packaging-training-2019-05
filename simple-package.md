---
title: A Simple Package
---

We want to create a basic package that can be installed via `pip`. As a thought exercise, let's first search `PyPI` for the package `protobuf` and see what turns up:

```terminal
(venv) $ pip3 search protobuf
protobuf-gis (1.0.3)                         - GIS ProtoBuf module
protobuf-extra (0.5.2)                       - Extra tools for Protobuf and Python
protobuf-ntypes (1.3.0)                      - protobuf nilable data structures
machinetalk-protobuf (1.1.0)                 - Protobuf Python modules for machinetalk
corenlp-protobuf (3.8.0)                     - Python bindings for Stanford CoreNLP protobufs
uplink-protobuf (0.1.0)                      - Protocol Buffers (Protobuf) support for Uplink.
protobuf-gen (0.0.4)                         - Python 3 type hinted protobuf binding generator
mypy-protobuf (1.10)                         - Generate mypy stub files from protobuf specs
(...)
```

The packages that it found have a name, a version, and a description. Where is that data coming from? If we want to create a package as well, don't we also need to specify that information?

Shockingly, the answer is *yes*.

The core of a Python package is `setup.py`. Let's create that file:

```terminal
(venv) $ $EDITOR setup.py
```

```python
from setuptools import setup

setup(
    name='helloworld',
    version='0.1.0',
    description='Writes the words Hello World to STDOUT.',
    author='Max Powers',
    packages=['helloworld'],
    entry_points={ # Optional - allows running helloworld from command line
        'console_scripts': ['helloworld=helloworld.hello:greet'],
    },
    install_requires=[
        'simplejson==3.0.0',
        'protobuf',
    ],
)
```

According to this file, we are distributing a package `helloworld`. We will create that package with a little bit of source code.

```terminal
(venv) $ mkdir helloworld
(venv) $ touch helloworld/__init__.py
(venv) $ $EDITOR helloworld/hello.py
```

`hello.py`:

```python
def greet():
    print('Hello World')

def main(args=None):
    greet()

if __name__ == "__main__":
    main()
```

Now that we have made a simple package, `pip` can install it from the current directory:

```terminal
(venv) $ pip install -e .
Processing /Users/jlost/Projects/training/python-packaging-training-2019-05/package-training
Collecting simplejson==3.0.0 (from helloworld==0.1.0)
Collecting protobuf (from helloworld==0.1.0)
  Using cached https://files.pythonhosted.org/packages/d7/08/a316e74d41a1f3d606dfc3b71cc068354e8b9a0232f46bc098aa50b37116/protobuf-3.7.1-cp37-cp37m-macosx_10_9_intel.macosx_10_9_x86_64.macosx_10_10_intel.macosx_10_10_x86_64.whl
Collecting six≥1.9 (from protobuf-＞helloworld==0.1.0)
  Downloading https://files.pythonhosted.org/packages/73/fb/00a976f728d0d1fecfe898238ce23f502a721c0ac0ecfedb80e0d88c64e9/six-1.12.0-py2.py3-none-any.whl
Requirement already satisfied: setuptools in ./venv/lib/python3.7/site-packages (from protobuf-＞helloworld==0.1.0) (40.6.2)
Installing collected packages: simplejson, six, protobuf, helloworld
  Running setup.py install for helloworld ... done
Successfully installed helloworld-0.1.0 protobuf-3.7.1 simplejson-3.0.0 six-1.12.0
```

Notice that installing your package also caused `pip` to install all of the dependencies that were specified in `setup.py`. Why specify the same list of requirements in two places? Delete the redundant file.

```terminal
(venv) $ rm requirements.txt
```

Open up a Python REPL to try out your package:

```terminal
(venv) $ python
Python 3.7.2 (default, Feb 12 2019, 08:16:38)
[Clang 10.0.0 (clang-1000.11.45.5)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from helloworld.hello import greet
>>> greet()
Hello World
```

Because we included an `entry_points` with `console_scripts`, we can also use it from the command line:

```terminal
(venv) $ which helloworld
/Users/jlost/Projects/training/python-packaging-training-2019-05/package-training/venv/bin/helloworld
(venv) $ helloworld
Hello World
```

We can also execute it as a module!

```terminal
(venv) $ python -m helloworld.hello
Hello World
```

Because we used the `-e` flag in `pip install -e`, changes to your files will immediately take effect in your environment. Try making a minor change to `hello.py`:

```terminal
(venv) $ $EDITOR helloworld/hello.py
```

`hello.py`:

```python
def greet():
    print('Sup World?') # Changed string

def main(args=None):
    greet()

if __name__ == "__main__":
    main()
```

Now we run it again to compare the output:

```terminal
(venv) $ helloworld
Sup World
```

We managed to create a library with a single method, `greet`, which can also be used as a command line application. In doing so you learned about `pip`, `requirements.txt`, `setup.py`, `venv` and package structure. Now move on to the [next section, Pipenv]({{ "/pipenv" | relative_url }}).
