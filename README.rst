"Simons Observatory Developer Guide" Developer Guide
====================================================

This is the source document for the Simons Observeratory Developer Guide. The
guide is hosted on simons1 here:
https://simons1.princeton.edu/docs/so_dev_guide/html/

To render the source files into nicely formatted html or PDF versions,
you will need sphinx.  This can be obtained through most linux package
managers (e.g. apt-get install python3-sphinx).  For more details,
visit http://www.sphinx-doc.org/en/master/usage/installation.html.

To render the html version of the Guide, run::

  make html

Then open build/html/index.html in a web browser.

To create a pdf verison of the Guide, run::

  make latexpdf

Then open build/latexpdf/SODeveloperGuide.pdf somehow.


Version / Release tags
----------------------

Our versions are numbered in the form X.y.z.  These correspond to
github release tags vX.y.z.  The policy on incrementing versions is as
follows:

- The major version X should be incremented when there is a major
  reorganization of the text (such as rearranging chapters).  During
  initial development (X=0), don't worry about that.
- The minor version y is incremented when there are significant
  changes in policy or best practices, or when a significant new
  section is added (such as a new chapter).
- Otherwise, increment the patch version, z.

Note that the "version" and "release" are automatically generated, in
conf.py, by a script taken from versioneer_.  This uses the most
recent git tag of the form vX.y.z.  If the git tree is exported, a
trigger in .gitattributes will insert the latext such information to
version.py.

.. _versioneer: https://github.com/warner/python-versioneer


Parts, chapters, sections
-------------------------

The guide is organized into parts (currently 2).  Each part has its
own table-of-contents listing, in index.rst.  Each chapter is in a
separate rst files.  The sphinx rst processor will automatically
detect a hierarchy of section markup, in any given file.  If possible
use only = and -, since this is the most pleasing in raw text.  I
propose the following ordering::

  ==============================
  H1 Header (chapter, mandatory)
  ==============================

  --------------------
  H2 Header (optional)
  --------------------

  H3 Header
  =========

  H4 Header
  ---------

