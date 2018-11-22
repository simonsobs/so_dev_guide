======
Python
======

Overview
========

Version Support
===============

.. todo:: Invent a basis for setting what minor version of python3
          should be supported at any given time.

Python code should be developed to work with python3, backwards
compatible to version 3.3 if possible.  Compatibility with python 2.7
is not required but is encouraged where possible.

Style
=====

.. todo:: Emphasize the most important parts of PEP8.

Syntax should follow PEP8_.  There are tools available, such as pylint
and flake8, to check for PEP8 compliance.  We will pick one of those
utilities and run with it.  Either one can be told to ignore certain
errors or lines, in cases where it is necessary to violate the PEP8.

Documentation of Code
=====================

For docstrings, SO will adopt the `google style`_.  This choice
accomplishes the following goals:

- compact and nicely formatted in the code itself.
- compact and nicely formatted by python's "help" facility
- recognized by sphinx auto-generated documentation, if one activates
  the `napoleon plugin`_.

.. _PEP8: https://www.python.org/dev/peps/pep-0008/
.. _google style: https://github.com/google/styleguide/blob/gh-pages/pyguide.md#38-comments-and-docstrings
.. _napoleon plugin: https://sphinxcontrib-napoleon.readthedocs.io/en/latest/

Implementation Choices
======================

Module Packaging
================

setup.py
--------

.. todo:: Show simple example but mostly lean on external references.

develop vs. build+install
-------------------------

.. todo:: Demand that both modes be supported, but develop is enough
          for unit testing.

User override of compiler options and install locations
-------------------------------------------------------

.. todo:: **Thesis:** It's useful for users to be able to store
          "config" information, saving their preferred install
          locations or compiler options.  Show how environment
          variables and/or Makefiles can be used for this.


Unit Testing
============

.. todo:: Define unit test.

Designing good unit tests
-------------------------

unittest
--------

travis
------


Compiled Extensions
===================

Numerical Data
--------------

.. todo:: Advise on a few ways of passing data arrays between python
          and C levels.

Style in Mixed Language Codes
-----------------------------

In cases of hybrid Python/C/C++ libraries, consistency between class
and function names is more important than rigidly following all the
recommendations for individual languages.  So it's ok, for example, if
the Python interface to a C++ library uses theSameVariableNames as
the C++ library.
  

Tips for Successful Scientific Codes
====================================

Parameter Files
---------------

.. todo:: **Thesis**: Why implement a Turing-complete parameter file
          parser, if your user already knows python?  Otherwise, use
          YAML.

Command-Line Scripts
--------------------

.. todo:: **Thesis**: Why force someone to write in bash if they
          already know python?

User Choice of Install Location, Compiler Choice, etc.
------------------------------------------------------

.. todo:: **Thesis**: Sensible defaults that are easy for an
          experienced user to override.

