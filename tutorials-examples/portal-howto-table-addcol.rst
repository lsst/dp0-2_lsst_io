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
.. _Tutorials-Examples-DP0-2-Portal-howto-table-addcol:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

##############################################
09.2. How to add a column to the results table
##############################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to manipulate the table panel, apply constraints, and add derived columns in the Portal results tab.

**1. Execute a query.**
Go to the Portal's DP0.2 Catalogs tab, switch to the ADQL interface, and execute the query below.
This query will retrieve a small sample of point-like objects (stars) brighter than 25th magnitude (as in preceding tutorials).

.. code-block:: SQL

  SELECT coord_dec, coord_ra, detect_isPrimary, refExtendedness, 
         u_cModelFlux, g_cModelFlux, r_cModelFlux, 
         i_cModelFlux, z_cModelFlux, y_cModelFlux 
  FROM dp02_dc2_catalogs.Object 
  WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), 
        CIRCLE('ICRS', 62, -37, 0.167)) =1 
        AND (detect_isPrimary =1 AND refExtendedness =1 
             AND u_cModelFlux >360 AND g_cModelFlux >360 
             AND r_cModelFlux >360 AND i_cModelFlux >360 
             AND z_cModelFlux >360 AND y_cModelFlux >360)


**2. View the default table** (Figure 1).
Only one query has been executed, so there is only one tab in the table panel (A in Figure 1).

.. figure:: /_static/portal-howto-table-1.png
    :name: portal-howto-table-1
    :alt: The default view of the table panel.

    Figure 1: The table panel that results from the query in step 1. The third row has been clicked on and is highlighted orange.


**3. Open the "Add a column" window.**
Click on the "add column" icon (H in Figure 1) to open the pop-up window in Figure 2.

.. figure:: /_static/portal-howto-table-5.png
    :name: portal-howto-table-5
    :alt: The pop-up window to add a new column, with entry field boxes to define the derived column.

    Figure 2: The pop-up window to add a new column, with entry field boxes set to define a new derived column of g-band AB magnitudes.


**4. Define the new column.**
New columns can only be derived from pre-existing columns using an expression.
In the pop-up window, name the new column ``g_cModelMag``.
Use the following expression, which converts fluxes (in units of nJy) into AB magnitudes: ``-2.5 * LOG10(g_cModelFlux) + 31.4``.
Provide the units of the new column as ``mag``, and add a description.
Click "Add Column", and it will appear in the table.

**5. Option to save the table.**
Click on the save icon (G in Figure 1), choose a file format of comma-separated values (CSV) and name the file as "my_table.csv".
Leave the default selection of "Save table as displayed" in order to include the new derived column of g-band magnitudes, and click "Save" to download the file.


.. figure:: /_static/portal-howto-table-6.png
    :name: portal-howto-table-6
    :alt: The pop-up window to save a table.

    Figure 2: The pop-up window to save a table, with the selections as described in step 5.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
