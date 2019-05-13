---
title: Introduction
---

You’ve got some useful Python scripts. Your colleagues want to make use of some or all of the code you’ve written. How do you get it to them? You could email it to them. (No.) You could put it in a git repository and send them the URL. (Better.) But then what do they do with it? Clone it, then copy the modules or functions that are useful for them into their code? Think about adding it to their repo as a submodule? (No.) What happens when you improve your code to fix a bug or add a feature? Learn how to factor your code so that it’s reusable & learn how to package it so that it’s easy to share with others. In this session we’ll talk about several tools and patterns: pip, requirements.txt, setup.py, pipenv, and PyPI.

To begin our tour of tools, open up a terminal window and create a new directory:
```terminal
$ mkdir package-training
$ cd package-training
```
Note that Windows users may need to adapt some commands to their shell of choice.

[Next: pip install]({{ "/pip-install" | relative_url }})
