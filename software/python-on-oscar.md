# Python on Oscar

Several versions of Python are available on Oscar as modules. For Python 2, we recommend using the python/2.7.16 module. For Python 3, we recommend using the python/3.7.4 module. These modules include the `pip` and `virtualenv` commands, but do not include other common Python packages \(e.g., SciPy, NumPy\). This affords individual users complete control over the packages they are using, thereby avoiding issues that can arise when code written in Python requires specific versions of Python packages.

To use the recommend Python modules, use the following commands to load the relevant module:

`module load python/2.7.16`

`module load python/3.7.4`

Users can install any Python package they require by following the instructions given on the [Installing Python Packages](python-installs.md) page.

{% hint style="info" %}
Intel provides optimized packages for numerical and scientific work that you can install through[ pip](https://software.intel.com/en-us/articles/installing-the-intel-distribution-for-python-and-intel-performance-libraries-with-pip-and) or [anaconda](https://software.intel.com/en-us/articles/using-intel-distribution-for-python-with-anaconda).
{% endhint %}

{% hint style="warning" %}
Python 2 will enter End-of-Life \(EOL\) status and will receive no further official support as of January 2020. As a consequence, you may see the following message when using pip with Python 2.

`DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won't be maintained after that date. A future version of pip will drop support for Python 2.7.`

Going forward, the [Python Software Foundation recommends](https://wiki.python.org/moin/Python2orPython3) using Python 3 for development.
{% endhint %}

