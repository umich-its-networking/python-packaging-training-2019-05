---
title: VENV
---

```terminal
$ which python
/usr/local/bin/python
```

Create the virtual environment
```terminal
$ python3 -m venv venv
```

See what's in the venv directory
```terminal
$ cd venv
$ ls -la
total 8
drwxr-xr-x   6 steinhof  1410742483  192 May  7 15:34 .
drwxr-xr-x   3 steinhof  1410742483   96 May  7 15:34 ..
drwxr-xr-x  12 steinhof  1410742483  384 May  7 15:34 bin
drwxr-xr-x   2 steinhof  1410742483   64 May  7 15:34 include
drwxr-xr-x   3 steinhof  1410742483   96 May  7 15:34 lib
-rw-r--r--   1 steinhof  1410742483   75 May  7 15:34 pyvenv.cfg
```

Activate the ewnvironment

```terminal
$ source ./venv/bin/activate
```

Notice what oythin executable you're using...

```terminal
$ which python
/Users/steinhof/Desktop/demo/venv/bin/python
```
