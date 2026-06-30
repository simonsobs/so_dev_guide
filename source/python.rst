======
Python
======

Overview
========

Python is a high-level laanguage that is widely used in the scientific computing
community. It is general purpose, easy to learn and has a rich ecosystem of 
libraries. It is also highly portable and readable which significantly reduces
the cost of maintaining and sharing code.

For these reasons, it is the language SO will use the most for its codebase. Any
other language choise should be either for a very specific use case, or for
having significant performance advantages. In the latter case, the code should be
written in C++ and provide a Python interface to the user.

Version Support
===============

All SO code targets Python 3. Developers must not assume that all users 
will have access to the latest and greatest versions of Python and key 
scientific packages. We recommend that packages always support the oldest Python
version that is at not at the end of life (`Python versions`_).  

.. note:: 

  Certain DAQ or super-computing environments may have
  additional constraints; these can be explained in the code README or
  CONTRIBUTING instructions.

Cloud-based unit-testing frameworks typically support a variety of
Python versions; complete test coverage and the use of such services
is a good way to validate your code across multiple versions.

Style
=====

Although Python is a very flexible language, it is important to follow a 
consistent style across the SO python codebase for the reasons mentioned in the
introduction of this document. For any rule not explicitly specified in this
document, please refer to the `PEP8`_ style guide. We strongly recommend to use
`pyproject.toml` to configure your project as it is the new standard for Python
projects.

In addition to the style description, we provide a :ref:`config file for ruff <python-ruff-config>`
that can automatically format code. In case you find yourself working on code that is
not formatted according to the style, you can maintain the existing style. However,
when you are formatting the code, we highly recommend to use a branch which only contains
the formatting changes and submit a pull request.


Indentation
-----------
Indentation is one of the aspects of code formatting that is important to be consistent
across codebases, especially since we use multiple languages.

We will use 4 spaces as the indentation for python.

Tabs are not allowed for indentation.


Line width
----------

The maximum line width allowed is 120 characters.


Naming Conventions
------------------

The name of a variable, function or class is one of the most important aspects of code
readability. It can immediately inform about the purpose of the named thing. Please avoid
single letter names, except for loop variables, even if it is a commonly understandable
variable.

We will utilize the following naming conventions:
1. Class and struct names should be in PascalCase, e.g. `MyClass`.
2. Function names should be in camelCase, e.g. `myFunction`.
3. Variable names should be in snake_case, e.g. `my_variable`.
4. Constants should be in ALL_CAPS with underscores, e.g. `MAX_SIZE`.
5. Namespaces should be in snake_case, e.g. `my_namespace`.


Typing
------

Python typing is optional, but we  recommend to use it in all new code. It provides
a way to document the expected types of a function's arguments and return value.
We also suggest when used to use the `typing` module of the standard library,
and not a third part library. Please refer to `PEP 484`_ for more information.

.. _python-ruff-config:

Ruff Config
-----------
As formatting tool, we will use ruff. The config file for the expected formatting
is:

.. code-block:: toml
  
  indent-width = 4
  line-length = 120


Please copy this in `.ruff.toml` file in the root of your repository.

If you want to add it in your `pyproject.toml` file, please add the following section:

.. code-block:: toml

  [tool.ruff]
  indent-width = 4
  line-length = 120


In addition to `ruff` similar tools are `black` and `pylint`. Lastly, you can 
use `isort` to sort your imports. Please refer to the `isort`_ documentation for 
more information.


Documentation of Code
=====================

docstrings
----------

