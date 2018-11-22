======
Python
======

Python code should be developed to work with python3, backwards
compatible to version 3.3 if possible.  Compatibility with python 2.7
is not required but is encouraged where possible.

Syntax should follow PEP8_.  There are tools available, such as pylint
and flake8, to check for PEP8 compliance.  We will pick one of those
utilities and run with it.  Either one can be told to ignore certain
errors or lines, in cases where it is necessary to violate the PEP8.

For docstrings, SO will adopt the `google style`_.  This choice
accomplishes the following goals:

- compact and nicely formatted in the code itself.
- compact and nicely formatted by python's "help" facility
- recognized by sphinx auto-generated documentation, if one activates
  the `napoleon plugin`_.

In cases of hybrid Python/C/C++ libraries, consistency between class
and function names is more important than rigidly following all the
recommendations for individual languages.  So it's ok, for example, if
the Python interface to a C++ library uses theSameVariableNames as
the C++ library.
  
.. _PEP8: https://www.python.org/dev/peps/pep-0008/
.. _google style: https://github.com/google/styleguide/blob/gh-pages/pyguide.md#38-comments-and-docstrings
.. _napoleon plugin: https://sphinxcontrib-napoleon.readthedocs.io/en/latest/


