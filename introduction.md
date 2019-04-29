---
title: Introduction
---

You’ve got some useful Python scripts. Your colleagues want to make use of some or all of the code you’ve written. How do you get it to them? You could email it to them. (No.) You could put it in a git repository and send them the URL. (Better.) But then what do they do with it? Clone it, then copy the modules or functions that are useful for them into their code? Think about adding it to their repo as a submodule? (No.) What happens when you improve your code to fix a bug or add a feature? Learn how to factor your code so that it’s reusable & learn how to package it so that it’s easy to share with others. In this session we’ll talk about several tools and patterns: pip, requirements.txt, setup.py, pipenv, and PyPI.

## Recon: Application or Library?

### Applications...
* Are run externally from a command line, executable, or web server.
* Typically have a main entry point (`__main__`)

Examples:
* A full Django project
* An ETL or batch job
* A command-line tool

### Libraries...
* Are used from a programming language
* Often do not have a main entry point, and if it does have one, it is not the main purpose of the codebase

Examples:
* A wrapper to simplify the use of a web service
* A module with methods codifying business rules that should be shared with other developers in your unit
* A plugin that will help your coworkers set up single sign-on in your web framework of choice
* A Django App (distinct from a project)

### Or both?!
It sometimes makes sense for a program to be both an application *and* a library. For example, if you made a wrapper to simplify using a web service, it might only take a little bit more work to add a command-line interface that allows you to quickly and conveniently perform common tasks. But beware, as a large application that is tightly coupled to methods you want to share as a library might be a sign that some refactoring is in order.

***
Next, we will examine tools and strategies for sharing programs as [applications](./applications.md), sharing them as [libraries](./libraries.md), and how those tools can be used together in harmony.
