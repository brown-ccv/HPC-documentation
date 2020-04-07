---
title: Python Installs
date: '2019-01-30T17:51:11.000Z'
draft: false
project: Oscar
section: Software
weight: 0
icon: check
---

# Installing Python Packages

For Python 2, we recommend using the **python/2.7.16** module. For Python 3, we recommend using the **python/3.7.4** module.

{% hint style="info" %}
Both these modules include the `pip`and `virtualenv`commands, but do not include other common Python packages \(e.g., SciPy, NumPy\). This affords individual users complete control over the packages they are using.
{% endhint %}

There are several ways for users to install python packages on Oscar

* using a **virtual environment**
* using conda
* into their home directory
* into a custom location
* from source into a custom location

{% hint style="warning" %}
We recommend using a virtual environment for your workflow if you prefer`pip.` If you are a conda user we recommend managing your workflow with [conda environments ](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
{% endhint %}

{% hint style="info" %}
In this document, we use angular brackets `<>` to denote command line options that you should replace with an appropriate value
{% endhint %}

{% hint style="info" %}
Note for python3 packages replace `python` with `python3` _\*\*_and `pip` with `pip3`
{% endhint %}

{% hint style="info" %}
Intel provides optimized packages for numerical and scientific work that you can install through[ pip](https://software.intel.com/en-us/articles/installing-the-intel-distribution-for-python-and-intel-performance-libraries-with-pip-and) or [anaconda](https://software.intel.com/en-us/articles/using-intel-distribution-for-python-with-anaconda).
{% endhint %}

## Using virtualenv

Virtual environments are a cleaner way to install python packages for a specific workflow. [This webpage](https://virtualenv.pypa.io/en/stable/) gives a good explanation of the use cases. In the example below, a virtual environment called 'my\_cool\_science' is set up in your home directory:

```text
module load python/2.7.16
cd ~
virtualenv my_cool_science
source ~/my_cool_science/bin/activate
pip install <your package>
deactivate
```

line 1: load the version of python you want to use

line 2: change directory to home

line 3: create the virtual environment

line 4: activate the virtual environment

line 5: install any packages you need for the virtual environment

line 6: deactivate the environment

When you want to use the environment, e.g. in a batch script or an interactive session

`source ~/my_cool_science/bin/activate`

When your work is finished, deactivate the environment with

`deactivate`

### Install into your home directory

The `--user` flag will instruct pip to install to you home directory

```bash
pip install --user <package>
```

This will install the package under the following path in user's HOME directory:

```text
~/.local/lib/python<version>/site-packages
```

{% hint style="warning" %}
If you omit the `--user` flag you will see

```text
    IOError: [Errno 13] Permission denied: '/gpfs/runtime/opt/python/2.7.3/lib/python2.7/site-packages/ordereddict.py'
```

This is because users do not have access to the default locations where software is installed.
{% endhint %}

Python packages can often have conflicting dependencies. For workflows that require a lot of python packages, we recommend using virtual environments.

## Install at custom location

Users have a limit of 20GB for their home directories on Oscar. Hence, users might want to use their data directory instead for installing software. Another motivation to do that is to have shared access to the software among the whole research group.

```bash
 pip install --target=</path/to/install/location> <package>
```

This path to install location will have to be added to the **PYTHONPATH** environment variable so that python can find the python modules to be used. This is not necessary for software installed using the `--user` option.

```bash
export PYTHONPATH=</path/to/install/location>:$PYTHONPATH
```

This can be added at the end of your `.bashrc` file in your home directory. This will update the PYTHONPATH environment variable each time during startup. Alternatively, you can update PYTHONPATH in your batch script as required. This can be cleaner as compared to the former method. If you have a lot of python installs at different locations, adding everything to PYTHONPATH can create conflicts and other issues.

A caveat of using this method is that pip will install the packages \(along with its requirements\) even if the package required is already installed under the global install or the default local install location. Hence, this is more of a brute force method and not the most efficient one.

For example, if your package depends on numpy or scipy, you might want to use the numpy and scipy under our global install as those have been compiled with MKL support. Using the `--target` option will reinstall numpy with default optimizations and without MKL support at the specified location.

## Installing from source

Sometimes, python software is not packaged by the developers to be installed by pip. Or, you may want to use the development version which has not been packaged. In this case, the python package can be installed by downloading the source code itself. Most python packages can be installed by running the `setup.py` script that should be included in the downloaded files.

{% hint style="warning" %}
You will need to provide a "prefix path" for the install location

```text
python setup.py install --prefix=</path/to/install/location>
```
{% endhint %}

This will create the sub-directories `bin`, `lib`, etc. at the location provided above and install the packages there. The environment will have to be set up accordingly to use the package:

```bash
export PATH=</path/to/install/location>/bin:$PATH
export PYTHONPATH=</path/to/install/location>/lib/python<version>/site-packages:$PYTHONPATH
```

