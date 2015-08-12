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
Usage
-----

Example usage:

```console
$ ls
Procfile  conda-requirements.txt  numbercrunch.py

$ heroku create --buildpack https://github.com/kennethreitz/conda-buildpack.git

$ git push heroku master
...
-----> Fetching custom git buildpack... done
-----> Python/Miniconda app detected
-----> Preparing Python/Miniconda Environment (3.5.2)
       installing: python-2.7.6-2 ...
-----> Installing dependencies using Conda
      Fetching packages ...
        bitarray-0.8.1 100% |###############################| Time: 0:00:00  17.53 MB/s00  B/s
        dateutil-2.1-p 100% |###############################| Time: 0:00:00   2.29 MB/s00  B/s
        h5py-2.3.0-np1 100% |###############################| Time: 0:00:00  13.49 MB/s00  B/s
        hdf5-1.8.9-1.t 100% |###############################| Time: 0:00:00  12.20 MB/s00  B/s
        libpng-1.5.13- 100% |###############################| Time: 0:00:00   8.05 MB/s00  B/s
        llvm-3.3-0.tar 100% |###############################| Time: 0:00:03  10.65 MB/s00  B/s
        llvmpy-0.12.6- 100% |###############################| Time: 0:00:00   9.65 MB/s00  B/s
        nltk-2.0.4-np1 100% |###############################| Time: 0:00:00   6.26 MB/s00  B/s
        numba-0.13.2-n 100% |###############################| Time: 0:00:00  11.54 MB/s00  B/s
        numexpr-2.3.1- 100% |###############################| Time: 0:00:00   6.80 MB/s00  B/s
        numpy-1.8.1-py 100% |###############################| Time: 0:00:00   8.82 MB/s00  B/s
        pandas-0.14.0- 100% |###############################| Time: 0:00:00   9.90 MB/s00  B/s
        pyside-1.2.1-p 100% |###############################| Time: 0:00:00   6.00 MB/s00  B/s
        pytables-3.1.1 100% |###############################| Time: 0:00:00   9.24 MB/s00  B/s
        pytz-2014.3-py 100% |###############################| Time: 0:00:00   1.54 MB/s00  B/s
        qt-4.8.5-0.tar 100% |###############################| Time: 0:00:01  17.36 MB/s00  B/s
        reportlab-3.1. 100% |###############################| Time: 0:00:00   4.87 MB/s00  B/s
        scikit-image-0 100% |###############################| Time: 0:00:01  12.81 MB/s00  B/s
        scikit-learn-0 100% |###############################| Time: 0:00:00   8.70 MB/s00  B/s
        scipy-0.14.0-n 100% |###############################| Time: 0:00:02  15.16 MB/s00  B/s
        shiboken-1.2.1 100% |###############################| Time: 0:00:00   3.33 MB/s00  B/s
        six-1.6.1-py27 100% |###############################| Time: 0:00:00  12.54 MB/s00  B/s
```

You can also add it to upcoming builds of an existing application:

```console
$ heroku config:add BUILDPACK_URL=https://github.com/kennethreitz/conda-buildpack.git
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

## Fair Warning

Heroku limits the final application footprint (slug) size to 300MB. Start small. In case the slug size limit is exceeded, deleting the build cache through the [heroku-repo plugin](https://github.com/heroku/heroku-repo#purge_cache) might help.

ॐ
