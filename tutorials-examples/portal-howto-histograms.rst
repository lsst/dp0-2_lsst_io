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

###################################################################
08.2. How to plot one- and two-dimensional histograms in the Portal
###################################################################


.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** beginner

**Introduction:**
This tutorial demonstrates how to create one- and two-dimensional ("heatmap") histograms of quantities (g- and r-magnitudes) retrieved from object or source catalogs.

.. =====================

.. The Portal aspect of the Rubin Science Platform lends itself well to retrieve apparent magnitudes of (for instance) extended objects in a region of the sky.
.. It provides convenient and easy to use tools to plot 1- and 2-dimensional histograms to explore their apparent magnitude and color distributions.

.. For the retrieval of the required data, this "How to" uses the Astronomy Data Query Language (ADQL), which is similar to SQL (Structured Query Language).
.. The option to use the ADQL in the Portal aspect of the Rubin Science Platform is selected by clicking on "Edit ADQL" in the upper right-hand side of the Portal landing page.

.. For more information about the DP0.2 catalogs, tables, and columns, visit the DP0.2 Data Products Definition Document (DPDD)
.. :ref:`DP0-2-Data-Products-DPDD` or the `DP0.2 Catalog Schema Browser <https://sdm-schemas.lsst.io/dp02.html>`_.

.. _DP0-2-Portal-Histogram-Step-1:

**1.  Prepare to execute the ADQL query to retrieve data.**
Navigate to the Portal's DP0.2 Catalogs tab and switch to the ADQL interface by selecting  "Edit ADQL" at upper right.
If needed, reload the webpage in the browser to clear any previously-entered constraints.

**2. Enter an ADQL statement in the box.**
For example, copy and paste the statement below, which converts the fluxes to magnitudes, by the use of an ADQL function ``scisql_nanojanskyToAbMag()`` where the respective flux is the argument (and renames them as ``g_cModelMag`` and ``r_cModelMag``).
It limits the search to the extended objects with ``g`` and ``r`` cModel fluxes greater than 360 nJy (cModel magnitudes less than 25), located in a circular region with a radius of 10 arc min (0.167 degree), around the direction with RA of 62.0 deg and and Dec of -37.0 deg.

.. code-block:: SQL

   SELECT coord_dec, coord_ra, 
   scisql_nanojanskyToAbMag(g_cModelFlux) AS g_cModelMag, 
   scisql_nanojanskyToAbMag(r_cModelFlux) AS r_cModelMag, 
   g_extendedness, 
   r_extendedness 
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), 
   CIRCLE('ICRS', 62, -37, 0.167)) =1 
   AND g_extendedness = 1 
   AND r_extendedness = 1 
   AND g_cModelFlux > 360 
   AND r_cModelFlux > 360 

**3.  Extract the required magnitudes.**
Execute the ADQL query by clicking the “Search” button in the lower left corner.
The resulting display will by default show the sky coverage on the left, and the plot of the 1st column as a function of the 2nd column on the right.

**4.  Plot the distribution of g magnitudes.**
To do so, add another plot panel, by clicking on the "+" button on the upper left-hand side of the active chart, and select "Histogram" as the Plot Type.
In the resulting  pop-up window, in the "Column or expression" box, enter ``g_cModelMag`` and click "OK" which will result in displaying an additional plot window, with g magnitude histogram.

**5.  Remove the "coord_ra vs. coord_dec" plot** by clicking on the "x" in the upper right-hand side of the plot window, which will result in the display as below.

.. figure:: /_static/Howto_Histogram_1d.png
	:name: Howto_Histogram_1d.png
	:alt: Screenshot of the 1-d histogram of g-magnitudes in the selectred region, obtained by executing an ADQL query.

Figure 1:  screenshot of the 1-d histogram of g-magnitudes of extended objects in the selected region, obtained by executing an ADQL query.

.. _DP0-2-Portal-Histogram-Step-2:

**6.  Plot the 2-d histogram (heatmap) of the g-r colors vs. g cModel magnitudes.**
Add an additional plot panel by clicking on the "+" button on the upper left-hand side of the active chart, and in the resulting pop-up window, click on "Heatmap" as the plot type.
Plot the heatmap of g-r color vs. g-magnitude by entering ``g_cModelMag`` for X, and ``g_cModelMag-r_cModelMag`` for Y.

.. figure:: /_static/Howto_Histogram_2d.png
	:name: Howto_Histogram_2d.png
	:alt: Screenshot of the 2-d histogram of g-r color vs. g-magnitudes in the selected region, obtained by executing an ADQL query.

Figure 2:  The 1-d histogram of g-magnitudes as well as the 2-d histogram of g-r color vs. g-magnitudes of the extended objects in the selected region, obtained by executing an ADQL query.
