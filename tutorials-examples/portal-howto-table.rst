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
.. _Tutorials-Examples-DP0-2-Portal-howto-table:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

################################
09. How to use the results table
################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to use the table panel in the Portal results tab.

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


**3. Mouse-over for pop-up notes.**
In the table panel (Figure 1) use the mouse to hover over the column headers and icons see pop-up explanations.

**4. Explore menus and icons.**
In the table panel (Figure 1) click on each of the items below and review the functionality.

* C: **Navigate** the pages of the table or jump to a page.
* D: **Actions** - generate new TAP searches (advanced, not covered in this tutorial).
* E: **Filter** - show or hide the header row for table filter entries.
* F: **Text view** - switch the table view to text mode.
* G: **Save** file (download table); a variety of formats are offered.
* H: **Add a column** that is derived from existing columns.
* I: **Information** about the query job that produced these results.
* J: **Table options** - open a pop-up window to show, hide, or filter columns.
* K: **Expand panel** - have the table take the full browser window.


**5. Sort the table.**
Click on the table header ``coord_ra`` to sort the table by the Right Ascension coordinate.
Any column can be sorted in this way.

**6. Select rows.**
Click on the boxes at left (B in Figure 1) for the first 10 rows.
Notice how these objects are colored differently in the coverage and active chart, as in Figure 2.

.. figure:: /_static/portal-howto-table-2.png
    :name: portal-howto-table-2
    :alt: The full Results tab when 10 rows have been selected.

    Figure 2: The full Results tab after 10 rows have been selected in the table panel.


**7. Filter on the selected rows.**
Click the filter icon (under B in Figure 1).
See how all panels update to show only the selected objects, as in Figure 3.

.. figure:: /_static/portal-howto-table-3.png
    :name: portal-howto-table-3
    :alt: The full Results tab when 10 rows have been selected and filtered on.

    Figure 3: The full Results tab after 10 rows have been selected in the table panel, and filtered on.


**8. Remove the filter and selection.**
Click the "unfilter" icon at upper right in the table panel to remove the filter (A in Figure 3).
Click the "unselect" icon at uppr right in the active chart panel to unselect all objects (B in Figure 3).

Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
