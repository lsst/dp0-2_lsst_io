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

############################################
01. How to navigate the user interface (UI).
############################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-03

**Targeted learning level:** beginner 

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

**.8.** Click on the tab labeled DP0.2 Catalogs.

.. figure:: /_static/portal-howto-nav-4.png
    :name: portal-howto-nav-4
    :alt: The graphical user interface for the Portal, offering drop-down menus to select catalogs and tables, entry fields for temporal and spatial constraints, and an interative view of the selected table schema.

    Figure 4: The Portal User Interface (UI) for querying the DP0.2 catalogs.


**9.** Review the 8 main components of the UI, labeled A through H, that are used together to query (search) and retrieve data.

* A. Drop-down menu of the available DP0.2 catalogs.
* B. Drop-down menu of tables available for the selected catalog. The ``Object`` table is selected by default.
* C. Schema interface to put column constraints on, and choose rows to be returned from, the selected table.
* D. Entry fields for spatial constraints to be applied to the selected table.
* E. Entry field to set the maximum number of rows to return from the selected table.
* F. Button to convert the search constraints set with C, D, and E into an ADQL statement.
* G. The toggle to switch between this graphical UI and the alternative ADQL UI.
* H. A button to execute the query: to apply the search constraints and retrieve data.

**10.** Review the X components of the schema interface.
