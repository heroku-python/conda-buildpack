Conda Buildpack
===============

This is a [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks) for [Conda](http://conda.pydata.org/), the Python distribution for scientific computing by Continuum Analytics.

This buildpack enables the installation of binary packages through the
open source [conda](http://conda.pydata.org/) application.  Conda is
recognized as being core to Continuum's Anaconda Scientific Python distro
but it's also at the heart of the lighter weight
[Miniconda](http://conda.pydata.org/miniconda.html) distro which we use
here to install _only_ the binary packages we need for our apps deployed
on Heroku.

To control what binary packages are installed by conda, supply a
`conda-requirements.txt` file (which can be created by capturing the output
of `conda list -e` for your working conda environment).
Like when using the standard buildpack for python from Heroku, you can also
still supply a `requirements.txt` file for [pip](https://github.com/pypa/pip)
to process.  In this way, you can install binary packages via conda for
everything you can and still use pip for anything you can't.

**Warning**: this buildpack is functional but still a work in progress.

Usage
-----

Example usage:

```console
$ ls
Procfile  conda-requirements.txt  numbercrunch.py

$ heroku create --buildpack https://github.com/kennethreitz/anaconda-buildpack.git

$ git push heroku master
...
-----> Fetching custom git buildpack... done
-----> Python/Anaconda app detected
-----> Preparing Python runtime
-----> Installing dependencies using Conda
        Downloading/unpacking bitarray-0.8.0-py27_0.tar.bz2
```

You can also add it to upcoming builds of an existing application:

```console
$ heroku config:add BUILDPACK_URL=https://github.com/kennethreitz/anaconda-buildpack.git
```


Simple test:

```python
>>> bitarray.test()
bitarray is installed in: /app/.heroku/anaconda/lib/python2.7/site-packages/bitarray
bitarray version: 0.8.0
2.7.3 |Continuum Analytics, Inc.| (default, Feb 25 2013, 18:46:31)
[GCC 4.1.2 20080704 (Red Hat 4.1.2-52)]
.................................................................................................................................
----------------------------------------------------------------------
Ran 129 tests in 1.375s

OK
<unittest.runner.TextTestResult run=129 errors=0 failures=0>
```
