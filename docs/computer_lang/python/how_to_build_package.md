---
layout: default
title: How to build the package
nav_order: 3
parent: python
grand_parent: Computer Language
---

# How to build the package
---

## python project structure

    packaging_tutorial/
    ├── LICENSE
    ├── pyproject.toml
    ├── README.md
    ├── src/
    │   └── example_package_YOUR_USERNAME_HERE/
    │       ├── __init__.py
    │       └── example.py
    └── tests/

## Inside pyproject.toml 

```toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "example_package_YOUR_USERNAME_HERE"
version = "0.0.1"
authors = [
  { name="Example Author", email="author@example.com" },
]
description = "A small example package"
readme = "README.md"
requires-python = ">=3.7"
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

[project.urls]
"Homepage" = "https://github.com/pypa/sampleproject"
"Bug Tracker" = "https://github.com/pypa/sampleproject/issues"
```
    
## Install build file

```python
python3 -m pip install --upgrade build
```
## Build

```bash
    python3 -m build
```
will create a dist directory

## Uploading the distribution

### Create an test account

    https://test.pypi.org/account/register

### Install twine
    python3 -m pip install --upgrade twine

### Config API key

    add apikye to .pypirc

    [testpypi]
    username = __token__
    password = pypi-Ag...

### Upload
```bash
python3 -m twine upload --repository testpypi dist/*
```

### Install package

```bash
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-package-YOUR-USERNAME-HERE
```
