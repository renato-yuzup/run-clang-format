=====================
 run-clang-format.py
=====================
----------------------------------------------
 Lint files and directories with clang-format
----------------------------------------------

.. contents::
   :local:

Introduction
============

A wrapper script around clang-format, suitable for linting multiple files
and to use for continuous integration.

This is an alternative API for the clang-format command line.
It runs over multiple files and directories in parallel.
A diff output is produced and a sensible exit code is returned.

.. image:: screenshot.png


How to use?
===========

Copy `run-clang-format.py <run-clang-format.py>`_ in your project,
then run it recursively on directories, or specific files::

  ./run-clang-format.py -r src include foo.cpp

It's possible to exclude paths from the recursive search::

  ./run-clang-format.py -r \
      --exclude src/third_party \
      --exclude '*_test.cpp' \
      src include foo.cpp

These exclude rules can be put in a ``.clang-format-ignore`` file,
which also supports comments.

An example configuration is available in this repo::

  $ cat .clang-format-ignore
  # ignore third_party code from clang-format checks
  src/third_party/*


Continuous integration
======================

Check `.travis.yml <.travis.yml>`_.

For an example of failure in logs, click the badge (build is broken on purpose):

.. image:: https://travis-ci.org/Sarcasm/run-clang-format.svg?branch=master
    :target: https://travis-ci.org/Sarcasm/run-clang-format


FAQ
===

Can I check only changed files?
-------------------------------

Yes. You can run against staged files in the current git repository
by running this script without arguments::

  ./run-clang-format.py

You don't get all the flavors for recursivity and exclusion list, however.