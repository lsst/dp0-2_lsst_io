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
.. _Tutorials-Examples-DP0-2-Portal-howto-query-image:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#################################
10. How to execute an Image query
#################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Yumi Choi

**Last verified to run:** 2025-02-11

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to execute a simple Portal query for image data using the `ObsTAP <https://www.ivoa.net/documents/ObsCore/>`_.

                                           
**1. Go to the Portal’s DP0.2 Images tab.**
Navigate to the "DP0.2 Images" tab in the Portal aspect.

.. figure:: /_static/portal-howto-query-image-1.png
    :name: portal-howto-query-image-1
    :alt: The Portal DP0.2 image search set up.

    Figure 1: The Portal image search set up for a simple location search query for the processed visit images (PVIs; the calibrated single-epoch images also called calexps).


**2. Enter constraints** (A in Figure 1).
Impose a variety of constraints on the image query. 


**2.1. Set observation type and source** (B in Figure 1).
To specify a specific data product, check the Observation Type and Source box.
Under “Observation Type and Source”, the IVOA standard options for “Calibration Level” (0, 1, 2, 3, or 4) are provided. For DP0.2, “1” is the raw (unprocessed) images, “2” is the processed visit images (PVIs; the calibrated single-epoch images also called calexps), and “3” are the derived image data such as difference images and deep coadds.

The “Data Product Type” should be left as “Image”, and the “Instrument Name”, “Collection”, and “Data Product Subtype” can all be left blank.

**Warning!**
If changes are made to the ADQL statement and then the interface is toggled back to the "Single Table (UI assisted)" interface using the button at lower right in Figure 2,
those changes will not be reflected in the UI.
The conversion only works in one direction: from the UI to ADQL.


=================================
Option 2: Enter an ADQL statement
=================================

**2.1. Go to the Portal's DP0.2 Catalogs tab.**
If needed, reload the webpage in the browser to clear any previously-entered constraints.
The interface should look like Figure 3.

.. figure:: /_static/portal-howto-adql-3.png
    :name: portal-howto-adql-3
    :alt: The Portal UI with no constraints set.

    Figure 3: The Portal UI with no query constraints entered.


**2.2. Switch to the ADQL interface.** 
Select "Edit ADQL" at upper right in Figure 3 to go to the ADQL interface.
The ADQL Query box will be empty (Figure 4).
Scroll down to see example queries and visit the :doc:`/data-access-analysis-tools/adql-recipes` page for more.

.. figure:: /_static/portal-howto-adql-4.png
    :name: portal-howto-adql-4
    :alt: The ADQL interface with no query entered.

    Figure 4: The ADQL interface with no query entered.


**2.3. Enter an ADQL statement in the box.**
For example, copy paste the statement below.
It is the same query as was used above in Option 1.

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


**2.4. Execute the ADQL query.**
Click the Search button at lower left.
The query will be executed and the results will appear in the Results tab.


.. figure:: /_static/portal-howto-uiquery-5.png
    :name: portal-howto-uiquery-5
    :alt: Default search results from a query.

    Figure 5: The default results view layout for the query described above. Interacting with query results is covered in a separate tutorial.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
