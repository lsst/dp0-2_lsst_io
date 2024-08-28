.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
    - If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Major-Updates-Log:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#############################
Log of Major Tutorial Updates
#############################

How to find version histories
=============================

Notebook tutorials
------------------

All Jupyter Notebook tutorial headers contain the date "last verified to run".
If the date in the file you are using does not match the date shown in that file in `the "prod" branch of the tutorial-notebooks repository <https://github.com/rubin-dp0/tutorial-notebooks/tree/prod>`_, your version is out of date.
Follow the instructions for what to do if notebooks do not automatically update in the :ref:`NB-Intro-Use-A-NB-tips`. 

A full history for all tutorial notebooks can be accessed in GitHub via this `direct link to the commit log for the
tutorial-notebooks repository <https://github.com/rubin-dp0/tutorial-notebooks/commits/main>`_.

The full history for any given tutorial notebook can be accessed via GitHub by going to the notebook of interest
(e.g., the `introduction to DP0.2 notebook <https://github.com/rubin-dp0/tutorial-notebooks>`_),
and clicking on "history" (near upper-right).

Portal, command line, and API tutorials
---------------------------------------

All Portal, command line, and API tutorials contain the date last verified to run near the top of their page.

All tutorials for the Portal aspect, for the command line (Notebook Aspect), and for the API aspect 
are kept in the `dp0-2_lsst_io repository <https://github.com/lsst/dp0-2_lsst_io>`_.

The full history for any given tutorial can be accessed via GitHub by going to the tutorial of interest
(e.g., the `beginner Portal tutorial <https://github.com/lsst/dp0-2_lsst_io/blob/main/tutorials-examples/portal-beginner.rst>`_), 
and clicking on "history" (near upper-right).


Major Updates Log
=================

Aug 22 2024
-----------

The recommended image of the RSP at data.lsst.cloud was bumped to Weekly 2024_32.

Tutorial notebook 14 (synthetic source injection) was updated to work without writing the synthetic source catalog to the butler.

Aug 13 2024
-----------

Released command line tutorial 02, demonstrating butler command line usage.
The custom coadd command line tutorial is now labeled as command line tutorial 03.

Jul 29 2024
-----------

Split tutorial notebook 02 into 02a and 02b, to provide a more detailed introduction to the TAP service for catalog data.

Released new tutorial notebook 02c, an introduction to the ObsTAP service and image queries for metadata and pixel data.

Jun 13 2024
-----------

Released tutorial notebook 03c, which demonstrates how to create a big cutout image which spans patch and tract boundaries.

Jun 3 2024
----------

Tutorial notebook 05, Source Detection and Measurement, has been updated to include a demonstration of forced photometry.

May 2 2024
----------

The recommended image of the RSP at data.lsst.cloud was bumped to Weekly 2024_16.

Apr 30 2024
-----------

Released three introductory-level :ref:`DP0-2-Tutorials-ES`. 

Mar 27 2024
-----------

Released tutorial notebook 13a on the image cutout tool.

Feb 29 2024
-----------

Released tutorial notebook 14 on synthetic source injection.

Feb 1 2024
----------

The recommended image of the RSP at data.lsst.cloud was bumped to Weekly 2024_04.

Dec 6 2023
----------

Released new API tutorial 01 (TOPCAT).

Nov 30 2023
-----------

The recommended image of the RSP at data.lsst.cloud was bumped to Weekly 2023_47.

Sep 21 2023
-----------

The recommended image of the RSP at data.lsst.cloud was bumped to Weekly 2023_37.

New tutorial notebooks 12a and 12b on the Point Spread Function data products and their analysis were released.

Jul 31 2023
-----------

Released new tutorial notebook 11 on working with user packages.

Jun 1 2023
----------

The recommended image of the RSP at data.lsst.cloud was bumped to Weekly 2023_21.

In notebooks 02 and 06b, deprecated Bokeh keyword arguments "plot_height" and "plot_width" were replaced with "height" and "width". The same two notebooks were updated to cast the objectId to a string, because Bokeh was not able to handle such large integers.

