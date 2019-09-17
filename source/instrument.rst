===========================================
Special Guidance: Instrument Testing Groups
===========================================


Overview
========

Testing will necessarily involve the combination of standardized
functions with scripting code written to tie together a particular
analysis on a particular day.  Both the library-level code and the
ad-hoc connective tissue are critical components of the analysis.

The essence of this guidance is:

- We must put a high priority on establishing a core set of reference
  codes that will be used for performing various analyses in a
  consistent way across multiple testing and characterization centers.
- Record-keeping, verification, and reproducibility must be built into
  the ways that data are acquired, analyzed, and reported.


..  Your test and characterization results need to be carefully recorded,
..  and proper recording must include not only output plots and tables but
..  also the codes used to generate the essential results.  The codes
..  provide documentation of the inputs and methods used for the analysis,
..  and should be communicated in close association with the results.
..  
..  One key way to efficiently communicate the analysis technique is to
..  rely only on a small set of broadly accepted algorithms and scripts,
..  because that makes it possible to say "we use the usual library with
..  the usual options" and have many people then understand what was done.
..  It is thus a goal, in the Instrument Testing area, to focus efforts on
..  developing a single main trunk of codes to perform and report
..  instrument testing and characterization tasks.
..


Scope
=====

These instructions target readout, detector, and general instrument
component testing and characterization codes.

Many outputs from Instrument Testing and Characterization may end up
as inputs for Pipeline Working Groups creating mapping inputs or other
data characterization products.  Care to provenance tracking will also
be a focus of those groups, and will follow similar patterns.

This is not meant to apply to pysmurf code, as that is controlled by
SLAC.  It does not apply to OCS code and other instrument control
code, which falls into DAQ jurisdiction.  It `does` apply to data
acquisition scripts written to drive pysmurf through OCS.


Core Reference Codes
====================

**In order to provide uniform results across various test beds, it is
a high priority to develop a small set of well-understood routines
that form the core of all testing analyses.** So it is not enough to
"move functions into a library *if* they become widely used" --
rather, we should "move functions into a library *so that* they will
become widely used."

For example, there are many possible approaches to measuring resonator
properties, but we should quickly designate one of those algorithms
for "reference" use and give it special status in a broadly
distributed library.

Even in cases where there are many possible approaches, and when a
second algorithm seems superior to the reference algorithm, comparison
to the reference provides the necessary context for understanding such
superiority.  The reference implementation, even if it changes
drastically at some point, provides a coherent trunk from which other
branches may emerge in an organized fashion.


Provenance of Code and Data
===========================

"Provenance-Tracked" Results
------------------------------

Testing and characterization measurements and analyses that provide
key information for critical decisions or inputs to downstream data
analysis shall be designated as **"Provenance-Tracked"**, and certain
rules will be observed to properly record the provenance of the
results.

Examples of Provenance-Tracked activities:

- Measurements of resonator Qs to make decisions about acceptance.
- Measurements of detector properties for the detector property
  database.

Not all work in instrument characterization and testing will need to
be strictly tracked.  For example, the following are likely to be
exempt:

- Sanity checks of hardware function or component properties;
  preliminary analyses that are not part of quality control /
  acceptance.
- One-off follow-up analyses that are not shared broadly.

Recording Provenance
--------------------

For our purposes, full recording of the provenance of a test result
requires knowing:

- What versions of relevant library codes were used.
- What ad-hoc scripts were used.
- What data and meta-data files were used as inputs.

We will make such provenance recording possible through the following
mechanisms and policies:

- Libraries will carry version codes (see section on ``versioneer``),
  that will be reported with analysis results.  (Tools will be made
  available to assist with this reporting.)
- Ad-hoc scripts will be posted with the analysis results (i.e. on the
  same web page / wiki / database), or else committed to a github repo
  and the filename / commit hash recorded with the analysis result.
- Data and meta-data files will be given unique identifying paths and
  filenames.  The data being consumed should be unambiguously
  communicated, either in the ad-hoc script or in other information
  posted with the result.

Note that the above policies rule out some command analysis patterns,
and can lead to odd technical burdens:

- **Libraries with modifications** that have not been committed to SO
  github must not be used to generate tracked results.  In cases where
  a temporary change to a library is required to perform some
  analysis, there are a few options:

  1) Post the version of the library *and* the `git diff` showing
     local changes with the result.
  2) Create a github commit on a topic branch, and make that commit
     long-lived by merging it into a designated long-lived branch or
     by giving it a tag on the repository (consult your repo admin).

- When an analysis makes use of **command-line programs**, whose
  inputs and behavior are controlled to some degree through arguments
  passed from the shell, then the arguments used to run the program
  must be communicated along with the analysis result.
- Scripts that **glob filenames using wildcards** may need to more
  clearly communicate what data they have ended up using in a
  particular instance.  One solution to this is to record, as an
  output, the names of globbed files; the Version Summarizer described
  below may be able to help with that.
- Scripts that **acquire and analyze data in one go** are problematic,
  unless all data and meta-data are saved for posterity *and* the
  analysis approach can be extracted for re-application to data in
  situ.
- **Jupyter notebooks** can be very convenient for presenting a
  sequence of analysis operations.  Certain practices should be
  observed when using a Jupyter notebook as part of provenance; see
  below.


Tool: Version Summarizer
------------------------

This should be used to collect software version codes and data tags,
and to write that information alongside analysis results.
Unfortunately it does not exist yet.

The things we want to track with this are:

- The version codes of the python modules loaded in the present
  analysis script.
- The provenance information of some inputs (such as TOD).

We would ultimately like to support this kind of thing::
  
  # Create tracking object.
  provenance = Provenance(output_file='prov.out')

  for filename in files:
      dat = load_file(filename)
      provenance.add(filename=filename)  # register a file
                                         #  using a filename
      # ...do some stuff with dat...

  bias_line_map = BiasLineMap.get_latest('tube_28')
  provenance.add(bias_line_map)   # register an object that
                                  # supports the Provenance
                                  # interface (it can report
                                  # its own metadata)

  # ... do some stuff with bias_line_map or whatever ...

  # Call finalize() to write the results to prov.out. Will include
  # version tags of all loaded python modules.
  provenance.finalize()


Guidance: Jupyter notebooks
---------------------------

When writing code for yourself only, anything goes.  The advice below
should be consulted when you wish to use a Jupyter notebook to
communicate your analysis to other people.  Some ways to distribute
your notebook are:

- Post the ipynb file to the wiki / database server.
- Save the notebook and analysis to pdf and post the pdf.
- Commit the ipynb to a github repository and post the filename (and
  git commit hash or date).

Scripts generating Provenance-Tracked results should be committed to
the relevant repository.

When using notebooks as part of provenance, they can be communicated
in a few different ways:

- If you want to show the analysis calls along with plots and output
  generated by the script, then convert your output to PDF and post
  that to the web page / wiki / database with your result.
- If your notebook has utility going forward, then it can be committed
  to a a github repo.  However, it's usually a good idea in such cases
  to strip out all of the output and plots; there are tools available
  to help do this automatically.  The github path and commit hash
  should be posted to the analysis result page.

The Jupyter notebook interface allows the presented code to be run
out-of-order, modified after running, and so on.  Make sure that any
notebooks you distribute:

- Contain only relevant code and discussion.
- Are complete (do not contain hidden imports or analysis blocks).
- Are accurate in the presentation of the sequence of calculations and
  their results.

This is a nice discussion of how to write good Jupyter notebooks:
https://towardsdatascience.com/jupyter-notebook-best-practices-f430a6ba8c69
.  It includes links to other interesting discussions on the topic.
  
