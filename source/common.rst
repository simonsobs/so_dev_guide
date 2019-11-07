=====================================
Common Standards for Code and Process
=====================================

This section deals with code formatting and multi-user work flow that
is common to all SO activities.


Style and Technique
===================

In this document, we'll use "Style" to refer to the appearance of
source code, by which we mean code formatting issues that do not
affect the function of the code.  "Style" includes rules for how much
whitespace should be used in different situations, how long lines of
source code should be, and how one should name identifiers such as
variables and classes.

In contrast, "Technique" refers to the usage of programming language
features to accomplish some desired programmatic behavior.  For
example, a requirement that "global variables should be avoided unless
necessary" is a statement about technique; "global variable
identifiers should be in all caps" is a statment about style.

Detailed style and technique recommendations for specific programming
languages are presented in subsequent chapters.  We will just touch on
a couple of general points here.

Style is not Personal
---------------------

The underlying goal of style recommendations is to improve
readability, so that programmers can understand and modify each
other's work efficiently.  It is helpful if brains and source code
editors aren't struggling due to unfamiliar formatting choices.  Style
rules are thus about code maintainability.

Here are things to keep in mind, about code maintainance in SO:

- The importance of maintainability, and thus of style, varies with
  context.  For example, one-off data analysis scripts do not need to
  be held to the same commenting and technique standards as core
  instrument control codes, even though both might be written in
  Python.
- In many cases we will derive our code from pre-existing works, that
  may or may not follow some reasonable, established style.
  Large-scale reformatting jobs are probably not worth the effort,
  unless substantial modification of the code will then be
  undertaken.
- When a programmer is reviewing new contributed code changes, and
  trying to understand how the behavior of the code is going to be
  affected, then stylistic reformatting is actually quite distracting
  (even if it improves the style, in some sense).  Thus, work that
  makes substantial "style" improvements should be totally separate
  from work that makes changes to behavior or function.  In practice
  this means that style fixes and feature work should be in separate
  git commits, if not separate pull requests.

Behind every great writer is a great editor
-------------------------------------------

If you're having trouble keeping your code compliant with the
recommendations here, perhaps you should be using a different source
code editor.  The formatting guidelines in this document are designed
to be easily activated in the editors ``emacs`` and ``vim``.  If you
often need to code in a text-only terminal (rather than a graphical
desktop environment), then you should probably learn one of these
editors.  If you want to be a cool hacker, you should find out which
of these editors is currently most popular, and then learn the other
one.

If you think the graphical desktop environment is more your style,
there are many powerful editors that can be configured to respect
certain style guidelines.  Find one.  (``vim`` and ``emacs`` can
be run in some graphical environments, and integrate with the
desktop's pretend that they are graphical, but that's not really their selling
point.)

But if you're using ``nano`` (on the command line) or ``Notepad`` (in
your Windows), you will probably become very frustrated with them,
and wish you had invested the time in a smarter editor.

git and github
==============

.. todo:: Separate git (how to use git) and github (how SO uses
          github).

Introduction
============

This section deals with tools and practices for version control of
code.  It does not cover version and provenance tracking of data,
meta-data, or analysis products.


