=====================================
Common Standards for Code and Process
=====================================

 .. highlight:: none

This section deals with code formatting and multi-user work flow that
is common to all SO activities.  This includes some general
style guidlines, a discussion of git and github usage, and advice on
how to have sensible version codes in code packages.


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


Git and Github
==============

In this section we discuss best practices for use of git and github,
when developing code for Simons Observatory.

Resources for beginners
-----------------------

`git` is "source code management" software, that you would usually run
on the same computer where you are editing code, that helps you to
track changes in source code over time.  `github.com
<https://github.com>`_ is one of several websites that helps groups of
people to collaborate on code, using git under the hood.

Basic git and github usage will not be addressed in detail here.  New
users should do some basic reading on this topic, or ask for help from
a local expert, to get started.  There is a wide variety of git and
github advice available online.  Here are a few good tutorials and
introductions:

- https://git-scm.com/docs/gittutorial
- https://guides.github.com/introduction/git-handbook/
- https://guides.github.com/activities/hello-world/

To make sense of the rest of this section, you should probably:

- have git installed on the computer you want to use
- have a github account
- have a handle on some basic git terminology, including: repository,
  commit, push.


Additional advice on git usage
------------------------------

The points below are intended to address common errors as well as
alert users to useful intermediate features of github.  Tips for new
users are presented first, then more advanced topics presented later
in the list.

Do not commit garbage
`````````````````````

Do not add temporary files, backup files, or compilation products to a
repository.  Always run ``git status`` before you run ``git commit``.
This will tell you about the changes you are about to commit.  You
will generally run into trouble if you use the ``git add -a``
shortcut... unless you have a well-crafted `.gitignore file
<https://git-scm.com/docs/gitignore>`__ file in place!

Do not mix code and data in a repository
````````````````````````````````````````

The concern here is that large data files can "weigh down" an
otherwise light-weight code repository.  This is especially true if
the data files are sometimes changed -- because every git clone
includes a complete copy of the complete history of the repository,
you aren't getting rid of those old data files when you commit new
versions of them.  Every user of the repo will be dragging them
around, forever.

There are exceptions to this rule... some repositories will be
designed explicitly to contain data.  But be aware of the cost of
storing large files in a git repo.

Rebase instead of merge
```````````````````````

A neat thing about git is that it allows the commit history to diverge
into separate paths, and then "merge" back together.  This is powerful
when needed, but confusing if it is used often and unnecessarily.  A
"rebase" is when you take the commits you've made in your local branch
and ask git to re-position them so they appear *after* the commits in
the master branch.  Instead of a commit history that splits in two and
rejoins, you have a commit history that is a single line of sequential
changes.

Here are two commands you should learn how to use:

- ``git pull --rebase`` (to pull down the remote version of the
  repository, and then apply your changes on top of it)
- ``git rebase master`` (to synchronize your topic branch with the
  current master branch)

Squash your commits into logical units
``````````````````````````````````````

Sometimes the commit history can be unnecessarily detailed, with
intermediate commits that are not the complete solution to the problem
at hand.  Rather than pushing the full, blow-by-blow history of your
work to the main repository, consider "squashing" your local commits
into a smaller set of commits first.  If you've ever used ``git commit
--amend``, then you will probably like ``git rebase -i``.

The corollary to "do not push long blow-by-blow commit histories to
github" is "feel free to use blow-by-blow commits in your local work
flow".  I.e., because you know how to rewrite the commit history, you
can use your local commits to track the work in a more fine-grained
way than you would eventually want to have in the main repository.
You can commit "WIP" (work-in-progress) commits to save one part of
the work while you focus on some other aspect of the problem.  Before
pushing the commits, they can be re-ordered, joined together, and
decorated with helpful commit log messages.

Here's a nice discussion of why we like to squash-and-rebase:
https://blog.carbonfive.com/2017/08/28/always-squash-and-rebase-your-git-commits/

Here is the relevant part of the git book:
https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History

Fix it before you push
``````````````````````

There are git commands that allow you to go back and fix mistakes
you've made (such as re-wording a commit message, or removing some
garbage file from a repository).  "Rewriting history" on a single
branch of the code that you control is completely acceptable git
practice.  However, modifying history on a shared branch (such as a
branch that you are working on with others, through github) is all but
forbidden.  When you rewrite history on a shared branch, it can be
difficult for other users to absorb those changes into their clones of
the repo.

Normally git will prevent you from pushing such changes to a remote
repository, unless you specify you want to "force" the push.  github
repositories will often be set up to reject such pushes (even if
forced).  But it is important to be careful about this, in case the
repository has not been locked down.

There are cases where a force-push to github is acceptable.  These are
cases where you know you are in sole control of a branch, and you're
cleaning it up in advance of merging into the master branch.  The
"rebasing" and "squashing" described above are common history
modification practices that might take place just before a branch is
merged.

Git Style Recommendations
-------------------------

Commit Messages
```````````````

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

The Pro Git book recommends `very similar guidelines
<https://www.git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines>`__.

Here is an example::

  Change config file format to yaml

  The previous format was JSON, so previous config files will still be
  compatible with the new code.  We are moving to yaml primarily
  because we want to support comments in the config file.


