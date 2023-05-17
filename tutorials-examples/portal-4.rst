.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-4:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#########################################################
04. Exploring Extended Object Populations with Histograms
#########################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham and Greg Madejski

**Last verified to run:** 2023-05-14

**Targeted learning level:** intermediate

**Introduction:** This tutorial demonstrates how to retrieve apparent magnitudes and cluster offsets for a sample of extended objects around a rich galaxy cluster, and use 1- and 2-dimensional histograms to explore their apparent magnitude and color distributions.

This tutorial assumes the successful completion of the beginner-level Portal tutorial 01, and uses the Astronomy Data Query Language (ADQL), which is similar to SQL (Structured Query Language).

For more information about the DP0.2 catalogs, tables, and columns, visit the DP0.2 Data Products Definition Document (DPDD) :ref:`DP0-2-Data-Products-DPDD` or the DP0.2 Catalog Schema Browser (it is at https://dm.lsst.org/sdm_schemas/browser/dp02.html ).  

.. _DP0-2-Portal-Histogram-Step-1:

Step 1.  Execute the ADQL query
===============================

1.1.  Log into the Portal Aspect.  

1.2.  Next to “2. Select Query Type," switch from the default “Single Table (UI assisted)” to “Edit ADQL (advanced)”.

1.3. Enter the following ADQL code into the “ADQL Query” box:  

.. code-block:: SQL 

   SELECT coord_dec, coord_ra, detect_isPrimary, 
   scisql_nanojanskyToAbMag(g_calibFlux) as gmag, 
   scisql_nanojanskyToAbMag(r_calibFlux) as rmag, 
   g_extendedness as gext, 
   r_extendedness as rext, 
   DISTANCE(POINT('ICRS', coord_ra, coord_dec), POINT('ICRS', 55.75, -32.27)) as radial_offset 
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 55.75, -32.27, 1.0)) = 1 
   AND detect_isPrimary = 1 
   AND g_extendedness = 1 
   AND r_extendedness = 1 
   AND scisql_nanojanskyToAbMag(g_calibFlux) < 25 
   AND scisql_nanojanskyToAbMag(r_calibFlux) < 25 

1.4. Notice how the ADQL query above retrieves the g- and r-band `calibFlux` columns from the Object catalog as apparent AB magnitudes, and renames them as `gmag` and `rmag`. The `calibFlux` is the flux within a 12 pixel aperture; aperture fluxes are appropriate to use when calculating extended object colors, as is done in this tutorial. The query also retrieves the g- and r-band extendedness parameters as `gext` and `rext`, and the distance of the object from the search center, RA 55.75, Dec -32.27 degrees (the center of a rich galaxy cluster) as `radial_offset` (the units will be degrees).

1.5. Notice how the ADQL query above places a condition that returned objects must be within 1 degree of the search center; must have the `detect_isPrimary` flag equal to 1; must have the g- and r-band extendedness parameters equal to 1 (i.e., be extended and not point-like); and have g- and r-band apparent magnitudes brighter than 25. These conditions will return only bright, deblended, extended objects (i.e., individual galaxies).

1.6. Set the “Row Limit” at the bottom of the page to 300,000, and click “Search” in the lower left corner.  

.. figure:: /_static/portal_tut04_step01.png
	:name: portal_tut04_step01


.. _DP0-2-Portal-Histogram-Step-2:

Step 2.  Explore the default results view
==========================================

2.1. The above query should have returned 229,570 objects and the default results “tri-view” interface should look like the image below, with the sky image at left, a default xy plot of Dec vs. RA at right, and the tabular results along the bottom.

.. figure:: /_static/portal_tut04_step02a.png
	:name: portal_tut04_step02a

2.2. Notice in the sky image at left (above) that not all galaxies appear to be marked with a square as a returned object. (You might have to use the magnifying glass icon with the + sign at upper left to zoom in). This seems to suggest that objects are missing from the results table, when in fact not all returned objects are shown with markers in the sky image.

2.3. In the table view, add a constraint of `radial_offset < 0.03` as shown below, and see how the sky image plot updates to show that all extended members of the rich galaxy cluster were returned by the query (below). So the fact that above, not all are marked with icons, is not an issue for concern.

.. figure:: /_static/portal_tut04_step02b.png
	:name: portal_tut04_step02b

2.4. Delete the “< 0.03” constraint on the `radial_offset` column and press enter to reset the results view.

.. _DP0-2-Portal-Histogram-Step-3:

Step 3.  Change the heatmap to a color-magnitude diagram
========================================================

Galaxy color-magnitude diagrams (CMDs) are a standard and widely-used diagnostic plot type, and use of the g-r color vs. g-band magnitude are standard choices for axes. This type of plot is created below.  

3.1. Change the settings of the default xy plot of RA and Dec. At upper right, click the double-gears (settings) icon to open the "Plot Parameters" pop-up window. Select “Overplot New Trace”, and fill in the boxes as shown below.

.. figure:: /_static/portal_tut04_step03a.png
	:name: portal_tut04_step03a

3.2. See that now the plot has both the color-magnitude diagram and the RA vs. Dec. This is not very useful!  But, the purpose of showing this is to demonstrate the flexibility of the Portal’s plotting capabilities.

.. figure:: /_static/portal_tut04_step03b.png
	:name: portal_tut04_step03b
	
