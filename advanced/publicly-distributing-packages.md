---
title: Publicly Distributing a Package Through PyPi
---

This tutorial follows the [packaging web application guide]({{ "/advanced/packaging-web-applications" | relative_url }}) and shows how a distribution can be uploaded to PyPi for public use

## (Optional) Upload to Test PyPi for Experimentation Purposes

Uploading to Test PyPi won't affect the real index, since its repository is separate from PyPi

1. Create an account for [Test PyPi](https://test.pypi.org/account/register/)

2. Install Twine for interacting with PyPi

```terminal
$ python -m pip install --user --upgrade twine
python -m pip install --user --upgrade twine
Collecting twine
  Downloading https://files.pythonhosted.org/packages/28/90/59eec88c0b2ac9e47fe135959007acb93a3cc9f7146366e11fecf718dd15/twine-1.13.0-py2.py3-none-any.whl
Requirement already satisfied, skipping upgrade: setuptools>=0.7.0 in /usr/local/lib/python3.7/site-packages (from twine) (40.8.0)
Collecting tqdm>=4.14 (from twine)
  Downloading https://files.pythonhosted.org/packages/6c/4b/c38b5144cf167c4f52288517436ccafefe9dc01b8d1c190e18a6b154cd4a/tqdm-4.31.1-py2.py3-none-any.whl (48kB)
    100% |████████████████████████████████| 51kB 2.3MB/s
Collecting requests!=2.15,!=2.16,>=2.5.0 (from twine)
  Downloading https://files.pythonhosted.org/packages/7d/e3/20f3d364d6c8e5d2353c72a67778eb189176f08e873c9900e10c0287b84b/requests-2.21.0-py2.py3-none-any.whl (57kB)
    100% |████████████████████████████████| 61kB 8.0MB/s
Collecting readme-renderer>=21.0 (from twine)
  Downloading https://files.pythonhosted.org/packages/c3/7e/d1aae793900f36b097cbfcc5e70eef82b5b56423a6c52a36dce51fedd8f0/readme_renderer-24.0-py2.py3-none-any.whl
Collecting pkginfo>=1.4.2 (from twine)
  Downloading https://files.pythonhosted.org/packages/e6/d5/451b913307b478c49eb29084916639dc53a88489b993530fed0a66bab8b9/pkginfo-1.5.0.1-py2.py3-none-any.whl
Collecting requests-toolbelt!=0.9.0,>=0.8.0 (from twine)
  Downloading https://files.pythonhosted.org/packages/60/ef/7681134338fc097acef8d9b2f8abe0458e4d87559c689a8c306d0957ece5/requests_toolbelt-0.9.1-py2.py3-none-any.whl (54kB)
    100% |████████████████████████████████| 61kB 7.6MB/s
Collecting chardet<3.1.0,>=3.0.2 (from requests!=2.15,!=2.16,>=2.5.0->twine)
  Downloading https://files.pythonhosted.org/packages/bc/a9/01ffebfb562e4274b6487b4bb1ddec7ca55ec7510b22e4c51f14098443b8/chardet-3.0.4-py2.py3-none-any.whl (133kB)
    100% |████████████████████████████████| 143kB 4.6MB/s
Collecting idna<2.9,>=2.5 (from requests!=2.15,!=2.16,>=2.5.0->twine)
  Downloading https://files.pythonhosted.org/packages/14/2c/cd551d81dbe15200be1cf41cd03869a46fe7226e7450af7a6545bfc474c9/idna-2.8-py2.py3-none-any.whl (58kB)
    100% |████████████████████████████████| 61kB 12.1MB/s
Collecting certifi>=2017.4.17 (from requests!=2.15,!=2.16,>=2.5.0->twine)
  Downloading https://files.pythonhosted.org/packages/60/75/f692a584e85b7eaba0e03827b3d51f45f571c2e793dd731e598828d380aa/certifi-2019.3.9-py2.py3-none-any.whl (158kB)
    100% |████████████████████████████████| 163kB 4.0MB/s
Collecting urllib3<1.25,>=1.21.1 (from requests!=2.15,!=2.16,>=2.5.0->twine)
  Downloading https://files.pythonhosted.org/packages/01/11/525b02e4acc0c747de8b6ccdab376331597c569c42ea66ab0a1dbd36eca2/urllib3-1.24.3-py2.py3-none-any.whl (118kB)
    100% |████████████████████████████████| 122kB 16.2MB/s
Collecting Pygments (from readme-renderer>=21.0->twine)
  Downloading https://files.pythonhosted.org/packages/6e/00/c5cb5fc7c047da4af049005d0146b3a961b1a25d9cefbbe24bf0882a11ad/Pygments-2.4.0-py2.py3-none-any.whl (882kB)
    100% |████████████████████████████████| 890kB 9.2MB/s
Collecting six (from readme-renderer>=21.0->twine)
  Downloading https://files.pythonhosted.org/packages/73/fb/00a976f728d0d1fecfe898238ce23f502a721c0ac0ecfedb80e0d88c64e9/six-1.12.0-py2.py3-none-any.whl
Collecting docutils>=0.13.1 (from readme-renderer>=21.0->twine)
  Downloading https://files.pythonhosted.org/packages/36/fa/08e9e6e0e3cbd1d362c3bbee8d01d0aedb2155c4ac112b19ef3cae8eed8d/docutils-0.14-py3-none-any.whl (543kB)
    100% |████████████████████████████████| 552kB 11.4MB/s
Collecting bleach>=2.1.0 (from readme-renderer>=21.0->twine)
  Downloading https://files.pythonhosted.org/packages/ab/05/27e1466475e816d3001efb6e0a85a819be17411420494a1e602c36f8299d/bleach-3.1.0-py2.py3-none-any.whl (157kB)
    100% |████████████████████████████████| 163kB 16.1MB/s
Collecting webencodings (from bleach>=2.1.0->readme-renderer>=21.0->twine)
  Downloading https://files.pythonhosted.org/packages/f4/24/2a3e3df732393fed8b3ebf2ec078f05546de641fe1b667ee316ec1dcf3b7/webencodings-0.5.1-py2.py3-none-any.whl
Installing collected packages: tqdm, chardet, idna, certifi, urllib3, requests, Pygments, six, docutils, webencodings, bleach, readme-renderer, pkginfo, requests-toolbelt, twine
  The script tqdm is installed in '/root/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  The script chardetect is installed in '/root/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  The script pygmentize is installed in '/root/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  The script pkginfo is installed in '/root/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  The script twine is installed in '/root/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed Pygments-2.4.0 bleach-3.1.0 certifi-2019.3.9 chardet-3.0.4 docutils-0.14 idna-2.8 pkginfo-1.5.0.1 readme-renderer-24.0 requests-2.21.0 requests-toolbelt-0.9.1 six-1.12.0 tqdm-4.31.1 twine-1.13.0 urllib3-1.24.3 webencodings-0.5.1
```

3. Upload distribution(s) to Test PyPi

```terminal
$ python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*
Enter your username: username
Enter your password:
Uploading distributions to https://test.pypi.org/legacy/
Uploading django-polls-0.1.tar.gz
100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 10.3k/10.3k [00:00<00:00, 18.9kB/s]
```

4. Try installing from Test PyPi

```terminal
$ pip install --index-url https://test.pypi.org/simple/ --no-deps django-polls
```

## Upload to PyPi

1. Create an account for [PyPi](https://pypi.org/account/register/)

2. Upload distribution(s)

```terminal
$ python -m twine upload dist/*
```

3. Install from PyPi

```terminal
$ pip install django-polls
```
