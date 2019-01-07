======
Python
======

Overview
========

Version Support
===============

All SO code should target Python 3, rather than Python 2.  It is
possible to write code that works in both Python 3 and Python 2.7;
that support decision should be made within each repository.  The
general computing community has considered Python 2 to be deprecated
for several years; key scientific packages are now well-supported on
Python 3 and there are no strong reasons to resist the move to 3.x.

Developers must not assume that all users will have access to the
latest and greatest versions of Python and key scientific packages.
We recommend that packages always support a Python version that is at
least 3 years old.  **Python 3.5 was released on September 13, 2015,
and is thus the earliest Python version that needs to be supported by
all code.** Certain DAQ or super-computing environments may have
additional constraints; these can be explained in the code README or
CONTRIBUTING instructions.

Cloud-based unit-testing frameworks typically support a variety of
Python versions; complete test coverage and the use of such services
is a good way to validate your code across multiple versions.

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

