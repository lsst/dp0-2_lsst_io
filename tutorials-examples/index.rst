.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Tutorials:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###############
DP0.2 Tutorials
###############

.. This section should provide a brief, top-level description of the page.

These tutorials are for DP0 delegates using the Rubin Science Platform (RSP) deployed at the Interim Data Facility (IDF; the Google Cloud).

Before following these tutorials, delegates should:

| 1. have gotten their :ref:`Delegate-Homepage-RSP-Accounts` and be able to log in at `data.lsst.cloud <https://data.lsst.cloud/>`_,
| 2. be familiar with this list of :doc:`/data-access-analysis-tools/rsp-warnings`,
| 3. reviewed the basic introductions to the RSP's :ref:`Tools-RSP-Portal` or :ref:`Tools-RSP-Notebook`, and
| 4. know their options for :ref:`Delegate-Homepage-Getting-Support`.


.. _DP0-2-Tutorials-Portal:

Portal tutorials
================

A beginner-level overview for the Portal Aspect is provided in this :doc:`/data-access-analysis-tools/portal-intro`.
More information can also be found in the `about firefly <https://data.lsst.cloud/portal/app/onlinehelp/>`_ page on the `Rubin Science Platform Documentation <https://data.lsst.cloud/docs>`_ page.

The tutorials below are step-by-step demonstrations of how to use the Portal Aspect for science investigations with the DP0 data set.


.. toctree::
    :titlesonly:
    :glob:

    portal-beginner
    portal-intermediate
    portal-images


.. _DP0-2-Tutorials-Notebooks:

Notebook tutorials
==================

A beginner-level overview for the Notebook Aspect is provided in this :doc:`/data-access-analysis-tools/nb-intro`.
More information can also be found in the `Notebook Aspect documentation <https://nb.lsst.io/>`_.

All Jupyter Notebook tutorials are kept in the `tutorial-notebooks repository <https://github.com/rubin-dp0/tutorial-notebooks>`_
of the ``rubin-dp0`` GitHub Organization.
That repository `README file <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/README.md>`_ contains descriptions of the tutorials.

The contents of that repository are made available (and automatically updated) in the folder ``notebooks/tutorial-notebooks`` 
which appears in all users' home directories. 

Delegates who are new to using Jupyter Notebooks may want to review :ref:`NB-Intro-Use-A-NB`, :ref:`NB-Intro-Use-Tutorial-NBs`,
the :ref:`NB-Intro-Use-A-NB-faq`, and :ref:`NB-Intro-Use-A-NB-tips` available in the :ref:`Data-Access-Analysis-Tools-NB-Intro`.

.. list-table:: Jupyter Notebook tutorials
   :header-rows: 1
   :widths: 1 2
   
   * - Jupyter Notebook
     - Brief Description
   * - 01. Introduction to DP0.2
     - Use the Jupyter Notebooks and Rubin python packages to access LSST data products.
   * - 02. Catalog Queries with TAP
     - Explore the DP0.2 catalogs via TAP and execute complex queries to retrieve data.
   * - 03a. Image Display and Manipulation
     - Learn how to display and manipulate images using the LSST Science Pipelines.
   * - 03b. Image Display with Firefly
     - Use the Firefly interactive interface for image data.
   * - 03c. Survey Property Maps
     - Use the tools to visualize full-area survey property maps.
   * - 04a. Introduction to the Butler
     - Use the Butler to query DP0 images and catalogs.
   * - 04b. Intermediate Butler Queries
     - Learn to discover data and apply query constraints with the Butler.
   * - 05. Introduction to Source Detection
     - Access, display, and manipulate images; detect, deblend, and measure sources; and extract, plot, and use object footprints.
   * - 06a. Interactive Image Visualization
     - Create interactive image visualizations with the HoloViews and Bokeh open-source python libraries.
   * - 06b. Interactive Catalog Visualization
     - Create interactive catalog visualizations for large datasets with HoloViews, Bokeh, and Datashader.
   * - 07a. DiaObject Samples
     - Use the DiaObject table parameters to identify a sample of time-variable objects of interest.
   * - 07b. Variable Star Lightcurves 
     - Use the DP0.2 catalogs to identify variable stars and plot their lightcurves.
   * - 08. Truth Tables
     - Explore, retrieve, and compare data from the truth and measurement tables.
   * - 09a. Custom Coadd
     - Create a custom "deepCoadd" using only a subset of the input visits.
   * - 09b. Custom Coadd Sources
     - Detect and measure sources in a custom coadded image.
