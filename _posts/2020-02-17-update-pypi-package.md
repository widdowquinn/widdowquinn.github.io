---
title: "Updating a package on pypi"
categories: Coding
tags: [python, pypi, packaging, github]
toc: true
toc_label: "Table of Contents"
toc_icon: "book-reader"
toc_sticky: true
---

Detailed instructions can be found [here](https://packaging.python.org/tutorials/packaging-projects/)
{: .notice--info}

Suppose:

- You have updated a Python package, for example to add a feature or fix a bug
- You have an up-to-date local repository and have pushed all changes to `GitHub`
- You have incremented the version number for the package
- You have accounts on [`pypi`](https://pypi.org/) and [`test.pypi`](https://test.pypi.org/)

You will need to have in your repository (see link above):

- a suitably-configured `setup.py` file
- a `README.md` file (this will be your `pypi` documentation page)
- a `LICENSE` file
- If these are not present, add them now

## 1: Update local packages for distribution

```bash
python -m pip install --user --upgrade setuptools wheel
python -m pip install --user --upgrade twine
```

### 2: Create distribution packages on your local machine, and check the `dist/` directory for the new version files

```bash
python setup.py sdist bdist_wheel
ls dist
```

### 3: Upload the distribution files to `pypi`'s test server

```bash
python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```

- Check the upload on the `test.pypi` server
    - [https://test.pypi.org/project/PACKAGE/VERSION/](https://test.pypi.org/project/<PACKAGE>/<VERSION>)

### 4: Test the upload with a local installation

Create a new test environment
{: .notice--primary}

```bash
conda create --name test_pypi python=3.8
```

- Install your package from the test server

```bash
python -m pip install --index-url https://test.pypi.org/simple/ --no-deps <PACKAGE>
```

    - Start Python, import the package, and test the version

### 5: Upload the distribution files to `pypi`

```bash
python -m twine upload dist/*
```

- Check the upload at `pypi`
    - [https://pypi.org/project/<PACKAGE>/<VERSION>/](https://pypi.org/project/<PACKAGE>/<VERSION>/)