==========================
Copyright, Licensing, etc.
==========================

.. warning:: The policies described in this chapter need to be
             approved a high level.  Until that happens, do not take
             any drastic actions based on the text below!


Introduction
============

If you want to skip to the important parts, they are `Policy on Openly
Contributed Code`_ and `Copyright and License Cookbook`_.

Because of the complex structure of private entities, academic
institutions, and individuals working on SO code, the collaboration
will benefit from copyright and licensing practices that place minimal
restrictions on the use and re-use of code.  Such an `Open Source`_
approach has been adopted by a huge range of scientific and
non-scientific projects.

There is a bit of a complex interplay between copyright, licensing,
and exposure (whether a code is public or private), and this chapter
recommends certain approaches that will help protect the rights of
code contributors as well as the needs of the observatory.

The discussions and recommendations in the sections below are intended
to apply broadly to code that is important for the timely success of
the Observatory.  The Data Manager (DM), the TAC (Theory and Analysis
Committee), and the TC (Technical Committee) are the ultimate
authorities for enforcing these standards as they deem appropriate,
and for resolving disputes that involve shared collaboration resources
(such as the SO Github organization).

At the very end of this section you will find instructions for how to
record copyright and license information in your codebase.


Policy on Openly Contributed Code
=================================

We will use the designation "Openly Contributed Code" to describe
repositories that meet a certain desired standard for being
unencumbered by restrictive licenses.  Such designation is desirable
to Simons Observatory, because open licensing is an assurance that
access to the code will not be revoked at any point in the future.
The designation should also provide reassurance to individual
contributors, because the open license gives them access to their own
contributions as well as the contributions that others have made to
the repository.

The following points describe how we will work with Openly Contributed
Code in Simons Observatory.

1. We define "Openly Contributed Code" to be source code that is
   created for or made available to the Simons Observatory through a
   simple Open Source license, such as the BSD or MIT License, and
   that is stored (even if only as a fork) on the SO github
   organization.

2. All repositories hosting Openly Contributed Code must include a
   license file that states the terms of the license.  In cases where
   such a license file does not exist, some care should be taken to
   confirm that the copyright holders (i.e. the contributors of the
   code in the repo) are all on board with releasing their code under
   such a license.

3. When someone contributes code to an Openly Contributed Code
   repository, they are agreeing that their contributions may be used
   by others under the terms of the license in the repository.  Note
   that they (or their employers) may retain the copyright to their
   contributions.

4. In some cases, an Openly Contributed Code repository may be in the
   "private" state on github.  The code in private repositories should
   be considered as proprietary to SO, notwithstanding the Open
   License stated therein, and may not be treated as public code nor
   freely shared outside of the collaboration.  Decisions on when and
   how to take codes from the private state to the public state will
   be made by the DM/TAC/TC.  In other words, each contributor to a
   private repository does not gain the authority to make public all
   of the contributions to that repository; rather, each contributor
   acknowledges that the decision to make the code public lies with
   the DM/TAC/TC.  The responsible authorities will endeavor to
   respect the wishes of the authors, while protecting the mission of
   the Observatory.


Discussion
==========

Importance of Licensing and Copyright
-------------------------------------

Mission-critical SO source code must be clearly licensed so that
there is no risk of loss of access for the duration of the project.
SO must have sufficient rights to use, modify, and release such code without
significant burden (such as licensing fees or inappropriate
attribution requirements).  This condition is likely to be satisfied,
provided that any of the following is true:

- SO controls the copyright of the code.
- The code is openly licensed.
- The code is not openly licensed, but a specific license has been
  obtained that will grant the necessary rights over the necessary
  time period.

In contrast to "Openly Contributed Code", we defined "Specially
Contributed Code" to be source code that is licensed to SO through
some mechanism other than a full Open Source license.  We do not
expect this to happen very often, but if it does it will be good to
have a word for it.


Copyright
---------

The person or entity that holds the "copyright" of a work may
determine how the work may be used by other entities.  It is *not*
necessary for some Simons Observatory legal entity (such as the
project office or the Foundation) to hold the copyright of all
critical code.  Rather, it is only necessary that collaboration
members have sufficient license to use, modify, and release the code.
For simplicity, we recommend that each contributor (or in some cases
their employer) retain the copyright of their contributions, and
instead grant continuing use of those contributions to the Simons
Observatory Collaboration through an open license.

In the context of source code, the copyright holder has the sole right
to license the code for use by others; the importance of the license
is discussed in the next section.


Licensing
---------

The copyright holder of a work may grant licenses to other people in
order that they can make use of, modify, or redistribute the work,
under some set of conditions.

The Open Source approach is a simple way to ensure that individual
contributors get credit for and maintain access to their contributed
source code, while at the same time ensuring that the SO codebase does
not evolve into a complex and risk-laden system of closed, licensed
software.  Open Source ensures that we will all have access to the
contributed code, forever.

Note that the absence of a copyright notice and license does not imply
that a work is in the public domain.  The best way to make code freely
usable is by explicitly licensing the work, for certain uses, in the
distributed source code text.

