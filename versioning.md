---
title: Versioning
---

Let's take a look at the version number in your `setup.py`:
```
version='0.1.0'
```

As a consumer of libraries, you are probably aware of the risk of upgrading your project's packages. Some releases might only patch bugs. Some might introduce new features. Some might break, remove, or change old features that you relied on! If only there were some way you could communicate the safety of an upgrade to your co-workers without writing exhaustive patch notes...

Enter [semantic versioning](https://semver.org/).

> Given a version number MAJOR.MINOR.PATCH, increment the:
>
> MAJOR version when you make incompatible API changes,
> MINOR version when you add functionality in a backwards-compatible manner, and
> PATCH version when you make backwards-compatible bug fixes.

Following these rules will increase your team's trust in your releases, and tools like Pipenv take advantage of *semver* by including features to lock packages to e.g. the latest PATCH or MINOR version.
