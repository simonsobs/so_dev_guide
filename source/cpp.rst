=====
C/C++
=====

Overview
========

C++ is an important part of the software ecosystem of SO, and is used in important and
performance-critical code. C++ is a complex language and very permissive on formatting.

In addition, formatting and styling from older standards (C++98, C++03) is very
different from modern C++ (C++11 and later). As a result, these guidelines will
not require old codebases to be reformatted, but will require new code to follow a 
modern C++ style and formatting.

Though not required, if time permits, refactoring old code to modern C++ is encouraged.


Version Support
===============

All SO C++ code must compile as C++11 or later.  C++11 introduced
RAII-based resource management, lambda expressions, move semantics, and
the ``<thread>`` library, among other features that modern code relies
on.  New code should target C++11 at minimum; individual repositories
may choose a newer standard (C++14, C++17) if their environment
guarantees it, and should document that choice in their build
configuration and README.

The supported compilers are GCC 11 or later and Clang 10 or later.
Both provide full C++11 through C++17 support. Certain site computing resources
may have older compilers. In such cases, the minimum supported version should be
documented in the repository of the software.

Style
=====

Although there are many C++ style guides, and there is no single "correct" way to
write C++, we adopt a modified Google C++ style guide. For any rule not explicitly
specified in this document, please refer to the `Google C++ style guide`_.

In addition to the style description, we provide a :ref:`config file for clang-format <cpp-clang-format-config>`
that can automatically format code. In case you find yourself working on code that is
not formatted according to the style, you can maintain the existing style. However,
when you are formatting the code, we highly recommend to use a branch which only contains
the formatting changes and submit a pull request.


Indentation
-----------

Indentation is one of the aspects of code formatting that is important to be consistent
across codebases, especially since we use multiple languages.

We will use 2 or 4 spaces as the indentation for C++.

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
#. Class and struct names should be in PascalCase, e.g. `MyClass`.
#. Function names should be in camelCase, e.g. `myFunction`.
#. Variable names should be in snake_case, e.g. `my_variable`.
#. Constants should be in ALL_CAPS with underscores, e.g. `MAX_SIZE`.
#. Namespaces should be in snake_case, e.g. `my_namespace`.


Header Files
------------

All header files must guard against multiple inclusion. Use ``#pragma once`` at the
top of the file, rather than traditional ``#ifndef``/``#define``/``#endif`` guards::

  #pragma once

  // header contents

``#pragma once`` is supported by all compilers we target (GCC and Clang) and avoids
the maintenance burden and risk of typos or naming collisions inherent to manually
written include guard macros.


Use of Language Features
------------------------

Guidance on modern C++ features is already covered by the `Google C++ style guide`_, 
and we follow it without modification.

.. _cpp-clang-format-config:

Clang-format Config
-------------------
As formatting tool, we will use clang-format. The config file for the expected formatting
is:

.. code-block:: yaml

  BasedOnStyle: Google
  ColumnLimit: 120
  IndentWidth: 2

Please copy this in `.clang-format` file in the root of your repository.

Note: Indentation width can be 2 or 4 spaces, but it should be consistent across the codebase.

Documentation of Code
=====================
Documentation of the code provides information about the code to users and developers alike.
There are two types of documentation that are important: inline comments, and API docstrings.

For comments `/*..*/` and `//` are acceptable, but try to be consistent within the
code.

For API docstrings, we will use Doxygen style comments. The block starts with `/**` and
ends with `*/`. Each block should contain a `@brief` description, `@param` for each 
parameter, and `@return` for the return value, unless it is a void.

For example:
  .. code-block:: cpp

    /**
     * @brief Adds two integers and returns the result.
     *
     * @param a The first integer to add.
     * @param b The second integer to add.
     * @return The sum of a and b.
     */
    int add(int a, int b) {
        return a + b;
    }



Unit Testing
============

Due to the importance of unit testing, we will require that all new code be accompanied by at
least one unit test. The unit test should be in a separate file, and should be named
`<name>_test.cpp`, where `<name>` is the name of the file being tested. Organize tests 
in a ``tests/`` directory at the repository root.

`Catch2`_ is the unit testing framework for C++ we will use for SO as it is easy
to use, represents tests as normal boolean expressions and also allows benchmarking code.

Please refer to the Catch2 documentation for more information on how to write unit tests.
To have Catch2 tests picked up by CTest (as used in the CI workflow below), call
``catch_discover_tests`` on your test target in ``CMakeLists.txt``; see the
`Catch2 CMake integration`_ documentation for details.

For CTest to find and build these tests, the root ``CMakeLists.txt`` must enable
testing and pull in the ``tests/`` directory::

  # root CMakeLists.txt
  enable_testing()
  add_subdirectory(tests)

with a ``tests/CMakeLists.txt`` that builds the test binary and registers it::

  # tests/CMakeLists.txt
  find_package(Catch2 REQUIRED)
  add_executable(my_lib_test my_lib_test.cpp)
  target_link_libraries(my_lib_test PRIVATE my_lib Catch2::Catch2WithMain)

  include(CTest)
  include(Catch)
  catch_discover_tests(my_lib_test)

Github Actions for Continuous Integration
-----------------------------------------