**Note for deep repositories:** Some repositories contain distinct
sub-modules that can operate more or less independently.  In such
cases it may be appropriate to declare, in the commit subject line,
the sub-module that is affected.  This helps someone browsing the log
to identify changes that affect some sub-system of interest.  For
example::

  HK format: change timestamp fields to G3Time

The alternatives to this are "Change timestamp fields to G3Time",
which does not communicate the sub-system, or "Change timestamp fields
to G3Time in HK format", which communicates the same information but
buries the hierarchical part (HK format) in an otherwise
domain-specific description.

The SO Github Organization
--------------------------

Simons Observatory has an institutional "Organization" on github,
where members collaborate on a wide variety of code used in instrument
control, low-level data processing, data simulations, analysis, and
everything else.

Our home on github is https://github.com/simonsobs/.

Administration
``````````````

Administration of the Simons Observatory github organization is
supervised by the Data Manager, with many administrative powers
delegated to a set of Organization Admins.  There is one Organization
Admin for each of three subsystems: "Science" (covering the work of
the AWGs), "Pipeline" (covering the work of the PWGs) and "Instrument"
(covering the work of the TWGs).  Contact information for the current
admins will be kept up-to-date on this wiki page:
http://simonsobservatory.wikidot.com/main:wiki-mail .

The primary role of Organization Admins is to add and remove members
from the organization, to configure Teams, and to change repository
settings in cases where this is not available to the Repository Admin
(see below).

Each repository also has one or more "Repository Admin", who has a
high level of control over that repository.  If you want to contact a
Repository Admin, and you are not sure who that is... ask an
Organization Admin to help.  Repository admins should take care to
exercise their privileges only within the rules described here.  For
example, it might be possible for an admin to make a private
repository be public; but that power is specifically restricted as
described in :ref:`The Covenant of the SO Github` (and below).  The
Repository Admin will also be the contact person for issues relating
to "Openly Contributed Code" compliance.


User Accounts
`````````````

In order to be added to the SO github Organization, you must first
have a general github.com account; then you must email one of the
Organization Admins (see link above).

If your username is not similar to your real name, it will be
difficult for collaborators to find you and work with you on github.
One way to improve this is to include your full name, or your first
name and last initial, in your github profile.

Your membership in the SO github Organization can be Public or
Private.  If Public, this means that anyone on the internet will be
able to see that your github username is associated with SO.  If
Private, then only other Organization members will see this fact.  By
default your membership is Private.  To set it Public, make sure
you're logged into your github account and then go to
github.com/simonsobs/people.  Find your username in the list, and
change the visibility setting from "Private" to "Public."

A list of users, with email addresses and full names, will be
maintained by the Data Manager and periodically reviewed against
membership lists.  A user who is no longer an SO member may be removed
from the organization.


User Privileges
```````````````

By default, all Organization users will have "Read" access on all SO
repositories.  In order to get "Write" access to a repository, which
will allow you to make commits to the repo, a Repository Admin must
add you (possibly using a Team).

Users are likely to have Read access to many "private" repositories,
including ones that contain some sensitive information (such as
preliminary science results or secure access information).  Please
don't share, outside SO, things you find in private repositories
unless you know it's acceptable to do so.

Admin privileges on a repo should normally only be held by a small
number of experienced users.  Giving a whole team "Admin" on a repo is
probably a bad idea (except in the case of special Teams designed for
admin purposes!).

Github Teams
````````````

A github Team is a named group of users that can be granted
permissions, in bulk, on a repository.  This simplifies administration
in cases where the same group of people need to have certain
privileges on a non-trivial number of repositories.

The Organization Admins can create teams, as needed, to simplify
repository administration.  We will not get too fine-grained on this,
though.  We expect that Teams will normally correspond closely to an
AWG, PWG, or TWG.  Smaller, ad-hoc groups will be discouraged in favor
of per-user permissions for the affected repositories.

Issues, Projects, Wiki
``````````````````````

Github has integrated features for communication and planning.  Each
working group should consider whether to use these features, as a
complement or a replacement for separate channels such as email and
Slack.  The main advantage of using the github channels is that they are
strongly integrated with each other and with the code; one can easily
click through from a Project to an Issue, to the Pull Request that
resolves the issue.

*Issues*: This feature allows users to report bugs, request features,
or start a more general discussion.

*Projects*: Projects support the factoring of complex or long-term
code changes into smaller work units.  The integration with github
means that you can tie certain items to github Issues, or assign items
to particular github users.  As work progresses you can move items
from one list (say, "to-do") to another list ("done").  github
projects can be defined at the Organization level, or can be attached
to a particular repository.  Groups such as TWGs and PWGs are
encouraged to maintain a single, organization-level project page as a
way to communicate their plans and activity to the broader SO
community.

*Wiki*: github repositories can host a wiki.  This could be used to
provide supplementary documentation, such as work-arounds for recently
emerged bugs, or for meta-documentation, such as a description of
various long-lived branches on the repository.  (Note that for general
user documentation, other approaches are recommended; see the relevant
chapter of this guide.)

