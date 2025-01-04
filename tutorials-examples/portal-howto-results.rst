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
.. _Tutorials-Examples-DP0-2-Portal-howto-results:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#############################
04. How to view query results
#############################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to view and interact with the results of a simple Portal query.

**1. Execute a query.**
Go to the Portal's DP0.2 Catalogs tab, switch to the ADQL interface, and execute the query below.

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

**2. Review the Results tab layout.**
The default layout of the Results tab is shown in Figure 1.

.. figure:: /_static/portal-howto-results-1.png
    :name: portal-howto-results-1
    :alt: The Results tab after a query has been executed defaults to a screens split three ways: coverage map at upper left, default plot at uppr right, and the tabular data below.

    Figure 1: The Results tab after a query has been executed defaults to a screens split three ways: coverage map at upper left, default plot at uppr right, and the tabular data below.

**3. Coverage map** (A in Figure 1).
The default view is a `HEALpix <https://healpix.sourceforge.io/>`_ grid showing the number of returned objects per grid region
and red squares marking individual objects outside the grid,
overplotted on a color `HiPS <https://aladin.cds.unistra.fr/hips/>`_ map of the DP0.2 deeply coadded images.

**4. Active chart** (B in Figure 1).
The default plot will be the first two columns of the returned data table.
In Figure 1, this is the Declination coordinate on the y-axis and the Right Ascension coordinate on the x-axis.
This plot will switch to a two-dimensional histogram if so many objects are returned that individual points cannot be distinguished.

**5. Table results** (C in Figure 1).

**X. Change the layout.**

**X. Viw multiple results.**

**X. To delete results** click on the X in the tab in the table.

