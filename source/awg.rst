=========================================
Special Guidance: Analysis Working Groups
=========================================

General guidance
================

We recommend that Analysis Working Group (AWG) members write code that is open-source and publicly viewable.
We strongly encourage papers to be accompanied by public code releases to aid reproducibility.
Generally, Simons Observatory AWG codes do not *need* to be hosted
on the Simons Observatory github, and copyright ownership is up to the developers, but see the more specific and stringent requirements
for "core codes" outlined in the next section.

Requiring that users of your code cite certain papers may be incompatible with
open source licenses. However, you may *request* such citations without making it conditional on free usage of your
code. You may submit your code to `ASCL`_ or `JOSS`_ to allow it to be citeable.

Core codes
==========

Certain codes designated as "core codes" receive special consideration and extra scrutiny. The process of providing well-characterized maps to the AWGs and to the public requires quick iteration with the Pipeline Working Groups (PWGs). We anticipate several AWG codes to be critical components of this iteration pipeline and/or important for the process of releasing data, providing results for key papers and overview papers (e.g. power spectrum estimation, lensing estimation, null test pipeline scripts, cosmological likelihoods). We will not attempt to provide an exhaustive definition of core codes in this document; the designation will be made on a case-by-case basis by the Theory and Analysis Committee (TAC). Once a code is designated as a core code, the following restrictions will apply to it:

- the code repository must be hosted on the Simons Observatory Github organization
- the code should be openly contributed, with an open-source license
- the copyright should belong to "Members of the Simons Observatory Collaboration"
- approval should be sought from TAC before a private core code is made public
- the code will be periodically reviewed and inspected by TAC and/or Data Management (DM) to ensure it is well-documented, has good test coverage and can be run by multiple SO members

The general recommendation that codes be publicly viewable applies to core codes as well, though this is not a strict requirement. The TAC will maintain a wiki page that lists all AWG codes hosted on the Simons Observatory github with the core codes clearly designated.

Codes on SO Github
==================

If a code repository is hosted on the SO Github and is publicly visible, then it may be used by anyone (e.g. the public, ACT, Polarbear) without requiring explicit permission, unless the license somehow forbids this.

If a hosted code is private, then it is only visible to Simons Observatory members. Explicit permission must be requested from the developers of the code and TAC must be informed if SO members would like to use a private code in a non-SO project (e.g. a theory paper, ACT or Polarbear analysis).


.. _`ASCL`: https://ascl.net/
.. _`JOSS`: https://joss.theoj.org/
