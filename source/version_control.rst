########################
Version Control for Code
########################

This section deals with tools and practices for version control of
code.  It does not cover version and provenance tracking of data,
meta-data, or analysis products.


git and github
==============

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


