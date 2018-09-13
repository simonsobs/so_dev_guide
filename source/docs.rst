##################
Code Documentation
##################

This section deals with standards and tools for code documention.
This includes inline comments as well as more narrative works that
stand alone (perhaps in a web page or PDF) to provide reference,
tutorial, or background information on code operation or usage.

Documentation System
====================

.. todo:: sphinx is pretty obvious here, but what are the relative
          merits of readthedocs, private servers, github pages, etc?
          What approach to take for private repositories?  Will we
          have collaboration accounts on readthedocs / whatever?

We will adopt the following tools to process and publish SO codebase
documentation:

- sphinx: This code processes reStructuredText input files and can
  produce html, pdf, and many other output formats.
- readthedocs: This is an online service that integrates with github
  and sphinx to serve web versions of documentation.

Attention should be paid that the documentation render properly for
the following targets:

- html
- latexpdf


Plain-text documentation
========================

Use reStructuredText (e.g., create README.rst not README.md).  It is
fully compatible with sphinx and github, and is more standardized than
Markdown (see writeup on `Why You Shouldn't Use "Markdown" for
Documentation`_).

Wrap paragraphs at 80 characters.