All SO packages should run their test suite automatically on every
pull request using a continuous integration (CI) service.  The SO
Github organization uses GitHub Actions; a minimal workflow that builds
the project and runs its test suite across several compilers looks like::

  name: Tests
  on: [push, pull_request]
  jobs:
    test:
      runs-on: ubuntu-latest
      strategy:
        matrix:
          compiler: [g++-11, clang++-10]
      steps:
        - uses: actions/checkout@v3
        - run: sudo apt-get update && sudo apt-get install -y ${{ matrix.compiler }}
        - run: cmake -B build -DCMAKE_CXX_COMPILER=${{ matrix.compiler }}
        - run: cmake --build build
        - run: ctest --test-dir build

Place this file at ``.github/workflows/tests.yml`` in your repository.
The CI check must pass before a pull request can be merged. Similarly, you can
set the CI to run linter check to verify that the code is formatted according 
to the style guide.

.. important::

  CI time costs money, especially when running on Private repos. Please be 
  considerate and make sure that your tests remain fast and efficient. Another
  way to avoid the cost is by making your repo public.

Automatic Semantic Versioning
==============================

`cmake-git-version-tracking`_ is the recommended tool for versioning.  At configure 
time CMake queries ``git describe``, writes the result into a generated C++ 
header, and re-runs automatically whenever the git state changes.  
There is no version string to maintain by hand.

**Step 1 — fetch the module.**  Copy ``git_watcher.cmake`` and
``git_version.h.in`` from the repository into your tree, e.g.::

  cmake/
    git_watcher.cmake
    git_version.h.in   # provided by the library

**Step 2 — wire it into** ``CMakeLists.txt``::

  cmake_minimum_required(VERSION 3.14)
  project(my_project)

  # Pull in the version-tracking module.
  include(cmake/git_watcher.cmake)

  # This target re-runs whenever .git/HEAD or the index changes.
  add_git_version_header(${PROJECT_NAME}_version
      HEADER_FILE_NAME git_version.h
  )

  add_library(my_lib src/my_lib.cpp)
  # Make the generated header visible to your targets.
  target_link_libraries(my_lib PRIVATE ${PROJECT_NAME}_version)

**Step 3 — use the version in C++.**  Include the generated header::

  #include "git_version.h"

  void printVersion() {
      // GIT_RETRIEVED_STATE is false when building outside a git repo.
      if (GIT_RETRIEVED_STATE) {
          std::cout << "Version: " << GIT_DESCRIBE << "\n";
          // GIT_IS_DIRTY is true if there are uncommitted changes.
      }
  }

The most useful macros exposed by the header are:

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Macro
     - Description
   * - ``GIT_DESCRIBE``
     - Output of ``git describe --tags --dirty`` (e.g. ``v1.2.3-4-gabcdef0-dirty``)
   * - ``GIT_TAG``
     - Most recent tag (e.g. ``v1.2.3``)
   * - ``GIT_COMMIT_DATE_ISO8601``
     - Commit timestamp
   * - ``GIT_IS_DIRTY``
     - ``true`` if there are uncommitted changes
   * - ``GIT_RETRIEVED_STATE``
     - ``false`` when built outside a git repository



`cmake-git-semver`_ is a lightweight single-file alternative that parses a
``vMAJOR.MINOR.PATCH[-pre][+build]`` git tag directly into individual CMake
variables, which can be useful when you need to embed numeric version
components into build artefacts (shared library ``SOVERSION``, pkg-config
files, installers, etc.) rather than just exposing a raw ``git describe``
string to C++ code.

**Step 1 — fetch the module.**  Copy ``git_semver.cmake`` into your tree::

  cmake/
    git_semver.cmake

**Step 2 — wire it into** ``CMakeLists.txt``::

  cmake_minimum_required(VERSION 3.14)
  project(my_project)

  include(cmake/git_semver.cmake)
  git_semver(GIT_SEMVER)

  # Use the parsed components anywhere CMake variables are valid.
  message(STATUS "Version: ${GIT_SEMVER}")
  set_target_properties(my_lib PROPERTIES
      VERSION   "${GIT_SEMVER_MAJOR}.${GIT_SEMVER_MINOR}.${GIT_SEMVER_PATCH}"
      SOVERSION "${GIT_SEMVER_MAJOR}"
  )

The variables set after calling ``git_semver(<prefix>)`` are:

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Variable
     - Description
   * - ``<PREFIX>``
     - Full version string (e.g. ``1.2.3-alpha+001``)
   * - ``<PREFIX>_MAJOR``
     - Major version component
   * - ``<PREFIX>_MINOR``
     - Minor version component
   * - ``<PREFIX>_PATCH``
     - Patch version component
   * - ``<PREFIX>_PRE_RELEASE``
     - Pre-release label (e.g. ``alpha``), empty if absent
   * - ``<PREFIX>_BUILD_METADATA``
     - Build metadata (e.g. ``001``), empty if absent

.. note::

   Tags must follow the ``vMAJOR.MINOR.PATCH`` format exactly.
   ``cmake-git-semver`` will set all variables to ``0`` (and emit a
   warning) if no conforming tag is found, so it is safe to use on a
   fresh repository.


.. _cmake-git-version-tracking: https://github.com/andrew-hardin/cmake-git-version-tracking
.. _cmake-git-semver: https://github.com/nunofachada/cmake-git-semver
.. _Google C++ style guide: https://google.github.io/styleguide/cppguide.html
.. _Catch2: https://github.com/catchorg/Catch2
.. _Catch2 CMake integration: https://github.com/catchorg/Catch2/blob/devel/docs/cmake-integration.md

.. note::

   Portions of this page were drafted with the assistance of `Claude Code Sonnet 4.6`.