For general information about the principles of Open Source software,
see https://opensource.org/osd and the other pages at that site.

We recommend that Openly Contributed Code be licensed under the `BSD
2-Clause License`_. Similar licenses, such as the `MIT License`_, are
also acceptable.  These licenses, in essence, allow for the free
modification and use of the source code, but require any public
release of the modified source code to include the original copyright,
license, and disclaimer notices.


Public vs. Private Repositories
-------------------------------

When code resides in a "private" repository on the Simons Observatory
github organization, it is considered to be in a protected,
proprietary state, even though it may contain licensing text that
suggests it is Open Source software.  SO members must not make such
code public, nor distribute it to members outside the collaboration,
except as directed by the appropriate authorities (DM/TAC/TC).

Some SO repositories will be private, initially, and become public
later.  The transition to public should occur only once all the
following conditions have been met:

* The copyright and licensing information is clear and accurate.
* The code has been reviewed to ensure that no software licenses would
  be violated by such publication (i.e., ensure that all license
  requirements for imported codes have been met).
* The primary developers of the code have been consulted.
* The Data Manager (for DAQ and PWG codes), the TAC (for AWG
  codes), or the TC (for TWG codes) agree to the change.

An exception to the above procedure is allowed for the case when a
repository is being newly created, and is kept private during initial
setup but then quickly (within a few days) made public.  In such
cases, consultation with the DM/TAC/TC is not necessary.

Acknowledgment Requirements
---------------------------

In some cases, developers within SO may want to impose additional
restrictions or requirements on the use of code they have produced.
For example, it is not uncommon to see a statement of the form "If
results from this code are used in a scientific publication, then
*some text* must be included in the acknowledgments, and *some
paper* must be cited."

Some contributors may object to having their work encumbered by a
strong citation requirement clause.  So such requirements should not
be applied without consensus among the contributing developers.  The
DM/TAC/TC should be consulted if consensus cannot be reached.

External Collaboration Opportunities
------------------------------------

As an author of or expert in the use of a particular piece of Openly
Licensed software, you may be asked by some external entity (for
example, another telescope collaboration) to assist it in the use of
that software for some non-SO project.  In such cases, it may be
reasonable to request "External Collaborator" (EC) status on the
project in exchange for your advice on how to best use the software.
As a courtesy, any developer that has contributed significantly to the
codebase in question should be made aware of the arrangement, and
offered the same EC opportunity.  (This courtesy should be applied
even if the SO point of contact is already happy to provide assistance
without quid pro quo.)


Copyright and License Cookbook
==============================

Stating Copyright
-----------------

Near the top of every source code file, state the copyright and
mention the license.  This should look something like::

  # Copyright (C) 2018 Members of the Simons Observatory collaboration.
  # Please refer to the LICENSE file in the root of this repository.

If you later make edits to this file, update the copyright year to
include the date of all changes.  For example the date may ultimately
be something like "2018-2020, 2022."  It is not necessary or helpful
to update the date string unless actual changes are made.

Note that we point the reader elsewhere to learn about the license
conditions.  Although one often encounters codes where a complete copy
of the license is stated at the top of every source file, this is
awkward and not legally necessary, so let's not do it unless we have
code where individual files are likely to be extracted and somehow
misused.

The vagueness of *"Members of the ... collaboration"* would probably
be a concern if the code were not openly licensed.  The details of
exactly who owns the copyright to each line of code could probably be
figured out; but it's largely irrelevant since we're making all those
lines freely available.

Declaring the License
---------------------

At the top level of your repository, clearly state the license
conditions.  The best way to do this is to have a text file called
``LICENSE``, that either contains the license (e.g. the text from the
`BSD 2-Clause License`_) or contains instructions on how to find the
licensing information (as is done, for example, `here
<https://github.com/mozilla/gecko-dev/blob/master/LICENSE>`_).

Inherited Licenses
------------------

If you have introduced source code from another project into an SO
repository, please endeavor to respect the licensing conditions of
that code.  This means:

- Make sure that you understand and accept the conditions of the
  license.  Some licenses may constrain the ways in which you can
  distribute modified code (e.g. `SOFA`_ forbids the distribution of
  modified routines unless you also change the names of the routines).
  Even some "Open Source" licenses, such as `GPL`_, have strict
  requirements on how derivative code can be distributed.
- If the imported code requires you to preserve the
  license/copyright/disclaimer, take care to do so.  It may be
  necessary to copy some license information into your project's
  LICENSE file, perhaps under a heading such as "This repository
  contains code by *developer*, which is distributed under the
  following license and conditions: ...".
- If you modify imported code, make a clear note that you have done
  so, near the top of the source code file.


.. _`Open Source`: https://opensource.org/osd
.. _`MIT License`: https://opensource.org/licenses/MIT
.. _`BSD 2-Clause License`: https://opensource.org/licenses/BSD-2-Clause
.. _`SOFA`: http://www.iausofa.org/tandc.html
.. _`GPL`: https://opensource.org/licenses/gpl-license
