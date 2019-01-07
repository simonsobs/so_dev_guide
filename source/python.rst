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

docstrings
----------

docstrings are blocks of text located near the tops of python modules,
classes, and functions.  These blocks are often extracted and
published separately from the code, as a part of the documentation for
how to use the code.

Simple functions may be documented with one-liners, in plain English.
For example::

  def get_hubble_constant():
      """Returns the Hubble Constant of this Universe, in km/s/Mpc."""
      ...

When documenting a more complicated function, it is helpful to have
standards for organizing and formatting important information, such as
the expected type and meaning of each argument, the format of the
return value, and the type and meaning of any exceptions that might be
raised.

We will accept any standard that meets the following criteria:

- compact and nicely formatted text in the raw code
- compact and nicely formatted text within Python's "help" facility
- nicely formatted text in auto-generated documentation using Sphinx

We strongly recommended that SO codes use either the `numpy
style`_ or the `google style`_ for docstrings.  These two styles are
very similar.  They are both supported in Sphinx, e.g. through the
`napoleon plugin`_.

**Because of the broad use of numpy style in the scientific community
(from numpy through to astropy), we recommend the use of numpy in SO
code.** If you think you'd rather use google style, that's probably
fine, just be clear about it in the README or CONTRIBUTING file.


Inline Comments
---------------

In addition to docstrings, Python code should be documented with
comments prefixed with the # character.  Remember that people reading
the comments will also be reading the code -- so the comments should
clarify and elucidate, rather than simply re-state what is already
obvious from the code.  The code already says *what* is happening; use
the comments to say *why* those things are happening.

Here's a perhaps unnecessary inline comment::

  # Loop through all catalogs.
  for catalog in catalogs:
    catalog.mask_red_galaxies()

Here's an example of a helpful explanatory comment::

  # Mask the red galaxies, because we will later assume that all galaxies are blue.
  for catalog in catalogs:
    catalog.mask_red_galaxies()

.. _PEP8: https://www.python.org/dev/peps/pep-0008/
.. _google style: https://github.com/google/styleguide/blob/gh-pages/pyguide.md#38-comments-and-docstrings
.. _numpy style: https://docs.scipy.org/doc/numpy-1.15.0/docs/howto_document.html
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

