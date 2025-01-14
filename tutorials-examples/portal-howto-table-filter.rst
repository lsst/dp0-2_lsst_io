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
.. _Tutorials-Examples-DP0-2-Portal-howto-table-filter:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

################################################
09.1. How to apply a filter to the results table
################################################

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


**3. Apply a filter.**
Filter the table such that only objects with Right Ascension coordinates :math:`<` 61.9 degrees are shown
by typing ``< 61.9`` into the filter entry box at the top of the ``coord_ra`` column as shown in Figure 2 (item A).
See how all panels update to show only the filtered objects.

.. figure:: /_static/portal-howto-table-4.png
    :name: portal-howto-table-4
    :alt: The full Results tab when rows have been filtered by the right ascension coordinate.

    Figure 2: The full Results tab after a filter for objects with ``RA`` :math:`<` 61.9 degrees is applied (item A).


**4. Remove the constraint.**
Click the "unfilter" icon at upper right in the table panel to remove the filter (B in Figure 2).


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.