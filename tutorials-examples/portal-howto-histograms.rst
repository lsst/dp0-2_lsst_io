.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-howto-histograms:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#########################################
08.2. How to plot histograms and heatmaps
#########################################


.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-03-04

**Targeted learning level:** intermediate

**Introduction:**
This tutorial demonstrates how to create one- and two-dimensional ("heatmap") histograms in the Portal's active chart.


**1. Execute a query.**
Go to the Portal's DP0.2 Catalogs tab, switch to the ADQL interface, and execute the query below.
This query will retrieve g- and r-band magnitudes for a sample of extended objects (galaxies) brighter than 25th magnitude.

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


**2. Add a new chart, and choose histogram.**
In the Active Chart panel, click on the "+" button in the upper-left corner of the panel.
In the "Add New Chart" pop-up window select "Histogram" as the plot type and enter ``g_cModelMag`` as the column (Figure 1).
Click "OK".

.. figure:: /_static/portal-howto-histograms-1.png
	:name: portal-howto-histograms-1
	:alt: Screenshot of the "Add New Chart" pop-up window, set up for a histogram.

Figure 1: The "Add New Chart" pop-up window, set up for a histogram.


**3. Delete the default chart.**
Remove the default plot of ``coord_ra`` vs. ``coord_dec`` by clicking on the "x" in the upper right corner of the plot.


**4. Add a new chart, and choose heatmap.**
Open the "Add New Chart" pop-up window.
Select "Heatmap" as the plot type and enter ``g_cModelMag`` for X and the expression ``g_cModelMag`` - ``r_cModelMag`` for Y (Figure 2).
Leave the Color Scale as "Default".
Click "OK".

.. figure:: /_static/portal-howto-histograms-2.png
	:name: portal-howto-histograms-2
	:alt: Screenshot of the "Add New Chart" pop-up window, set up for a heatmap.

Figure 2: The "Add New Chart" pop-up window, set up for a heatmap.


**5. View the histogram and heatmap.**
The Active Charts panel now displays a 1-dimensional histogram of the g-band magnitudes at left,
and a 2-dimensional histogram (a heatmap) of the g-band magnitude vs. the g-r color at right,
as in Figure 3.

.. figure:: /_static/portal-howto-histograms-3.png
	:name: portal-howto-histograms-3.png
	:alt: Screenshot of the Active Charts showing a 1-d histogram and a 2-d heatamp.

Figure 3: The Active Charts panel displays the two histograms.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
