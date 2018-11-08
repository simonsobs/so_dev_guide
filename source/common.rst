#####################################
Common Standards for Code and Process
#####################################

This section deals with code formatting and multi-user work flow that
is common to all SO activities.


Licensing
=========

Clear licensing protects authors, their employers, and the
collaboration.

SO will likely have a variety of public and private repositories.  It
is likely that public code will be licensed in an open source model.
We should pick a license soon and start pasting that on the top of all
the source files.


Grandparent clause
==================

Large bodies of code that we absorb into SO may have incompatible
standards.  Large reformatting jobs should not be undertaken unless
there is an immediate intention to then make extensive modifications
to the code.

In cases where extensive reformatting `is` necessary, commits carrying
the reformatting must not also include any changes to the
functionality or interface.


Documentation
=============

More discussion of documentation can be found in the
:doc:`Documentation page <docs>`.


Release Numbering
=================

In addition to the other ways of tracking and tagging the code, it is
useful to associate clean version tags (such as v1.2.3) to certain
version of your code.  There are many possible, reasonable approaches
to this, and many ways to accomplish the embedding of version
information in the code that is distributed to users.

This Guide recommends the use of "Semantic Versioning", see below.  We
also recommend using github "release tags", and the "versioneer"
package for embedding version tags into python libraries.

Semantic Versioning
-------------------

"Semantic Versioning" is described here: https://semver.org/.  The
idea is that versions are of the form X.y.z, where each of X,y,z is a
non-negative integer, and there are certain rules that dictate whether
changes to the software should induce an increment in X, y, or z.

I'm sure you'll eventually read the whole semver page.  But in the
meantime, know that in the initial period of development, your version
numbers should be 0.x.y.  The major version "0" is special in that
you're "allowed" to make changes to your code's API without
incrementing the major version number.

In some cases, a codebase might go through multiple phases of rapid
API evolution, while still wanting to have public, sequential version
tags.  A fun solution to this is to differentiate between even and odd
Major or Minor release numbers.

versioneer
----------

The "versioneer" tool is a nice way to automate the creation of
version codes for python packages, and to make those codes available
from within the package: https://github.com/warner/python-versioneer.
This is most appropriate for git projects that use distutils or
setuptools (i.e. that have a ``setup.py`` to drive the build and
installation).

Once versioneer is working in your repository, the package will return
informative version strings such as ``0.1.2+5.gc6ca281`` (in this case
indicating that the library is 5 commits beyond the commit tagged as
0.1.2, with commit hash ``c6ca281``).

To get versioneer operating on your python project, do the following:

1. Install versioneer.  ``pip install versioneer`` will do it, but see
   below about using the bleeding edge version from git if you run
   into issues with "cmdclass" in your ``setup(...)`` call.

2. Create, or edit, ``setup.cfg`` (the configuration information for
   setup.py) and add these lines::
     
     [versioneer]
     VCS = git
     style = pep440
     versionfile_source = mylibname/_version.py
     versionfile_build = mylibname/_version.py
     tag_prefix = v
     parentdir_prefix = mylibname-

   Naturally you must replace "mylibname" with the name of your python
   package.  The "tag_prefix" affects how versioneer searches your
   github tags; in this case it will look for tags starting with v,
   such as v0.1.2.

3. Edit setup.py to integrate versioneer's functionality.  That
   amounts to::

     ...
     import versioneer
     ...
     setup(
       ...
       version=versioneer.get_version(),
       ...
       cmdclass=versioneer.get_cmdclass(cmdclass),
       ...
       )

   If you already have a ``cmdclass`` entry, that can be worked
   around; seek advice.

4. Run the versioneer binary, at the top of your source directory
   (where setup.py is), ``versioneer install``. This will check that
   you've made the changes to setup.cfg and setup.py; it will also
   create _version.py in your python source tree, versioneer.py in the
   root level, and will modify a few other git/PyPI files.  ``git
   status`` will show something like:

   	new file:   .gitattributes
	modified:   MANIFEST.in
	modified:   mylibname/__init__.py
	new file:   mylibname/_version.py
	new file:   versioneer.py

   Those can all be committed, along with your changes to setup.cfg
   and setup.py.  A new build should yield informative version
   strings, e.g.::

     $ python -c 'import mylibname; print (mylibname.__version__)'
     0.4.0+2.g13ed14d.dirty

5. All you need to do to bump the version number is to tag the
   relevant commit, with a tag that matches the right format (in this
   example, something like v0.4.0).  The github "releases" feature
   allows you to do this, and to see all the tags.


(Note about ``cmdclass`` -- if your setup.py already modifies the
cmdclass with custom build classes, you need to merge them with the
ones provided by versioneer.  This is easy in the most recent version
of versioneer on github (as of Nov. 8 2018), but is not easy in the
current version available on PyPI, 0.18 (dated Jan. 1 2017).  Once
versioneer has been "set up" on the code, the file versioneer.py in
the root of the source tree is all you need; so your package won't
depend, for the user, on this bleeding edge version of versioneer.)

     
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
.. _Why You Shouldn't Use "Markdown" for Documentation: http://ericholscher.com/blog/2016/mar/15/dont-use-markdown-for-technical-docs/


C/C++
=====

.. todo:: Argue about C/C++ formatting.

Proposal:

- The basic indent shall be 4 spaces (2 is hard to follow, 8 is to
  wasteful; non-powers of 2 are too weird).
- Spaces, not tabs.

