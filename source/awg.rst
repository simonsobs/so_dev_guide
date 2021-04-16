=========================================
Special Guidance: Analysis Working Groups
=========================================

.. warning:: The policies described in this chapter need to be
             approved at a high level (including by the Publication Panel and the Planning Committee).
	     Until that happens, do not take
             any drastic actions based on the text below!


General guidance
================

We recommend that Analysis Working Group (AWG) members write code that is Open Source and publicly viewable.
We strongly encourage papers to be accompanied by public code releases to aid reproducibility.
Generally, Simons Observatory AWG codes do not *need* to be hosted
on the Simons Observatory Github, and copyright ownership is up to the developers, but see the more specific and stringent requirements
for "Core Codes" outlined in the next section.

Requiring that users of your code cite certain papers may be incompatible with
Open Source licenses. However, you may *request* such citations (e.g. in the README file) without making it conditional on free usage of your
code. You may submit your code to `ASCL`_ or `JOSS`_ to allow it to be citeable.

Core Codes
==========

Certain codes designated as "Core Codes" receive special consideration and extra scrutiny. The process of providing well-characterized maps to the AWGs and to the public requires quick iteration with the Pipeline Working Groups (PWGs). We anticipate several AWG codes to be critical components of this iteration pipeline and/or important for the process of releasing data, providing results for key papers and overview papers (e.g. power spectrum estimation, lensing estimation, null test pipeline scripts, cosmological likelihoods). We will not attempt to provide an exhaustive definition of Core Codes in this document; the designation will be made on a case-by-case basis by the Theory and Analysis Committee (TAC). Once a code is designated as a Core Code, the following restrictions will apply to it:

- the code must meet the requirements of Openly Contributed code as defined in Chapter 2 (this includes that it must be hosted on the Simons Observatory Github organization, have an Open Source license and the list of Copyright owners should be truncated to a simple and broad summary such as "Members of the Simons Observatory Collaboration" to facilitate further expansion)
- approval should be sought from TAC before a private Core Code is made public
- the code will be periodically reviewed and inspected by TAC and/or Data Management (DM) to ensure it is well-documented, has good test coverage and can be run by multiple SO members

The general recommendation that codes be publicly visible applies to Core Codes, though public visibility is not a strict requirement. The TAC will maintain a wiki page that lists all AWG codes hosted on the Simons Observatory Github with the Core Codes clearly designated.

Codes on SO Github
==================

If a code repository is hosted on the SO Github and is publicly visible, then it may be used by anyone (e.g. the public, ACT, Polarbear, other SO members) without requiring explicit permission, if the license allows this. The licenses that we recommend (`BSD 2-Clause License`_ or `MIT License`_) do allow this.

If a hosted code is private, then it is only visible to Simons Observatory Github members. Explicit permission must be requested from the developers of the code and TAC must be informed if SO members would like to use a private code in a non-SO project (e.g. a theory paper, ACT or Polarbear analysis), even if the license states otherwise.


.. _`ASCL`: https://ascl.net/
.. _`JOSS`: https://joss.theoj.org/
.. _`MIT License`: https://opensource.org/licenses/MIT
.. _`BSD 2-Clause License`: https://opensource.org/licenses/BSD-2-Clause