We recommend the use of git for source code tracking.  SO has as an
institutional account on github (https://github.com/simonsobs/), which
hosts private and public repositories, across all domains of SO code.


Introduction to git and github
------------------------------

.. todo:: Provide recommended references and tutorials that are
          appropriate for SO users and patterns.


Additional advice to new users
------------------------------

Users that are new to git/github should pay particular attention to
avoid some common errors.  Please:

1. Do not add temporary files, backup files, or compilation products
   to the repository.  Always run "git status" before you run "git
   commit".  This will tell you about the changes you are going to
   commit.

2. Do not store large data or binary files in a repository that is
   mostly for code, unless absolutely necessary.  Large files are
   annoying because anyone cloning the repository will be forced to
   download those large files from the server.


Guideline: squash and rebase
----------------------------

We encourage contributors to "squash and rebase" whenever it is
appropriate and possible to do so.

**Rebase**: A neat thing about git is that it allows the commit
history to diverge into separate paths, and then "merge" back
together.  This is powerful when needed, but confusing if it is used
often and unnecessarily.  A "rebase" is when you take the commits
you've made in your local branch and ask git to re-position them so
they appear *after* the commits in the master branch.

Here are two commands you should learn how to use:

- ``git pull --rebase`` (to pull down the remote version of the
  repository, and then apply your changes on top of it)
- ``git rebase master`` (to synchronize your topic branch with the
  current master branch)

**Squash**: Sometimes the commit history can be unnecessarily
detailed, with intermediate commits that are not the complete solution
to the problem at hand.  Rather than pushing the full, blow-by-blow
history of your work to the main repository, consider "squashing" your
local commits into a smaller set of commits first.  If you've ever
used ``git commit --amend``, then you will probably like ``git rebase
-i``.

Here's a nice discussion of why we like to squash-and-rebase:
  https://blog.carbonfive.com/2017/08/28/always-squash-and-rebase-your-git-commits/

Here is the relevant part of the git book:
https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History




Guideline: github Push Policies
-------------------------------

.. todo:: Explain how the principals of each SO repository will
          communicate and encorce their Push Policy.


In this section we discuss possible approaches to "Push Policy", by
which we mean the rules that developers should follow when pushing
revisions from their personal respositories to the shared repository
on github.

In a git repository, different "branches" can be used for different
purposes.  Normally, the main copy of the code is in a branch called
"master".  Each repository must have policy about about how revisions
end up in the "master" branch.  To some extent this policy can be
enforced using repository configuration options in github.

Consider two examples of Push Policy, which lie near two extremes of a
spectrum:

**"Unrestricted Push to Master"**

    In this policy, all users are allowed to push their commits
    directly to the github:master branch.  This is appropriate in the
    case that the repository:

    - is being developed by only a small group of people.
    - is being used by only a small group of people (probably the
      developers).
    - is in the early stages of development, where there is no
      expectation of stability and features are rapidly evolving.

**"Pull Request and Review"**

    In this policy, only a small set of users are permitted to accept
    revisions into the master branch.  Other developers submit their
    code as a "pull request", meaning that it has been developed on a
    separate repository or in a separate branch from the main SO
    master.  The Pull Request is reviewed by the repository's
    guardians, and requests may be made for amendments.  This level of
    control is appropriate in the case that the repository:

    - must maintain stability in its external interface.
    - must maintain stability in its performance.
    - has a large number of developers or a large user base.


Guideline: git Commit Messages
-------------------------------

Well crafted git commit messages improve the quality of a repository's history.
They improve readability and communicate the context of a change to other
developers. The author of `this blog post`__ put it best when he wrote:

.. _how_to_write_a_git_commit_message: https://chris.beams.io/posts/git-commit/
__ how_to_write_a_git_commit_message_

    A project’s long-term success rests (among other things) on its
    maintainability, and a maintainer has few tools more powerful than [their]
    project’s log. It’s worth taking the time to learn how to care for one
    properly.

The same author proposes the following seven rules for writing a great git
commmit message, which we suggest you follow:

#. Separate subject from body with a blank line
#. Limit the subject line to 50 characters
#. Capitalize the subject line
#. Do not end the subject line with a period
#. Use the imperative mood in the subject line
#. Wrap the body at 72 characters
#. Use the body to explain what and why vs. how

Rules 1-5 focus on the title of the commit message, which is often presented
when using certain other git commands (i.e. ``git rebase -i``, ``git log
--oneline``) or even the GitHub interface (i.e. the latest commit title
associated with each file is displayed next to the file). Since it is used so
widely we emphasize following especially rules 1 and 2.

| The Pro Git book recommends very similar guidelines:
| https://www.git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines

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
   status`` will show something like::

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

5. (Optional) If you are using Sphinx to build documentation for your project
   you can have Sphinx determine the project version number from versioneer by
   importing ``__version__`` in your ``conf.py`` file::

    from mylibname import __version__ as mylibname_version

   You should then change the ``version`` and ``release`` fields to
   ``mylibname_version``::

    # The short X.Y version
    version = mylibname_version
    # The full version, including alpha/beta/rc tags
    release = mylibname_version

6. All you need to do to bump the version number is to tag the
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


