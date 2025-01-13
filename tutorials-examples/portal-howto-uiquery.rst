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
.. _Tutorials-Examples-DP0-2-Portal-howto-uiquery:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#############################
02. How to execute a UI query
#############################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-03

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to execute a simple query for table data with the Portal's user interface (UI).


**1. Go to the Portal's DP0.2 Catalogs tab.** The screen should look like Figure 1.

.. figure:: /_static/portal-howto-uiquery-1.png
    :name: portal-howto-uiquery-1
    :alt: The graphical user interface for the Portal, offering drop-down menus to select catalogs and tables, entry fields for temporal and spatial constraints, and an interative view of the selected table schema.

    Figure 1: The Portal User Interface (UI) for querying the DP0.2 catalogs.


**2. Select collection and table.**
Set the collection to ``dp02_dc2_catalogs`` (A in Figure 1) and the table to ``Object`` (B in Figure 1).
These are the defaults of a new Portal session and might be pre-selected.

**3. Set spatial constraints** (C in Figure 1).
Select shape type "cone shape", set the coordinates to 62, -37 (near the center of the DP0.2 simulation),
and set the radius to 10 arcminutes (as in Figure 2).

.. figure:: /_static/portal-howto-uiquery-2.png
    :name: portal-howto-uiquery-2
    :alt: Spatial constraints applied in the Portal UI.

    Figure 2: Spatial constraints for a cone search centered on Right Ascension 62 degrees, Declination -37 degrees, and with a radius of 10 arcminutes.


**4. Select columns to return.** 
In the schema interface (D in Figure 1), select all of the columns listed below.
Use the table search functionality, such as ``like '%_cModelFlux'`` as shown in Figure 3, to find the columns.

* ``coord_ra``
* ``coord_dec``
* ``detect_isPrimary``
* ``refExtendedness``
* ``u_cModelFlux``
* ``g_cModelFlux``
* ``r_cModelFlux``
* ``i_cModelFlux``
* ``z_cModelFlux``
* ``y_cModelFlux``

.. figure:: /_static/portal-howto-uiquery-3.png
    :name: portal-howto-uiquery-3
    :alt: Selecting columns from the schema interface.

    Figure 3: The schema interface, with a search for column names containin the string ``cModelFlux``, and six columns selected.


**5. Set column constraints.**
In the schema interface (D in Figure 1), click on the funnel icon to show only selected columns.
Set the constraints in the list below, as shown in Figure 4.

* ``detect_isPrimary`` :math:`= 1` to return deblended objects and reject duplicates.
* ``refExtendedness`` :math:`= 1` to return objects that appear extended (likely galaxies, not stars).
* All ``cModelFlux`` :math:`> 360` nJy to return objects brighter than 25th mag. (Recall that :math:`m = -2.5 log(f) + 31.4`, where :math:`f` is in units of nJy).

.. figure:: /_static/portal-howto-uiquery-4.png
    :name: portal-howto-uiquery-4
    :alt: Applying column constraints in the schema interface.

    Figure 4: The schema interface, with all desired columns selected and all column constraints applied. The funnel icon has been clicked so that only selected columns are shown.


**Warning!**
Do not use the schema interface to apply spatial constraints, i.e., do not apply limits on coordinate columns (``coord_ra``, ``coord_dec``).
Only apply spatial constraints as instructed in Step 3, because cone and polygon searches are executed much more quickly than columns limits.

**6. Execute the UI query.**
Leave the Row Limit (E in Figure 1) at the default of 50,000 and click Search (F in Figure 1).
The query will be executed and the results will appear in the Results tab.

.. figure:: /_static/portal-howto-uiquery-5.png
    :name: portal-howto-uiquery-5
    :alt: Default search results from a query.

    Figure 4: The default results view layout for the query described above. Interacting with query results is covered in a separate tutorial.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
