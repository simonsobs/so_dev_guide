==========================
Copyright, Licensing, etc.
==========================

.. warning:: The policies described in this chapter need to be
             approved a high level.  Until that happens, do not take
             any drastic actions based on the text below!

Introduction
============

Because of the complex structure of private entities, academic
institutions, and individuals working on SO code, the collaboration
will benefit from copyright and licensing practices that place minimal
restrictions on the use and re-use of code.  Such an `Open Source`_
approach has been adopted by a huge range of scientific and
non-scientific projects.

Note that the absence of a copyright notice and license does not imply
that a work is in the public domain.  The best way to make your code
freely usable by others is with an explicit statement that you, as
creator of the work, wish to do so.

The Open Source approach is a simple way to ensure that individual
contributors get credit for and maintain access to their contributed
source code, while at the same time ensuring that the SO codebase does
not evolve into a complex and risk-laden system of closed, licensed
software.  Open Source ensures that we will all have access to the
contributed code, forever.

The discussions and recommendations in the sections below are intended
to apply to all "mission-critical" code, by which we mean all software
developed or contributed by collaboration members in order to meet the
scientific and related goals of the SO collaboration.

At the very end of this section you will find instructions for how to
record copyright and license information in your codebase.

Copyright
=========

The person or entity that holds the "copyright" of a work may
determine how the work may be used by other entities.  It is *not*
necessary for SO to hold the copyright of all critical code.  Rather,
it is only necessary that SO have sufficient license to use and modify
the code.  For simplicity, **we encourage developers who are funded by
SO, or who are otherwise free to do so, to grant copyright of their
code to "Simons Observatory Collaboration"**.  But it is also
completely acceptable for developers to hold copyright of their code
individually, or to assign copyright to their employers (some
universities and funding bodies may require this).

In the context of source code, the copyright holder has the sole right
to license the code for use by others; the importance of the license
is discussed in the next section.

Licensing
=========

The copyright holder of a work may grant licenses to other people in
order that they can make use of, modify, or redistribute the work,
under some set of conditions.

Mission-critical SO source code must be clearly licensed such that
there is no risk of loss of access for the duration of the project.
SO must have sufficient rights to use and modify the code without
significant burden (such as licensing fees or inappropriate
attribution requirements).  This condition is likely to be satisfied,
provided that any of the following is true:

* SO controls the copyright of the code.
* The code is openly licensed.
* The code is not openly licensed, but a specific license has been
  obtained that will grant the neccessary rights over the necessary
  time period.

We define "Openly Contributed Code" to be source code that is created
for or made available to the Simons Observatory through a simple Open
Source license such as the BSD or MIT License.

We define "Specially Contributed Code" to be source code that is
licensed to SO through some mechanism other than a full Open Source
license.  We do not expect this to happen very often, but if it does
it will be good to have a word for it.

When users contribute code to the Simons Observatory github
organization, within a repository that does not already have an
explicit license, the collaboration will reasonably assume this to
constitute "Openly Contributed Code".  Thus, code must not be
contributed to the SO github organization unless one or more of the
following conditions is met:

* The code has clear copyright and license information attached.
* The contributor accepts that they may retain copyright of the
  original work, but they grant SO collaboration members an implicit
  license to modify and use the code for the duration of SO.

If you would like to set up open licensing on your contribution, **we
recommend the use of the** `BSD 2-Clause License`_. Similar licenses,
such as the `MIT License`_, are also acceptable.  These licenses, in
essence, allow for the free modification and use of the source code,
but require any public release of the modified source code to include
the original copyright, license, and disclaimer notices.


Public vs. Private Repositories
===============================

When code resides in a "private" repository on the Simons Observatory
github organization, it is considered to be in a protected,
proprietary state, even though it may contain licensing text that
suggests it is Open Source software.  SO members must not make such
code public, nor distribute it to members outside the collaboration,
except as directed by the appropriate authorities (Data Manager or
SOTAC).

Some SO repositories will be private, initially, and become public
later.  The transition to public should occur only once all the
following conditions have been met:

* The copyright and licensing information is clear and accurate.
* The code has been reviewed to ensure that no software licenses would
  be violated by such publication (i.e., ensure that all license
  requirements for imported codes have been met).
* The primary developers of the code have been consulted.
* The Data Manager (for DAQ and PWG codes) or the SOTAC (for AWG
  codes) have been consulted.


Acknowledgment Requirements and External Collaboration Opportunities
====================================================================

In some cases, developers within SO may want to impose additional
restrictions or requirements on the use of code they have produced.
For example, it is not uncommon to see a statement of the form "If
results from this code are used in a scientific publication, then
*some text* should be included in the acknowledgments, and *some
paper* must be cited."  Such additional license requirements may not
be compatible with "Openly Contributed Code", and the SOTAC and/or
Data Manager should be contact prior to adding such clauses to a
license.

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


Practical Recommendations
=========================

Near the top of every source code file, state the copyright and
mention the license.  This should look something like::

  # Copyright (C) 2018 Simons Observatory Collaboration.
  # Please refer to licensing information in the root of this repository.

If you later make edits to this file, update the copyright year to
include the date of all changes.  For example the date may ultimately
be something like "2018-2020, 2022."  It is not necessary or helpful
to update the date string unless actual changes are made.

At the top level of your repository, clearly state the license
conditions.  One way to do this is to have a file called ``LICENSE``,
that contains the text from the `BSD 2-Clause License`_.  That file
can also contain any *imported* licenses -- i.e., if you have included
source code that is licensed to you by someone else, there may be
requirements that you restate that license.

Although it is common practice to include a complete copy of the
license in every single source file, this is awkward and not legally
necessary.

If you are importing openly licensed source code from another project
into your SO repository, please endeavor to respect the licensing
conditions of that code.  For example:

* Make sure that you are ready to accept the conditions of the
  license.  Some "Open Source" licenses, such as `GPL`_, have strict
  requirements on how derivative code can be distributed.
* If the imported code requires you to preserve the
  license/copyright/disclaimer, take care to do so.  It may be
  necessary to copy some license information into your project's
  LICENSE file, perhaps under a heading such as "This repository
  contains code by *developer*, which is distributed under the
  following license and conditions: ...".
* If you modify the imported code, make a clear note that you have
  done so, near the top of the source code file.

.. _`Open Source`: https://opensource.org/osd
.. _`MIT License`: https://opensource.org/licenses/MIT
.. _`BSD 2-Clause License`: https://opensource.org/licenses/BSD-2-Clause
.. _`GPL`: https://opensource.org/licenses/gpl-license