`docstrings` are blocks of text located near the tops of python modules,
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
style`_ as it is widely used to scientific Python packages, from numpy to astropy.
You can also use the `google style`_ for docstrings, but you need to be clear
about it in either the README or CONITRIBUTING file. These two styles are
very similar.  They are both supported in Sphinx, e.g. through the
`napoleon plugin`_.


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


Implementation Choices
======================

Module Packaging
================

Pyproject file
--------------

Python packages should be installable via ``pip``. The minimal
configuration for a package named ``mypackage`` is a ``pyproject.toml`` at
the repository root:

.. code-block:: toml

  [project]
  name = "mypackage"
  version = "0.1.0"
  description = "Add your description here"
  readme = "README.md"
  requires-python = ">=3.11"
  dependencies = []


For more detail—including how to declare entry points, data files, and
optional dependencies—see the `pyproject.toml documentation`_ and the
`Python Packaging User Guide`_.


develop vs. build+install
-------------------------

Packages must support both development (editable) installs and
standard installs.  During development, use::

  pip install -e .

This creates a link from the install location back to the source tree,
so edits are immediately reflected without reinstalling.  It is the
recommended mode for day-to-day work and is sufficient for running
unit tests.

For distribution or deployment, use a standard install::

  pip install .

Both modes must work correctly.  In particular, any data files,
compiled extensions, or entry-point scripts must be declared in
``pyproject.toml`` so that they are included in both modes.

User override of compiler options and install locations
-------------------------------------------------------

Rather than hardcoding install prefixes or compiler choices, expose
them via environment variables with sensible defaults.  For example, a
``Makefile`` wrapper might read::

  CC      ?= gcc
  PREFIX  ?= $(HOME)/.local

  install:
      CC=$(CC) pip install --prefix=$(PREFIX) .

A user who needs a different compiler or install prefix can set the
variables without editing any project files::

  CC=clang PREFIX=/opt/myenv make install

Document the available variables in the README or CONTRIBUTING file so
that users can find them without reading the source.


Unit Testing
============

.. todo:: Move this explanation to common.rst after all PRs are merged.

A *unit test* is an automated check that a small, isolated piece of
code—typically a single function or method—behaves correctly.  Unit
tests are distinct from integration tests (which test interactions
between components) or end-to-end tests (which test a complete
workflow).  The goal is to catch regressions quickly and to give
developers confidence that individual components are correct before
combining them.

Designing good unit tests
-------------------------

Good unit tests share a few properties:

- **Isolated**: Each test exercises one code path and does not depend
  on state left by another test.  Tests that share mutable global
  state or that must run in a specific order are fragile.
- **Deterministic**: A test should produce the same result every time.
  Avoid relying on wall-clock time, random seeds, or external network
  resources unless the test explicitly controls them.
- **Fast**: Unit tests should run in milliseconds.  Slow tests
  discourage developers from running the suite frequently.
- **Focused**: Test one behavior per test function.  When a focused
  test fails, its name alone should indicate what broke.
- **Thorough on edge cases**: In addition to the happy path, test
  boundary conditions, empty inputs, and expected failure modes.

unittest
--------

Python ships with the ``unittest`` module, which provides a standard
framework for writing and discovering tests.  We recommend using
pytest_ as the test runner, since it produces cleaner output and
supports a simpler assertion style while remaining fully compatible
with ``unittest``-style test classes.

Organize tests in a ``tests/`` directory at the repository root.  Run
the full suite with::

  python -m pytest tests/

Run a single test file or function with::

  python -m pytest tests/test_mymodule.py
  python -m pytest tests/test_mymodule.py::test_my_function


Github Actions for Continuous Integration
-----------------------------------------

All SO packages should run their test suite automatically on every
pull request using a continuous integration (CI) service.  The SO
Github organization uses GitHub Actions; a minimal workflow that runs
tests across several Python versions looks like::

  name: Tests
  on: [push, pull_request]
  jobs:
    test:
      runs-on: ubuntu-latest
      strategy:
        matrix:
          python-version: ["3.11", "3.12", "3.13"]
      steps:
        - uses: actions/checkout@v3
        - uses: actions/setup-python@v4
          with:
            python-version: ${{ matrix.python-version }}
        - run: pip install -e .[test]
        - run: python -m pytest tests/

Place this file at ``.github/workflows/tests.yml`` in your repository.
The CI check must pass before a pull request can be merged. Similarly, you can
set the CI to run linter check to verify that the code is formatted according 
to the style guide.


Compiled Extensions
===================

Numerical Data
--------------

Scientific Python packages often need to call compiled C or C++ code
for performance.  Several approaches are in common use; choose one
that fits the complexity of your project:

- **ctypes**: Python's built-in foreign-function interface.  No
  compilation step is needed beyond building the shared library; load
  it at runtime with ``ctypes.CDLL``.  Good for calling a small number
  of existing C functions, but requires manual declaration of argument
  and return types.
- **cffi**: Similar in spirit to ctypes but with a cleaner API.
  Accepts C header declarations directly and handles type conversions
  more reliably.  Preferred over ctypes for new code.
- **pybind11_**: A header-only C++11 library for exposing C++ classes
  and functions to Python.  Handles numpy arrays natively through its
  buffer protocol support.  Recommended when the extension is written
  in C++ and interface performance matters.
- **Cython_**: A superset of Python that compiles to C.  Allows
  gradual optimization of existing Python code and tight integration
  with numpy arrays via typed memory views.  Requires a ``.pyx``
  source file and a build step.

For all of these, prefer passing ``numpy`` arrays rather than raw
pointers where possible.  Arrays carry shape and dtype metadata that
reduces the risk of type mismatches at the Python/C boundary.


Meson
-----

For projects that combine Python with C or C++ and need a real build
system—rather than a single small extension module—we recommend
`Meson`_ as the build tool. Meson is fast, has first-class support for
C++ and mixed-language projects, and integrates with Python packaging
through the `meson-python`_ build backend, which lets ``pip install``
and ``pip install -e .`` drive a Meson build transparently.

Meson is preferred over raw ``setup.py`` ``Extension`` builds or
hand-written ``CMakeLists.txt`` plus glue code because it has native,
well-tested support for both languages, clear cross-compilation and
dependency-discovery support (via ``pkg-config`` and Meson's own
wrap system), and a declarative ``meson.build`` syntax that is easier
to review and maintain than ``setup.py`` build logic.

To use Meson for a Python/C++ package, declare it as the build backend
in ``pyproject.toml``:

.. code-block:: toml

  [build-system]
  build-backend = "mesonpy"
  requires = ["meson-python", "pybind11"]

  [project]
  name = "mypackage"
  version = "0.1.0"

and describe the build in a ``meson.build`` file at the repository
root:

.. code-block:: meson

  project('mypackage', 'cpp', version: '0.1.0')

  py = import('python').find_installation(pure: false)
  pybind11_dep = dependency('pybind11')

  py.extension_module(
    '_mypackage',
    'src/mypackage/_mypackage.cpp',
    dependencies: [pybind11_dep],
    install: true,
  )

  subdir('src/mypackage')

The top-level ``meson.build`` should not list every Python source file
itself. Instead, the Python package directory needs its own
``meson.build`` (e.g. ``src/mypackage/meson.build``) that declares
which ``.py`` files belong to the package and installs them with
``py.install_sources``:

.. code-block:: meson

  python_sources = [
    '__init__.py',
    'core.py',
    'utils.py',
  ]

  py.install_sources(
    python_sources,
    subdir: 'mypackage',
  )

Keeping this list in the package's own ``meson.build`` means that adding a new 
module only requires updating the list next to the code it describes, rather 
than editing a build file at the root of the repository. The ``subdir`` keyword 
argument tells Meson where under the install prefix's ``site-packages`` the 
files should land, and should match the package's import name.

With this setup, both ``pip install .`` and the editable
``pip install -e .`` workflow described above work without further
configuration, and the compiled extension is built using Meson rather
than ``distutils`` / ``setuptools`` directly.


Style in Mixed Language Codes
-----------------------------

In cases of hybrid Python/C/C++ libraries, consistency between class
and function names is more important than rigidly following all the
recommendations for individual languages.  So it's ok, for example, if
the Python interface to a C++ library uses theSameVariableNames as
the C++ library. However, please maintain the described style guide for Python
and C++ code separately. 


Tips for Successful Scientific Codes
====================================

Parameter Files
---------------

Scientific codes are often controlled by large sets of parameters.
Rather than inventing a custom configuration format, prefer one of two
approaches.

**Use Python directly.**  If your users already know Python, a
configuration file that is simply a Python module is the most
expressive option.  Users get the full language—loops, conditionals,
imports—with no extra parser to maintain::

  # config.py
  n_samples = 1000
  output_dir = '/data/output'
  frequencies = list(range(90, 300, 30))

Load it with ``importlib.import_module`` or ``importlib.util``.

**Use YAML** for structured, human-readable configuration that does
not require executing code.  YAML is widely understood and has solid
Python library support via `PyYAML`_ or `ruamel.yaml`_.

Avoid inventing a custom text format with a hand-written parser; the
result is almost always harder to use and harder to maintain than
either of the above options.



Command-Line Scripts
--------------------

Prefer Python over shell scripts for non-trivial command-line tools.
Python is more readable, easier to test, and already familiar to the
developers and users of SO software.  A shell script that grows beyond
a few lines of plumbing becomes difficult to maintain; rewrite it in
Python before that point.

Entry-point scripts should use argparse_ (or the third-party click_
library) to parse arguments.  This provides automatic ``--help``
output, type coercion, and a consistent interface for users::

  import argparse

  def main():
      parser = argparse.ArgumentParser(description='Process data.')
      parser.add_argument('input', help='Input file path')
      parser.add_argument('--verbose', action='store_true')
      args = parser.parse_args()
      ...

  if __name__ == '__main__':
      main()

Declare scripts as ``scripts`` in ``pyproject.toml`` so that
``pip install`` places them on the user's ``PATH`` automatically:

.. code-block::toml

  [project.scripts]
  my-tool = "mypackage.cli:main"



User Choice of Install Location, Compiler Choice, etc.
------------------------------------------------------

Provide sensible defaults for all configurable choices—install prefix,
compiler, data directories—so that a new user can get started without
reading documentation.  At the same time, make every default easy to
override without editing project files.

Environment variables are the lightest-weight mechanism::

  import os
  DATA_DIR = os.environ.get('MYPACKAGE_DATA_DIR', '/usr/share/mypackage')

A user who needs a non-default path sets the variable in their shell
profile; the default continues to work for everyone else.  

For choices that affect the build, rely on Meson rather than plumbing
your own environment variables through. Meson natively honors the
standard ``CC``, ``CXX``, ``CFLAGS``, and ``CXXFLAGS`` environment
variables for compiler choice::

  CC=clang CXX=clang++ pip install .

The install prefix is set the same way: pass Meson options through
``meson-python``'s ``pip`` config-settings rather than a custom
environment variable::

  pip install . --config-settings=setup-args="-Dprefix=/opt/myenv"

Document the full set of environment variables and any supported
Meson options in the README so users can find them without reading
the source.


Automatic Semantic Versioning
==============================

There are several tools and methods to automatically generate version numbers
for Python packages. Three of the most popular are `versioneer`_, 
`setuptools_scm`_ and `hatchling`_.

Versioneer
----------

The "versioneer" tool is a nice way to automate the creation of
version codes for python packages, and to make those codes available
from within the package: `versioneer`_.

To get versioneer operating on your python project, do the following:

#. Install versioneer with the ``toml`` extra:
   ``pip install versioneer[toml]``.

#. Add the following sections to your ``pyproject.toml``:

   .. code-block:: toml

     [build-system]
     requires = ["setuptools", "versioneer[toml]"]
     build-backend = "setuptools.build_meta"

     [project]
     dynamic = ["version"]

     [tool.versioneer]
     VCS = "git"
     style = "pep440"
     versionfile_source = "mylibname/_version.py"
     versionfile_build = "mylibname/_version.py"
     tag_prefix = "v"
     parentdir_prefix = "mylibname-"

   Replace "mylibname" with the name of your python package.
   The ``tag_prefix`` affects how versioneer searches your git tags;
   in this case it will look for tags starting with ``v``, such as
   ``v0.1.2``.

#. Run the versioneer binary at the top of your source directory
   (where ``pyproject.toml`` is): ``versioneer install --no-vendor``.
   This will check your configuration, create ``_version.py`` in your
   python source tree, and modify a few other git/PyPI files.  ``git
   status`` will show something like::

	new file:   .gitattributes
	modified:   MANIFEST.in
	modified:   mylibname/__init__.py
	new file:   mylibname/_version.py

   Those can all be committed along with your changes to
   ``pyproject.toml``.  A new build should yield informative version
   strings, e.g.::

     $ python -c 'import mylibname; print(mylibname.__version__)'
     0.4.0+2.g13ed14d.dirty

#. (Optional) If you are using Sphinx to build documentation for your project
   you can have Sphinx determine the project version number from versioneer by
   importing ``__version__`` in your ``conf.py`` file::

    from mylibname import __version__ as mylibname_version

   You should then change the ``version`` and ``release`` fields to
   ``mylibname_version``::

    # The short X.Y version
    version = mylibname_version
    # The full version, including alpha/beta/rc tags
    release = mylibname_version

#. All you need to do to bump the version number is to tag the
   relevant commit with a tag that matches the right format (in this
   example, something like v0.4.0).  The GitHub "releases" feature
   allows you to do this, and to see all the tags.


.. note::

   Portions of this page were drafted/edited with the assistance of `Claude Code Sonnet 5`.


.. _Python versions: https://devguide.python.org/#status-of-python-branches
.. _PEP8: https://www.python.org/dev/peps/pep-0008/
.. _isort: https://isort.readthedocs.io/en/latest/
.. _PEP 484: https://peps.python.org/pep-0484/
.. _google style: https://github.com/google/styleguide/blob/gh-pages/pyguide.md#38-comments-and-docstrings
.. _numpy style: https://docs.scipy.org/doc/numpy-1.15.0/docs/howto_document.html
.. _napoleon plugin: https://sphinxcontrib-napoleon.readthedocs.io/en/latest/
.. _pyproject.toml documentation: https://packaging.python.org/en/latest/guides/writing-pyproject-toml/
.. _Python Packaging User Guide: https://packaging.python.org/
.. _argparse: https://docs.python.org/3/library/argparse.html
.. _click: https://click.palletsprojects.com/
.. _versioneer: https://github.com/python-versioneer/python-versioneer/tree/master
.. _setuptools_scm: https://github.com/pypa/setuptools-scm/blob/main/setuptools-scm/README.md
.. _hatchling: https://pypi.org/project/hatchling/
.. _pytest: https://docs.pytest.org/
.. _pybind11: https://pybind11.readthedocs.io/
.. _Cython: https://cython.readthedocs.io/
.. _Meson: https://mesonbuild.com/
.. _meson-python: https://mesonpy.readthedocs.io/
.. _PyYAML: https://pyyaml.org/
.. _ruamel.yaml: https://yaml.readthedocs.io/