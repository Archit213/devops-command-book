# Application Basics: Python Infrastructure
------------------------------------------------------------------------

# Table of Contents

-   What is Python?
-   Python 2 vs Python 3
-   What is pip?
-   Requirements File
-   Command Reference
-   Practical Exercises
-   Best Practices
-   Common Mistakes
-   Interview Questions

------------------------------------------------------------------------

# What is Python?

Python is a high-level, interpreted programming language widely used in
automation, DevOps, scripting, cloud engineering, AI, and web
development.

In DevOps, Python is commonly used to automate infrastructure, write
deployment scripts, and interact with cloud APIs.

------------------------------------------------------------------------

# Python 2 vs Python 3

  Python 2         Python 3
  ---------------- ----------------------------
  Legacy version   Current supported version
  End of Life      Actively maintained
  Older syntax     Modern syntax and features

Always prefer **Python 3** for new projects.

------------------------------------------------------------------------

# What is pip?

`pip` is Python's package manager. It installs, upgrades, removes, and
manages packages from the Python Package Index (PyPI).

------------------------------------------------------------------------

# requirements.txt

A `requirements.txt` file lists all Python dependencies required by a
project. It allows developers and CI/CD pipelines to recreate the same
environment.

Example:

``` text
Flask==2.3.2
requests==2.32.0
```

------------------------------------------------------------------------

# Command Reference

## 1. Check Python Version

``` bash
python2 -V
python3 -V
```

Displays the installed Python version.

Example:

``` bash
python3 -V
```

Expected Output:

``` text
Python 3.12.0
```

------------------------------------------------------------------------

## 2. Run a Python Script

``` bash
python3 app.py
```

Executes a Python application.

------------------------------------------------------------------------

## 3. Check pip Version

``` bash
pip2 -v
pip3 -v
```

Displays the installed pip version and associated Python interpreter.

------------------------------------------------------------------------

## 4. Install a Package

``` bash
pip install flask
```

Downloads and installs Flask from PyPI.

------------------------------------------------------------------------

## 5. Show Package Information

``` bash
pip show flask
```

Displays package version, installation path, and metadata.

------------------------------------------------------------------------

## 6. Install Dependencies

``` bash
pip install -r requirements.txt
```

Installs all packages listed in `requirements.txt`.

Expected Output:

``` text
Collecting Flask
Installing collected packages...
Successfully installed Flask
```

------------------------------------------------------------------------

## 7. Upgrade a Package

``` bash
pip install flask --upgrade
```

Upgrades Flask to the latest available version.

------------------------------------------------------------------------

## 8. Uninstall a Package

``` bash
pip uninstall flask
```

Removes Flask from the current Python environment.

------------------------------------------------------------------------

## 9. Install Using easy_install

``` bash
easy_install flask
```

Legacy package installation method. Modern projects should use `pip`.

------------------------------------------------------------------------

## 10. Install a Wheel Package

``` bash
pip install app.whl
```

Installs a package from a precompiled wheel file.

------------------------------------------------------------------------

## 11. Inspect Python Module Search Path

``` bash
python3 -c "import sys; print(sys.path)"
```

Displays directories searched for Python modules.

------------------------------------------------------------------------

# Practical Exercises

## Run a Script

``` bash
python3 app.py
```

## Install Dependencies

``` bash
pip install -r requirements.txt
```

## Upgrade Flask

``` bash
pip install flask --upgrade
```

## View Installed Package Details

``` bash
pip show flask
```

------------------------------------------------------------------------

# Best Practices

-   Use Python 3 for all new projects.
-   Track dependencies in `requirements.txt`.
-   Use virtual environments for project isolation.
-   Keep packages updated.

------------------------------------------------------------------------

# Common Mistakes

-   Using Python 2 for new development.
-   Forgetting to install dependencies.
-   Mixing global and project-specific packages.
-   Not pinning package versions.

------------------------------------------------------------------------

# Interview Questions

### What is the difference between Python 2 and Python 3?

Python 2 is deprecated, while Python 3 is the actively maintained
version with modern language features.

### What is pip?

Python's package manager used to install and manage libraries.

### What does `pip install -r requirements.txt` do?

Installs every dependency listed in the requirements file.

### What is a `.whl` file?

A precompiled Python package format that speeds up installation.

------------------------------------------------------------------------

# Summary

This chapter covered:

-   Python fundamentals
-   Python 2 vs Python 3
-   pip package manager
-   requirements.txt
-   Installing, upgrading, and removing packages
-   Wheel packages
-   Python module search paths
