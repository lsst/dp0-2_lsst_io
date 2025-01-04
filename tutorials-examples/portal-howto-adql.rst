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
.. _Tutorials-Examples-DP0-2-Portal-howto-adql:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

################################
03. How to execute an ADQL query
################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-03

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to execute a simple Portal query for table data using the `Astronomy Data Query Language (ADQL) <https://www.ivoa.net/documents/latest/ADQL.html>`_.

                                        
====================================
Option 1: Convert a UI query to ADQL
====================================
                                        
**1.1.** Navigate to the "DP0.2 Catalogs" tab in the Portal UI and set up a query in the user interface (UI), as shown in Figure 1.

.. figure:: /_static/portal-howto-adql-1.png
    :name: portal-howto-adql-1
    :alt: The Portal UI with a spatial query for bright, extended objects set up.

    Figure 1: The Portal UI set up for a simple cone search query for bright extended objects near the center of the DP0.2 region.


**1.2.** Click on the button labeled "Populate and edit ADQL", located bottom-center in Figure 1.
The UI will switch to the ADQL interface and will populate the ADQL Query box with an ADQL statement that represents the exact same query, as shown in Figure 2.

.. figure:: /_static/portal-howto-adql-2.png
    :name: portal-howto-adql-2
    :alt: The Portal UI with a spatial query for bright, extended objects converted from the UI to ADQL.

    Figure 2: The Portal's ADQL interface, automatically populated with the UI query from Figure 1, converted into an ADQL statement.


**1.3.** Click the Search button at lower left.
The query will be executed and the results will appear in the Results tab.

**Warning:** If changes are made to the ADQL statement and then the interface is toggled back to the "Single Table (UI assisted)" interface using the button at lower right in Figure 2,
those changes will not be reflected in the UI.
The conversion only works in one direction: from the UI to ADQL.


=================================
Option 2: Enter an ADQL statement
=================================

**2.1.** Navigate to the "DP0.2 Catalogs" tab in the Portal UI.

**2.2.** Reload the webpage in the browser to clear any previously-entered constraints.
The interface should look like Figure 3.

.. figure:: /_static/portal-howto-adql-3.png
    :name: portal-howto-adql-3
    :alt: The Portal UI with no constraints set.

    Figure 3: The Portal UI with no query constraints entered.


**2.3.** Select "Edit ADQL" at upper right in Figure 3.
The ADQL Query box will be empty; scroll down to see example queries or visit the :doc:`data-access-analysis-tools/adql-recipes.rst` page for examples.

.. figure:: /_static/portal-howto-adql-4.png
    :name: portal-howto-adql-4
    :alt: The ADQL interface with no query entered.

    Figure 4: The ADQL interface with no query entered.

**2.4.** Enter an ADQL statement in the box.
Copy paste the statement below.
It is the same query as was used above for Option 1.

.. code-block:: SQL

  SELECT coord_dec, coord_ra, detect_isPrimary, refExtendedness,
         g_ModelFlux, i_ModelFlux, r_ModelFlux, 
         u_cModelFlux, y_cModelFlux, z_cModeLFlux
  FROM dp02_dc2_catalogs.Object
  WHERE CONTAINS(POINT 'ICRS', coord_ra, coord_dec),
  CIRCLE(' ICRS', 62, -37, 0. 167) = 1
  AND (detect_isPrimary =1 AND refExtendedness =1
  AND g_ModelFlux >360 AND i_ModelFlux >360
  AND r_cModelFlux >360 AND u_ModelFlux >360
  AND y_cModelFlux >360 AND ≥_cModelFlux >360)


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
