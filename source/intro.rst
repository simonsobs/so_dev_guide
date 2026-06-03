===================================
Introduction to the Developer Guide
===================================

Welcome to Simons Observatory (SO) Developer Guide.

The purpose of this document is to establish the rules and guidelines for contributing
to SO's codebase across all repositories. It is intended to establish rules but also 
provide guidance and tips for helping SO produce high quality code with an effective 
workflow.

General best practices for coding, documentation and workflow are provided in the first
few chapters.  Afterwards, special policies relating to particular working groups are given.

As code is a live entity, this document is also live. We will update the document as
needed and as coding practices evolve over time. If you have any suggestions or corrections,
please submit a pull request or open an issue in the appropriate repository.


Why have a Developer's Guide and Style Guide?
==============================================

Code, especially open source code, is a collaborative effort. In addition, we all have
our own coding styles and preferences, and that's a good thing. Furthermore, software 
code is a product that is distributed to the public and hopefully will be used by many 
people outside of the collaboration. Incosistent code styles makes it harder for 
contributors and users to read, understand and reuse code. A developer and style 
guide aims to lower this friction.

A style guide removes trivial decision-making from code review.  When formatting and
naming are settled by convention, reviewers can focus on correctness, design, and
scientific validity. It also makes automated tooling—linters, formatters, documentation 
generators—easy to apply consistently across repositories.

A developer guide goes further: it captures the institutional knowledge that experienced
SO developers carry in their heads.  Which testing framework do we use?  How should a
new package be structured?  Writing these decisions down means a new collaborator can be 
productive in as little time as possble. 

The purpose of the guide is not to enforce uniformity just for the sake of uniformity.
Rather to reduce the time needed for new contributors to get up to speed, and reduce 
review times so that we produce better and faster science.
