---
title: Privately Distributing a Package
---

If you think your package is only suited to internal distribution, the simplest option is to add an [annotated tag](https://docs.gitlab.com/ee/university/training/topics/tags.html) to your repository.

```terminal
$ git tag -a v1.0.0 -m "Message briefly describing version"
$ git push origin v1.0.0
```

Anyone with access to your repository can now [pip install](https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support) it:

```terminal
$ pip install git://gitlab.umich.edu/<project>.git@v1.0.0
```

Or alternatively [add it to their Pipfile](https://docs.pipenv.org/en/latest/basics/#a-note-about-vcs-dependencies):

```terminal
$ pipenv install -e git@gitlab.umich.edu:<group>/<project>.git@v1.0.0#egg=<package_name>
```
