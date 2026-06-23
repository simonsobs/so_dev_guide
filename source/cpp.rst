=====
C/C++
=====

Overview
========

C++ is an important part of the software ecosystem of SO, and is used in important and
performance-critical code. C++ is a complex language and very permissive on formatting.

In addition, formatting and styling from older standards (C++98, C++03) is very
different from modern C++ (C++11 and later). As a result, these guidelines will
not require old codebase to be reformatted, but will require new code to follow a 
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
write C++, we will adopt a modified Google C++ style guide. For any rule not explicity
specified in this document, please refer to the Google [C++ style guide](https://google.github.io/styleguide/cppguide.html)

In addition to the style description, we will provide a config file for clang-format
that can automatically format code. In case you find yourself working on code that is
not formatted according to the style, you can maintain the existing style. However,
we higlhy recommend to format the code in a different branch and submit a pull request.


Indentation
-----------

Indentation is one of the aspects of code formatting that is important to be consistent
across codebases, especially since we use multiple languages.

We will use 2 or 4 spaces as the intendantion for C++.

Tabs are not allowed for indentation.

Line width
----------

The maximum line width allowed is 120 characters.


Naming Conventions
------------------

The name of a variable, function or class is one of the most important aspects of code
readability. It can immediately inform about the puspose of the named thing. Please avoid
single letter names, except for loop variables, even if it is a commonly understandable
variable.

We will utilize the following naming conventions:
1. Class and struct names should be in PascalCase, e.g. `MyClass`.
2. Function names should be in camelCase, e.g. `myFunction`.
3. Variable names should be in snake_case, e.g. `my_variable`.
4. Constants should be in ALL_CAPS with underscores, e.g. `MAX_SIZE`.
5. Namespaces should be in snake_case, e.g. `my_namespace`.


Use of Language Features
------------------------
  .. todo:: We will add guidelines on the use of language features, such as smart pointers, 
    exceptions, etc. We will also provide guidelines on the use of modern C++ features
    such as lambda functions, auto keyword, etc.

Documentation of Code
=====================
Documentation of the code provides information about the code to users and developers alike.
There are two types of documentation that are important: inline comments, and API docstrings.

For comments `/*..*/` and `//` are acceptable`, but try to be consistent within the
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

Unit testing is an important part of software development. It helps ensure that the code
is working as expected, helps catch bugs early and verify that the code is not regressing
when feature or changes are made. Testing suites are only expected to grow over time.

Due to the importance of unit testing, we will require that all new code be accompanied by at
least one unit test. The unit test should be in a separate file, and should be named
`<name>_test.cpp`, where `<name>` is the name of the file being tested.

[Catch2](https://github.com/catchorg/Catch2) is the unit testing framework for C++ we will
use for SO as it is easy to use, represents tests a normal boolean expressions and
also allows to benchmark code.



