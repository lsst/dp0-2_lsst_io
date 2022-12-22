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
(e.g., the `introduction to DP0.2 notebook <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/01_Introduction_to_DP02.ipynb>`_),
and clicking on "history" (near upper-right).

Portal tutorials
----------------

All Portal tutorials contain the date last verified to run near the top of their page.

All tutorials for the Portal aspect are kept in the `dp0-2_lsst_io repository <https://github.com/lsst/dp0-2_lsst_io>`_.
The full history for any given Portal tutorial can be accessed via GitHub by going to the Portal tutorial of interest
(e.g., the `beginner Portal tutorial <https://github.com/lsst/dp0-2_lsst_io/blob/main/tutorials-examples/portal-beginner.rst>`_), 
and clicking on "history" (near upper-right).


Major Updates Log
=================

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


Oct 4 2022
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