An update that was required in many notebooks was replacing "get_tap_service()" with "get_tap_service("tap")" (due to deprecation of the former syntax).

Finally, calls to the deprecated method "butler.getDirect()" were replaced with "butler.get()" in a few places.

May 24 2023
-----------

Released Portal tutorials 04 and 05.

May 15 2023
-----------

Added command line version of Notebook 09a, with a warning that it must be run with uncached RSP image Weekly 2022_40.

Apr 12 2023
-----------

Notebooks 09a and 09b have been reinstated, with a warning that they must be run with uncached RSP image Weekly 2022_40.

Mar 07 2023
-----------

Notebook 10 on deblender data products created and released.

Notebook 07b has been updated to use the ``ForcedSourceOnDiaObjects`` table.

Feb 16 2023
-----------

The recommended image of the RSP at data.lsst.cloud was bumped to Weekly 2023_07.

Notebooks 09a and 09b have been temporarily removed from the tutorial-notebooks repository and
are undergoing major redevelopment to start the reprocessing for custom coadds at earlier stages of the pipeline.

Notebook 04b, Section 3.3.1 has been updated to show a plot of the bounding boxes of patches which overlap with a calexp.

Notebook 06a, Section 2.1 has been updated to use ``calexp.visitInfo.id`` and ``calexp.filter.bandLabel``.

Many notebooks have had minor updates to use ``SELECT TOP`` instead of ``MAXREC`` (the latter produces an unavoidable but non-fatal warning)
and/or remove the use of the ``%%time`` magic as all code cells now have an execution time display built-in.

Feb 06 2023
-----------

Command line tutorial 01 created and released.

Jan 05 2023
-----------

Portal Tutorial 01 updated with a new Section 4, illustrating how to copy the URL containing query results for use in a notebook.  

Dec 21 2022
-----------

Notebooks 06a and 06b (data visualization) added instructions for how to output interactive plots to interactive HTML files that can be downloaded, shared, and opened outside of the JupyterLab environment.

Dec 16 2022
-----------

Notebook 03a (image display) added cutout funtion for calexps (previously only had one for deepCoadds)

Notebook 08 (truth tables) added new Section 3.3 to demonstrate an efficient single-Object search

Use of warning suppression has been modified in many notebooks to align with `RTN-045 <https://rtn-045.lsst.io/>`__.

:doc:`/data-access-analysis-tools/adql-recipes` and :doc:`/data-access-analysis-tools/python-functions` have been added to the DP0.2 documentation.
They include copy-pastable functions and query recipes for users.

Oct 26 2022
-----------

Notebook 03a (image display) updated to replace use of ``objectTable`` via the butler with a TAP query.

Notebook 07a (DiaObject samples) updated to use the recently released ``ForcedSourceOnDiaObject`` table.

Notebooks 09a and 09b (custom coadds) added.


Oct 04 2022
----------

Notebook 08 (truth tables) updated to optimize TAP query.


Sep 29 2022
-----------

Notebook 08 (truth tables) added.

The ``ForcedSourceOnDiaObject``, ``TruthSummary``, and ``MatchesTruth`` tables were released.

The recommended image of the RSP was bumped to version Weekly 40, and all notebooks were updated accordingly.

Permissions for users' "notebooks/tutorial-notebooks" directory changed to read-only.
For details about the permission change, see :ref:`NB-Intro-Use-Tutorial-NBs` and :ref:`NB-Intro-Use-A-NB-faq-readonly`.

| Relevant announcements in the Forum:
|  - `Truth-Match and ForcedSourceOnDiaObject tables are available <https://community.lsst.org/t/7088>`_ 
|  - `Permission changes for users’ “notebooks/tutorial-notebooks” directory <https://community.lsst.org/t/7087>`_


Aug 20 2022
-----------

Notebooks 03c (survey property maps) and 04b (intermediate butler queries) added.


June 27 2022
------------

All tutorials updated for the release of DP0.2.

