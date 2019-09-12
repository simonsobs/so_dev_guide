==========================================
Special Guidance: Instrument Testing Group
==========================================

These instructions are specifically for readout, detector, and general
instrument component testing codes.

This is not meant to apply to pysmurf code.  It does not apply to OCS
code.  It does apply to data acquisition scripts written to drive
pysmurf in the OCS context.

It's not meant to apply to PWGs, BUT especially for instrument
characterization and calibration results, similar high levels of
provenance tracking will be observed by the relevant PWGs.


Overview
--------

Your test results need to be carefully recorded, which includes not
just the output products and plots but also the codes used to generate
them.  The codes provide documentation of the inputs and methods used
for the analysis and it is thus desirable to distribute them along
with the results.

Libraries vs. Ad-hoc scripting
------------------------------

Testing will necessarily involve the combination of standardized
functions with scripting code written to tie together a particular
analysis on a particular day.  Both the library-level code and the
ad-hoc connective tissue are part of documenting your analysis result.

In order to provide uniform results across various test beds, it is a
high priority to develop a small set of well-understood routines that
form the core of all testing analyses.  So it is not enough to "move
functions into a library /if/ they become widely used" -- rather, we
should "move functions into a library so that they become widely
used."

For example, there are many possible algorithms to measure resonator
properties, but we should quickly designate one of those approaches
for "reference" use and give it special status in a broadly
distributed library.

Even in cases where there are many possible approaches, and when a
second algorithm seems superior to the reference algorithm, comparison
to the reference algorithm can be provided.  The reference
implementation, even if it changes drastically at some point, provides
a coherent trunk from which other branches may emerge in an organized
fashion.


Recording Provenance of Test Results
------------------------------------

Tracked: Testing operations that provide key information for critical
decisions or inputs to downstream data analysis are called "Tracked"
and certain rules should be observed to properly record the provenance
of the results.

Examples of "Tracked" activities:

- Measurements of resonator Qs to make decisions about acceptance.
- Measurements of detector properties for the detector property
  database.

Examples of activities that probably do not need to be "Tracked":

- Sanity checks and preliminary analyses that are not part of quality
  control / acceptance.
- One-off follow-up analyses that are not shared broadly.


Provenance Tracking Code - Version Summarizer
---------------------------------------------

This should be used to collect software version codes and data tags,
and to write that information alongside analysis results.
Unfortunately it does not exist.

The things we want to track with this are:

- The version codes of the python modules loaded in the present
  analysis script.
- The provenance information of some inputs (such as TOD)::
  
  provenance = Provenance(output_file='prov.out')

  for filename in files:
      d = load_file(filename)
      provenance.add(d)

  provenance.finalize()


Data Acquisition
----------------


- ocs -> sodet -> pysmurf



Jupyter notebooks
-----------------

When writing code for yourself only, anything goes.  The advice below
should be consulted when you wish to use a Jupyter notebook to
communicate your analysis to other people.  Some ways to distribute
your notebook are:

- Post the ipnb file to the wiki / database server.
- Save the notebook and analysis to pdf and post the pdf.
- Commit the ipnb to a github repository and post the filename (and
  git commit hash or date).

Scripts generating ''Tracked'' results should be committed to the
relevant repository.

Your distributed notebooks or pdf output should:

- Contain only relevant code and discussion.
- These are great but don't let it get out of hand.
- Don't mix data acquisition and data analysis.
- Functions should be moved into the library level.

This is a really good discussion of how to write nice Jupyter
notebooks:
https://towardsdatascience.com/jupyter-notebook-best-practices-f430a6ba8c69 .
  
