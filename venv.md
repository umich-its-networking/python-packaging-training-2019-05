---
title: VENV
---

## More Projects, More Problems
In the previous section, we encountered a couple of issues:
* Users might need to have multiple versions of Python installed for different projects and packages.
* Users might need to have multiple versions of a package installed, but `pip install` installed them globally.

Ideally, the version of Python and all installed dependencies could be set on a per-project basis. With *virtual environments*, we can turn this lofty ideal into a reality.

First, let's see which `python` you are using:

```terminal
$ which python
/usr/local/bin/python
$ python --version
Python 2.7.15
```

Next, create a virtual environment (venv) in the `venv` directory:

```terminal
$ python3 -m venv venv
```

See what's in the `venv` directory:

```terminal
$ ls -la venv
total 8
drwxr-xr-x   6 jlost  UMROOT\Domain Users  204 May  8 10:23 .
drwxr-xr-x   5 jlost  UMROOT\Domain Users  170 May  8 10:23 ..
drwxr-xr-x  12 jlost  UMROOT\Domain Users  408 May  8 10:23 bin
drwxr-xr-x   2 jlost  UMROOT\Domain Users   68 May  8 10:23 include
drwxr-xr-x   3 jlost  UMROOT\Domain Users  102 May  8 10:23 lib
-rw-r--r--   1 jlost  UMROOT\Domain Users   75 May  8 10:23 pyvenv.cfg
$ ls -la venv/bin
total 80
drwxr-xr-x  12 jlost  UMROOT\Domain Users   408 May  8 10:23 .
drwxr-xr-x   6 jlost  UMROOT\Domain Users   204 May  8 10:23 ..
-rw-r--r--   1 jlost  UMROOT\Domain Users  2262 May  8 10:23 activate
-rw-r--r--   1 jlost  UMROOT\Domain Users  1318 May  8 10:23 activate.csh
-rw-r--r--   1 jlost  UMROOT\Domain Users  2470 May  8 10:23 activate.fish
-rwxr-xr-x   1 jlost  UMROOT\Domain Users   316 May  8 10:23 easy_install
-rwxr-xr-x   1 jlost  UMROOT\Domain Users   316 May  8 10:23 easy_install-3.7
-rwxr-xr-x   1 jlost  UMROOT\Domain Users   298 May  8 10:23 pip
-rwxr-xr-x   1 jlost  UMROOT\Domain Users   298 May  8 10:23 pip3
-rwxr-xr-x   1 jlost  UMROOT\Domain Users   298 May  8 10:23 pip3.7
lrwxr-xr-x   1 jlost  UMROOT\Domain Users     7 May  8 10:23 python -> python3
lrwxr-xr-x   1 jlost  UMROOT\Domain Users    22 May  8 10:23 python3 -> /usr/local/bin/python3
```

Interesting -- in `venv/bin` we have symbolic links from `python` to our system's `python3`, some `pip` files that are essentially shortcuts to a particular version of `pip`, and a script called `activate`. Let's try running `activate`.

```terminal
$ source ./venv/bin/activate
```

Notice which versions of `python` and `pip` are now in our environment:

```terminal
(venv) $ which python
/Users/jlost/Projects/training/python-packaging-training-2019-05/package-training/venv/bin/python
(venv) $ python --version
Python 3.7.2
(venv) $ which pip
/Users/jlost/Projects/training/python-packaging-training-2019-05/package-training/venv/bin/pip
(venv) $ pip --version
pip 18.1 from /Users/jlost/Projects/training/python-packaging-training-2019-05/package-training/venv/lib/python3.7/site-packages/pip (python 3.7)
```

We installed some packages in the previous tutorial. Let's see if we can find them.

```terminal
(venv) $ pip show protobuf
(venv) $ pip list
Package    Version
---------- -------
pip        18.1
setuptools 40.6.2
```

As you can see, we're now working with a clean slate. We can follow these steps for any project to have an isolated environment with exactly the Python and package versions we need.

If we run `exit`, any packages we install in this `venv` will disappear until we run `source ./venv/bin/activate` again.

So far, we have learned the basics of tools that allow yourself and others to manage and use the dependencies of your project in a way that is isolated from all other projects.

What if you wanted to share your code with your team or the general public, similarly to how the authors of `protobuf` and `simplejson` shared theirs? We will approach that in the [next section, A Simple Package]({{ "/simple-package" | relative_url }}).
