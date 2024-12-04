.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-Portal-Intro:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#####################################
How to navigate the RSP Portal Aspect
#####################################

.. This section should provide a brief, top-level description of the page.

.. Current version:  September 1 2024

**1.  Logging in**:  The Portal Aspect of the Rubin Science Platform (RSP) can be accessed by clicking on the "Portal" panel of the main landing page at `data.lsst.cloud <https://data.lsst.cloud>`_.

The Rubin Science Platform Portal Aspect has a variety of search functions.
Those can currently access the simulated Rubin data, namely DP0.2 Images, DP0.2 Catalogs, and DP0.3 (Solar System only) Catalogs.
In the future, the RSP will be able to access the real (rather than simulated) Rubin data.

**2.  Selecting the repository**:  Logging in to the Rubin Science Platform and selecting "Portal aspect" will reveal the multiple tabs on top.
Those correspond to image / catalog repositories which can be accessed by clicking on the respective tab.

**3.  Selecting the search tool**:  Within each tab, there are multiple types of queries that can be performed.
Within those three choices above, there is the ability to use "User Interface (UI) assisted" searching (default, amounting to single-table queries) or execute the search using the Astronomical Data Query Language (ADQL) queries.
It is possible to toggle between the two by clicking on the button to the right of "View:".
Each of these options has a different user interface, covered in other "How to" documents.

**4.  Results**:  The leftmost tab marked as "Results" will contain the result of the most recently executed query.
Execution of the several queries will result in the appearance of separate sub-tabs in the "Results" tab.
The rightmost tab allows you to upload your own images or tables, but its use is more advanced, beyond the simple "How-to" guide.

.. figure:: /_static/portal_intro_DP02a.png
    :name: portal_default_view_DP02
    :alt: Screenshot of the default view of the rubin science platform portal interface for single table queries. From this window the user can select the type of search, tables to search, 
    	select various constraints, and can select the number of rows to return.

    **The default view of the Portal's user interface for UI assisted queries.**

.. :ref:`Portal-Intro-Image-Queries` from the "DP0.2 Images" tab, :ref:`Portal-Intro-Single-Table-Queries` and :ref:`Portal-Intro-ADQL-Queries`, from the DP0.2 Catalogs tab. 


