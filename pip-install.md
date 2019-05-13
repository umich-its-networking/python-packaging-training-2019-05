---
title: Pip Basics
---

Let's start by taking a look at your environment:

```terminal
$ which pip
/usr/local/bin/pip
$ pip --version
pip 18.0 from /usr/local/lib/python2.7/site-packages/pip (python 2.7)
$ which pip3
/usr/local/bin/pip3
$ pip3 --version
pip 19.0.2 from /usr/local/lib/python3.7/site-packages/pip (python 3.7)
```

This is my `pip` installation. There are many like it, but this one is mine. If you also have `pip` as well as `pip3`, you should use `pip3` in this section.

If you happen to be missing `pip`, try accessing it via:

```terminal
$ python -m pip --version
pip 18.0 from /usr/local/lib/python2.7/site-packages/pip (python 2.7)
$ python3 -m pip --version
pip 19.0.2 from /usr/local/lib/python3.7/site-packages/pip (python 3.7)
```

If you can only access `pip` via `python -m pip`, that is no problem. Simply replace the `pip3` commands in this section with that from here on out.

Already it is apparent that users may have different Python installations with different versions of packages, such as `pip`. Let's come back to that later.

# A Package Installer
Pip lets you install packages from a file system, Git, or PyPI. [PyPI is the Python Package Index](https://pypi.org/), and it is the most popular place to store and distribute public Python packages. 

```terminal
$ pip3 install simplejson
Collecting simplejson
  Downloading https://files.pythonhosted.org/packages/e3/24/c35fb1c1c315fc0fffe61ea00d3f88e85469004713dab488dee4f35b0aff/simplejson-3.16.0.tar.gz (81kB)
    100% |████████████████████████████████| 81kB 3.8MB/s
Building wheels for collected packages: simplejson
  Building wheel for simplejson (setup.py) ... done
  Stored in directory: /Users/jlost/Library/Caches/pip/wheels/5d/1a/1e/0350bb3df3e74215cd91325344cc86c2c691f5306eb4d22c77
Successfully built simplejson
Installing collected packages: simplejson
Successfully installed simplejson-3.16.0
$ pip3 show simplejson
Name: simplejson
Version: 3.16.0
Summary: Simple, fast, extensible JSON encoder/decoder for Python
Home-page: https://github.com/simplejson/simplejson
Author: Bob Ippolito
Author-email: bob@redivi.com
License: MIT License
Location: /usr/local/lib/python3.7/site-packages
Requires:
Required-by:
```

We just installed version 3.16.0 of `simplejson`. Great. What if we need an earlier version?

```terminal
$ pip3 install simplejson==3.0.0
Collecting simplejson==3.0.0
  Downloading https://files.pythonhosted.org/packages/e5/68/01d518b9b9b3931b142ac35ffe12cc8d819bef064f0b9baccc78a637193d/simplejson-3.0.0.tar.gz (57kB)
    100% |████████████████████████████████| 61kB 2.3MB/s
Building wheels for collected packages: simplejson
  Building wheel for simplejson (setup.py) ... done
  Stored in directory: /Users/jlost/Library/Caches/pip/wheels/b3/43/bd/d56048d59a97a95e8d7c34a60005b53e15e207f2c0a3048487
Successfully built simplejson
Installing collected packages: simplejson
  Found existing installation: simplejson 3.16.0
    Uninstalling simplejson-3.16.0:
      Successfully uninstalled simplejson-3.16.0
Successfully installed simplejson-3.0.0
$ pip3 show simplejson
Name: simplejson
Version: 3.0.0
Summary: Simple, fast, extensible JSON encoder/decoder for Python
Home-page: http://github.com/simplejson/simplejson
Author: Bob Ippolito
Author-email: bob@redivi.com
License: MIT License
Location: /usr/local/lib/python3.7/site-packages
Requires:
Required-by:
```

We just replaced our 3.16.0 version with a 3.0.0 version. But what if we had two projects that needed two different versions? Again, we'll come back to that later.

 Many projects require a laundry list of packages. Luckily, you can list all of them in a single file and then install with a single command:

 ```terminal
$ echo simplejson==3.16.0 >> requirements.txt
$ echo protobuf >> requirements.txt
$ cat requirements.txt
simplejson==3.16.0
protobuf
$ pip3 install -r requirements.txt
Collecting simplejson==3.16.0 (from -r requirements.txt (line 1))
Collecting protobuf (from -r requirements.txt (line 2))
  Downloading https://files.pythonhosted.org/packages/d7/08/a316e74d41a1f3d606dfc3b71cc068354e8b9a0232f46bc098aa50b37116/protobuf-3.7.1-cp37-cp37m-macosx_10_9_intel.macosx_10_9_x86_64.macosx_10_10_intel.macosx_10_10_x86_64.whl (1.3MB)
    100% |████████████████████████████████| 1.3MB 15.9MB/s
Requirement already satisfied: setuptools in /usr/local/lib/python3.7/site-packages (from protobuf-≥-r requirements.txt (line 2)) (40.8.0)
Requirement already satisfied: six≥1.9 in /usr/local/lib/python3.7/site-packages (from protobuf-≥-r requirements.txt (line 2)) (1.11.0)
Installing collected packages: simplejson, protobuf
  Found existing installation: simplejson 3.0.0
    Uninstalling simplejson-3.0.0:
      Successfully uninstalled simplejson-3.0.0
Successfully installed protobuf-3.7.1 simplejson-3.16.0
```

In the [next section, Virtual Environments]({{ "/venv" | relative_url }}), we will tackle some of the environmental and dependency issues that we encountered.