"Watch" and learn
`````````````````

A good way to monitor what's happening in a repository on github is to
"Watch" it (a quick-activation button is available near the top of
each repo's front page).  This works on any public repository on
github, as well as on private repositories within the SO Organization.
Once you're watching a repository, you'll get a "notification" (an
email, typically) when there are pull requests or other significant
changes.  (There are actually 4 levels of verbosity that you can
configure here.)

When you (or your Team) get added to an SO repository, the "Watch"
will be enabled automatically; if you find updates annoying you can
un-watch the repo.

Collaborative Development Model: shared repository
``````````````````````````````````````````````````

SO encourages the *shared repository model*, rather than the *fork and
pull model*.  The difference between these models is described in the
`github.com documentation
<https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-collaborative-development-models>`__,
and elsewhere.

But basically what this means is that our preferred way for SO users
to submit code changes is to do so directly on the SO github
Organization repositories, using "topic branches".  This can be done
without "forking" (see next section).

The basic steps are described below, but this is a very standard
procedure that you can read about online.  Note that collaboration is
more the domain of github (and similar services) rather than git -- so
you'll find more information on the `github documentation pages
<https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/proposing-changes-to-your-work-with-pull-requests>`__
than in, say, the git book.

#. Clone the SO repo to your system, using ``git clone``.
#. Create a topic branch using ``git checkout -b``.

   - Topic branches will usually only stick around until the changes
     are merged into the master branch, so it's ok to give the branch
     a short name describing its immediate purpose, e.g.:
     ``fix-docstrings`` or ``new-dust-model``.

#. Make edits and commit them.
#. Push your topic branch to SO github using ``git push``.

   - At this point your branch will be visible to other members of the
     github Organization.  Other users can "pull" your changes to
     their local copies to review or test them.  You, and other users,
     may make further commits on this branch.
   - Although the code changes are now broadly visible, the
     collaborative review process does not usually start until you
     issue a "Pull Request".

#. Go to github.com and open a "Pull Request" (PR) on your branch.

   - You can open a PR just to start discussion about some changes,
     even if you feel that the changes so far are not ready for
     merging.  Use the green button option "Create draft pull request"
     instead of "Create pull request".
   - If your PR is meant to address a specific "Issue" that someone
     raised on github, you should link to that issue in your PR
     comment.  Github has convenient shortcuts to help with that.
   - To draw specific people's attention to the PR, you may call them
     out in the PR comments, using ``@username``.  To request a formal
     review, use the "Reviewers" widget in the PR window.

#. Merge your changes into the `master` branch.

   - When everyone is satisfied with the changes, they can be merged
     into master.
   - PRs have a formal "Review" feature.  Depending on how the
     repository is set up, a formal Review may be *required* prior to
     merging.
   - In some cases it might be acceptable for you to "self-merge" the
     PR, even without any review or discussion.  Check with the
     Repository Administrator on this.

   
Forking (what is it good for)
`````````````````````````````

You may find advice online for contributing to Open Source codes that
begins with the recommendation that you create a fork of the
repository on your personal github account.  **Forking is not
necessary and is not recommended** for users who are members of the
Organization, and who have write privileges on the repository in
question.

The process of "fork, modify, and pull request" makes a lot of sense
in the case of large, public projects where access to the main
repository is highly guarded, and contributions from the general
community are only "pulled in" when they're really ready.

We do not have a hard rule against forks; we simply feel that the
collaborative nature of SO work is better matched to the topic-branch
approach.

Repository Administration
-------------------------

Repository Admins should specify the procedures that contributors must
follow to have their changes incorporated into the repository.
Consider two possible policies:

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


By default, repositories on github permit "Unrestricted Push to
Master".  This is a simple system, because it does not require the use
of branching or forking.

We strongly recommend that adminstrators adopt a policy of **"Pull
Request and Review"**, and that they configure the github repository
to enforce that policy.  The configuration is achieved as follows:

#. Go to the repository page, ``github.com/simonsobs/your-repo``.
#. Click on Settings tab.  If you don't see that tab, perhaps you
   don't have Admin privileges on the Repo.
#. In the left column menu, Click on "Branches".
#. Under "Branch protection rules", see if there is an entry that
   includes the "master" branch, and if so click its "Edit" button.
   If not, click "Add rule".
#. In the settings for the Branch protection rule, make sure it
   applies to the master branch.  Then enable "Require pull request
   reviews before merging".

If you want to activate more restrictions, that's probably fine.  It
depends on how much control you want to impose on the merging process.
There are good reasons to enable, or not enable, each of the other
protection settings.

It's also important to communicate your policy to potential
contributors (especially if you expect the contributer base to grow
beyond a small core).  One common way to do this is to explain the
process in a ``CONTRIBUTING.txt`` (or ``.rst`` or ``.md``) file, in
the root level of the repository.  Here are links to a couple of
examples, from public SO repositories:

- https://github.com/simonsobs/pixell/blob/master/CONTRIBUTING.rst
- https://github.com/simonsobs/so3g/blob/master/CONTRIBUTING.rst

Be careful to consider your target audience -- are you addressing
collaborators inside SO, or the general public, or both?


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


