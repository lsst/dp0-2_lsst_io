.. This is the beginning of a new tutorial focussing on learning to study variability using features of the Rubin Portal

.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-howto-nav:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

######################################
01. How to navigate the user interface
######################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-03

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to navigate the Portal's user interface (UI), and provides a tour of the its main components.

**1.** In a web browser, go to the URL `data.lsst.cloud <https://data.lsst.cloud/>`_.

.. figure:: /_static/portal-howto-nav-1.png
    :name: portal-howto-nav-1
    :alt: The main landing page of the Rubin Science Platform, showing log in at upper right and three panels, one for each aspect: the Portal the Notebooks and the API.

    Figure 1: The main landing page of the Rubin Science Platform.


**2.** At upper right, if "Log in" appears instead of your username, click "Log in" and follow the prompts to authenticate.

**3.** Click on the Portal square to enter the Portal Aspect.

.. figure:: /_static/portal-howto-nav-2.png
    :name: portal-howto-nav-2
    :alt: The main landing page of the Portal Aspect, showing tabs across the top and instructions in the middle.

    Figure 2: The main landing page of the Portal Aspect.


**4.** Notice the icons and tabs across the top of the screen, and that the default selected tab of the landing page is labeled Results.

**5.** Click on the menu icon (three horizontal lines at upper left) to open the sidebar menu.

.. figure:: /_static/portal-howto-nav-3.png
    :name: portal-howto-nav-3
    :alt: The sidebar menu of the Portal Aspect, showing options in addition to the tabs.
    :width: 300

    Figure 3: The sidebar menu of the Portal Aspect.


**6.** Notice that some of the menu options match the tabs (e.g., DP0.2 Catalogs), and that which tabs you see are configurable with the "Hide Tab" option.
Dismiss the sidebar menu by clicking on the X in the upper right corner of the menu.

**7.** Click on the Rubin logo next to the menu icon to see a pop-up window with Rubin Portal Version Information.
Dismiss the pop-up window by clicking on the OK button or on the X in its upper right corner.

**8.** Click on the tab labeled DP0.2 Catalogs.

.. figure:: /_static/portal-howto-nav-4.png
    :name: portal-howto-nav-4
    :alt: The graphical user interface for the Portal, offering drop-down menus to select catalogs and tables, entry fields for temporal and spatial constraints, and an interative view of the selected table schema.

    Figure 4: The Portal User Interface (UI) for querying the DP0.2 catalogs.

**9.** Use the mouse to hover-over the components of the UI and see pop-up explanations of the functionality.

**10.** Review the 8 main components of the UI, labeled A through H in Figure 4, that are used together to query (search) and retrieve data.

* A: Drop-down menu of the available DP0.2 catalogs.
* B: Drop-down menu of tables available for the selected catalog. The ``Object`` table is selected by default.
* C: Schema interface to put column constraints on, and choose rows to be returned from, the selected table.
* D: Entry fields for spatial constraints to be applied to the selected table.
* E: Entry field to set the maximum number of rows to return from the selected table.
* F: Button to convert the search constraints set with C, D, and E into an ADQL statement.
* G: Toggle to switch between this graphical UI and the alternative ADQL UI.
* H: Button to execute the query; to apply the search constraints and retrieve data into the results tab.

.. figure:: /_static/portal-howto-nav-5.png
    :name: portal-howto-nav-5
    :alt: The schema interface, showing how to select columns to include in the results, and how to place constraints on column values.

    Figure 5: The schema interface for the DP0.2 ``Object`` table, with three columns selected (``coord_ra``, ``coord_dec``, and ``g_ap03Flux``), and a constraint that ``g_ap03Flux`` be greater than 360 nJy (nanoJanskies).


**11.** Review the 8 components of the schema interface, labeled A through H in Figure 5, that are used to apply search constraints on the table data.

* A: Selection boxes. Click a box to include the column in the query. Click the funnel icon to view only selected columns.
* B: Names. Column names are short, descriptive, and unique within a table. Click on "Name" to sort by name.
* C: Constraints. Apply limits on column values by typing in desired constraints (e.g., :math:`>, <, =, !=`).
* D: Units. For DP0.2, it is a known issue that some columns are missing their units.
* E: Unified Content Descriptor (UCD). Vocabulary standards set by the `International Virtual Observatory Alliance <https://www.ivoa.net/>`_.
* F: Descriptions of the column's data.
* G: Data type. E.g., integer (int), double precision (double), boolean.
* H: Button to clear (reset) all column selections and constraints.

**12.** In the schema interface of Figure 5, notice that the columns are searchable.
Type a word, or use the drop-down menu, at the top of every column to find columns of interest.
For example, in the entry field under "Name" type "Flux" and click "enter" or "return" to see all column names with "Flux" in them.
Clear the entry field and click "enter" or "return" again to see all columns names (all rows of the schema interface).

Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