3.3. Remove the default “trace 0” (RA vs. Dec) from the plot. Click on the double-gears icon again. In the pop-up window, with "Modify Trace" selected, from the "Choose Trace" drop-down menu select "trace 0", and then from the top row choose "Remove Active Trace", and then click "OK". Now, the “CMD” trace created in step 3.1 is the only one.

.. figure:: /_static/portal_tut04_step03c.png
	:name: portal_tut04_step03c
	
3.4. Change the grey-scale color palette to something more exciting. Click on the double-gears icon again and in the drop-down menu next to “Color Scale” choose “YlOrRd”. Notice that the color bar at right has the name of the trace, “CMD”, and represents the number of objects per 2-dimensional bin.

.. figure:: /_static/portal_tut04_step03d.png
	:name: portal_tut04_step03d

3.5. Interact with the plot. At upper right, select the magnifying glass with the + sign icon and click-and-drag over the data to zoom in on a small area. Select the four-arrows-pointing-out icon and click-and-drag to navigate around the plot. Select the magnifying glass with 1x icon to return the plot to the default axes limits.

3.6. Be aware that clicking the half-circle upwards-pointing “go back” or “refresh” icon will return the xy plot to its default display of RA vs. Dec. Do not click it.

3.7. Notice the sharp cutoffs at the bright end (around g=17, g-r=0.5) and the faint end (around g=24.5, g-r=0.2), and recall that the DP0.2 data set is based on simulated astrophysical objects and simulated images. Notice that a clear red sequence, blue cloud, and green valley is not very obvious in this galaxy CMD. A real LSST color-magnitude diagram for galaxies might look quite different.

.. _DP0-2-Portal-Histogram-Step-4:

Step 4.  Add a plot showing histograms of apparent magnitude
============================================================

Distributions of apparent magnitude are another standard type of plot that gives an at-a-glance impression of the brightness and completeness of a population of galaxies.

4.1. Add a new plot. At upper right, click on the double-gears icon and select “Add New Chart” in the "Plot Parameters" pop-up window. Select a Plot Type of Histogram from the drop-down menu, and set the other boxes to match the screenshot below. 

.. figure:: /_static/portal_tut04_step04a.png
	:name: portal_tut04_step04a

4.2. Notice the histogram options available. In this demo, as shown above, a “Uniform binning” is used instead of “Bayesian blocks” (quantiles defined by the data itself); a set bin width of 0.2 mag is selected; and the minimum and maximum values are defined. However, users do have the option to instead choose the number of bins, and allow the bin size and the min/max values will be set automatically.

4.3. Review the g-band apparent magnitude distribution. Since the ADQL query only retrieved extended objects brighter than 25th magnitude, and the coadded images of DP0.2 (and thus the Object table) goes deeper than 25th mag, no turn-over due to detection incompleteness is seen in the apparent magnitude distribution. 

.. figure:: /_static/portal_tut04_step04b.png
	:name: portal_tut04_step04b

4.4. Add the r-band apparent magnitude distribution to the new plot. With the right-most plot selected (click on plot to select plot; selected plot has an orange outline), click on the double-gears icon at upper right. In the "Plot Parameters" pop-up window, select “Overplot New Trace”, fill out the remaining boxes as shown below (notice that the option to log the y-axis has been selected), and click “OK”.

.. figure:: /_static/portal_tut04_step04c.png
	:name: portal_tut04_step04c

4.5. Update the trace names and colors. The default colors used for g-band and r-band are inappropriate, and the g-band trace is still named “trace 0”. Click on the double-gears icon and use the "Plot Parameters" pop-up window to edit trace name and color. Click on the magnifying glass to the right of “Color” under “Trace Options” to get the “Color Picker” pop-up window. Choose green for g-band and orange for r-band.

.. figure:: /_static/portal_tut04_step04d.png
	:name: portal_tut04_step04d

4.6. Review the final plot. Notice that it is possible to change which trace is “in front” using the drop-down menu to the left of the magnifying glass icon. Bring the g-band trace to the front.

.. figure:: /_static/portal_tut04_step04e.png
	:name: portal_tut04_step04e

Step 5.  Restrict all plots to objects near the rich cluster
============================================================

5.1. View the sky image, the color-magnitude diagram, and the apparent magnitude histograms for the full set of returned objects.

.. figure:: /_static/portal_tut04_step05a.png
	:name: portal_tut04_step05a

5.2. Restrict the results to only those objects within < 0.05 degrees of the cluster center by entering “< 0.05” into the constraints box for the `radial_offset` column and clicking enter. Notice how all of the plots automatically update. The CMD (center) shows the red sequence of cluster galaxies, and the histogram (right) shows the over-density of bright objects in the cluster. Cool!

.. figure:: /_static/portal_tut04_step05b.png
	:name: portal_tut04_step05b

Step 6.  Exercises for the learner
==================================

6.1. Return to the ADQL query in step 1.3, and re-do this tutorial but include faint extended objects down to 28th magnitude. Notice how the histograms change in shape.

6.2. Return to the ADQL query in step 1.3, and add u, i, z, and y-bands to the retrieved columns. Create an apparent magnitude histogram with all six filters. Create a color-magnitude diagram (or a color-color diagram!!) with the bands of your choice.

