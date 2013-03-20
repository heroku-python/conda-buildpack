Conda Buildpack
===============

This is a [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks) for [Conda](http://docs.continuum.io/conda/), the Python distribution for scientific computing by Continuum Analytics.


Usage
-----

Example usage:

    $ ls
    Procfile  conda-requirements.txt  numbercrunch.py

    $ heroku create --buildpack https://github.com/kennethreitz/conda-buildpack.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python/Conda app detected
    -----> Preparing Python runtime (python-2.7.3)
    -----> Installing dependencies using Conda (1.4.6)
           Downloading/unpacking bitarray-0.8.0-py27_0.tar.bz2

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=https://github.com/kennethreitz/conda-buildpack.git


Simple test:

    >>> bitarray.test()
    bitarray is installed in: /app/anaconda/lib/python2.7/site-packages/bitarray
    bitarray version: 0.8.0
    2.7.3 |Continuum Analytics, Inc.| (default, Feb 25 2013, 18:46:31)
    [GCC 4.1.2 20080704 (Red Hat 4.1.2-52)]
    .................................................................................................................................
    ----------------------------------------------------------------------
    Ran 129 tests in 1.375s

    OK
    <unittest.runner.TextTestResult run=129 errors=0 failures=0>