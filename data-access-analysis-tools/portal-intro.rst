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

#############################################################
How to plot one- and two-dimensional histograms in the Portal
#############################################################

.. This section should provide a brief, top-level description of the page.

.. Most recent update:  October 9 2024

=====================

The Portal aspect of the Rubin Science Platform lends itself well to retrieve apparent magnitudes of (for instance) extended objects in a region of the sky.  
It provides convenient and easy to use tools to plot 1- and 2-dimensional histograms to explore their apparent magnitude and color distributions.

For the retrieval of the required data, this "How to" uses the Astronomy Data Query Language (ADQL), which is similar to SQL (Structured Query Language).
The option to use the ADQL in the Portal aspect of the Rubin Science Platform is selected by clicking on "Edit ADQL" in the upper right-hand side of the Portal landing page.  

For more information about the DP0.2 catalogs, tables, and columns, visit the DP0.2 Data Products Definition Document (DPDD) 
:ref:`DP0-2-Data-Products-DPDD` or the `DP0.2 Catalog Schema Browser <https://sdm-schemas.lsst.io/dp02.html>`_.  

.. _DP0-2-Portal-Histogram-Step-1:

1.  Preparation and execution of the ADQL query
===============================================

The sample query below uses the ``dp02_dc2_catalogs.Object`` catalog to extract the g-band and r-band fluxes (respectively ``g_calibFlux`` and ``r_calibFlux``) of all extended objects (by selecting ``g_extendedness = 1`` and ``r_extendedness = 1``).
The ``calibFlux`` is the flux within a 12 pixel aperture; aperture fluxes are appropriate to use when calculating extended object colors.  
It converts the fluxes to magnitudes, by the use of an ADQL function ``scisql_nanojanskyToAbMag`` where the respective flux is the argument (and renames them as ``gmag`` and ``rmag``).  
It restricts the search to return only objects with g and i magnitudes less than 23.  
It limits the search to those objects located in a circular region with a radius of 0.5 degree, around direction with RA of 55.75 deg and and Dec of -32.27 deg, via the restriction ``CONTAINS(POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 55.75, -32.27, 0.5) = 0.5``.

.. code-block:: SQL 

   SELECT coord_dec, coord_ra, 
   scisql_nanojanskyToAbMag(g_calibFlux) as gmag, 
   scisql_nanojanskyToAbMag(r_calibFlux) as rmag, 
   g_extendedness, 
   r_extendedness  
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 55.75, -32.27, 0.5)) = 1 
   AND g_extendedness = 1 
   AND r_extendedness = 1 
   AND scisql_nanojanskyToAbMag(g_calibFlux) < 23 
   AND scisql_nanojanskyToAbMag(r_calibFlux) < 23 

2.  Plotting the histogram of g-magnitudes
==========================================

Executing the ADQL query is via clicking the “Search” button in the lower left corner.  
The resulting display will by default show the sky coverage on the left, and the plot of the 1st column as a function of the 2nd column on the right.
To plot the distribution of g magnitudes, it is necessary to add another plot panel, by clicking on the "+" button on the upper left-hand side of the active chart, and selecting "Histogram" as the Plot Type.
The resulting  pop-up window allows a selection of the quantity for the plotted histogram - in ths case, "Column or expression" box needs to have "gmag" entered.
Clicking "Apply" will result in displaying an additional plot window, with g magnitude histogram.
The "coord_ra vs/ cpoord_dec" can be removed by clicking on the "x" in the upper right-hand side of the plot window.
This will result in the dispay as below.  

.. figure:: /_static/Howto_Histogram_1d.png
	:name: Howto_Histogram_1d.png
	:alt: Screenshot of the 1-d histogram of g-magnitudes in the selectred region, obtained by executing an ADQL query.


**Screenshot of the 1-d histogram of g-magnitudes of extended objects in the selectred region, obtained by executing an ADQL query.**

.. _DP0-2-Portal-Histogram-Step-2:

Step 2.  Explore the default results view
==========================================

2.1. The above query should have returned 229,570 objects and the default results interface should look approximately like 
the figure below, with the sky image at left, a default xy plot of Dec vs. RA at right, and the tabular results along the bottom.

2.2. In the sky image at upper left, click on the magnifying glass icon with the + sign a couple of times.
This should zoom in on the image until you can see the cluster, as in the figure below.
Notice how not all galaxies appear to be marked with a square as a returned object. 
This seems to suggest that objects are missing from the results table.
However, not all returned objects are shown with markers in the sky image.

.. figure:: /_static/portal_tut04_step02_02.png
	:name: portal_tut04_step02_02
	:alt: Screenshot of the default results view that appears after clicking the search button.

**Screenshot of default results view.**

2.3. In the table view, add a constraint of "radial_offset < 0.03" as shown below and hit return, and see how the sky image plot updates 
to show that all extended members of the rich galaxy cluster were returned by the query (below).  
So the fact that above, not all are marked with icons, is not an issue for concern.  

.. figure:: /_static/portal_tut04_step02_03.png
	:name: portal_tut04_step02_03
	:alt: The sky image view of the galaxy cluster, with purple squares marking all objects within 0.03 degrees of the center.

**Sky image view of the galaxy cluster.**

2.4. Delete the “< 0.03” constraint on the ``radial_offset`` column and press enter to reset the results view.

.. _DP0-2-Portal-Histogram-Step-3:

Step 3.  Change a heatmap illustrating a color-magnitude diagram
================================================================

Galaxy color-magnitude diagrams (CMDs) are a standard and widely-used diagnostic plot type, and use of the g-r color 
vs. g-band magnitude are standard choices for axes. 
This type of plot is created below.  

3.1. On the right-hand part of your current display, click on the "Active Chart" tab.  
Change the settings of the default xy plot of RA and Dec. 
At upper right, click the single gear (settings) icon to open the "Plot Parameters" pop-up window. 
Select “Overplot New Trace”, and fill in the boxes as shown below.

.. figure:: /_static/portal_tut04_step03_01.png
	:width: 300
	:name: portal_tut04_step03_01
	:alt: A screenshot of the plot parameters pop-up window showing how the parameters should be set to create the heatmap.

**Plot parameters pop-up window.**

3.2. See that now the plot has both the color-magnitude diagram and the RA vs. Dec. 
This is not very useful!  
But, the purpose of showing this is to demonstrate the flexibility of the Portal’s plotting capabilities.

.. figure:: /_static/portal_tut04_step03_02.png
	:name: portal_tut04_step03_02
	:alt: A screenshot of the initial plot with two heatmaps, the original coordinates heatmap and the color-magnitude heatmap.

**Intial plot with two heatmaps.**
	
3.3. Remove the default “trace 0” (RA vs. Dec) from the plot. 
Click on the single gear icon and select "Remove Active Trace" in the drop-down menu, select "trace 0", then click "OK".

.. figure:: /_static/portal_tut04_step03_03a.png
	:name: portal_tut04_step03_03b
	:alt: A screenshot of how to remove a trace.

**Screenshot to remove a trace.**


Now, the “CMD” trace created in step 3.1 is the only one.

.. figure:: /_static/portal_tut04_step03_03b.png
	:name: portal_tut04_step03_03b
	:alt: A screenshot of the color-magnitude heatmap in default.

**Default color scheme of CMD trace.**
	
3.4. Change the color palette by  
clicking on the single gears icon again and in the drop-down menu next to “Color Scale” choose from a number of color options. 
Notice that the color bar at right has the name of the trace, “CMD”, and represents the number of objects per 2-dimensional bin.


3.5. Interact with the plot. 
At upper right, select the magnifying glass with the + sign icon and click-and-drag over the data to zoom in on a small area. 
Select the four-arrows-pointing-out icon and click-and-drag to navigate around the plot. 
Select the magnifying glass with 1x icon to return the plot to the default axes limits.

3.6. Be aware that clicking the half-circle upwards-pointing arrow (the “go back” or “refresh” icon) will return the xy plot to 
its default 
display of RA vs. Dec. 
Do not click it.

3.7. Notice the sharp cutoffs at the bright end (around g=17, g-r=0.5) and the faint end (around g=24.5, g-r=0.2), and recall 
that the DP0.2 data set is based on simulated astrophysical objects and simulated images. 
Notice that a clear red sequence, blue cloud, and green valley are not very obvious in this galaxy CMD. 
A real LSST color-magnitude diagram for galaxies might look quite different.

.. _DP0-2-Portal-Histogram-Step-4:

Step 4.  Add a plot showing histograms of apparent magnitude
============================================================

Distributions of apparent magnitude are another standard type of plot that gives an at-a-glance impression of the brightness and 
completeness of a population of galaxies.

4.1. Add a new plot. At upper left of the right hand panel, click on the plus sign in a circle to add a new chart.
Select a Plot Type of "Histogram" from the drop-down menu, and set the other boxes to match the screenshot below. 

.. figure:: /_static/portal_tut04_step04_01.png
	:width: 300
	:name: portal_tut04_step04_01
	:alt: A screenshot of the plot parameters pop-up window showing how the parameters should be set to create the histogram.

**Plot parameters pop-up window for creating a histogram.**

4.2. Notice the histogram options available. 
In this demo, as shown above, a “Uniform binning” is used instead of “Bayesian blocks” (quantiles defined by the data itself); 
a set bin width of 0.2 mag is selected; and the minimum and maximum values are defined. 
However, users do have the option to instead choose the number of bins, and allow the bin size and the min/max values will be set automatically.

4.3. Review the g-band magnitude distribution. 
Since the ADQL query only retrieved extended objects brighter than 25th magnitude, and the coadded images of DP0.2 (and thus the 
Object table) goes deeper than 25th mag, no turn-over due to detection incompleteness is seen in the apparent magnitude distribution. 

.. figure:: /_static/portal_tut04_step04_03.png
	:name: portal_tut04_step04_03
	:alt: A screenshot of the portal's results view showing both the color-magnitude heatmap and the magnitude histogram.

**Color-magnitude heatmap and magnitude historgram.**

4.4. Add the r-band apparent magnitude distribution to the new plot. 
With the right-most plot selected (click on plot to select plot; selected plot has an orange outline), click on the single gear icon 
at upper right. 
In the "Plot Parameters" pop-up window, select “Overplot New Trace”, fill out the remaining boxes as shown below (notice that the 
option to log the y-axis has been selected), and click “OK”.

.. figure:: /_static/portal_tut04_step04_04.png
	:name: portal_tut04_step04_04
	:alt: A screenshot of the plot parameters pop-up window showing how to overplot a new trace and add the r-band histogram.

**Over-plot trace and add r-band histogram.**

4.5. Update the trace names and colors. 
The default colors used for g-band and r-band are inappropriate, and the g-band trace is still named “trace 0”. 
Click on the single gear icon and use the "Plot Parameters" pop-up window to edit trace name and color. 
Click on the magnifying glass to the right of “Color” under “Trace Options” to get the “Color Picker” pop-up window. 
Choose green for g-band and orange for r-band.

.. figure:: /_static/portal_tut04_step04_05.png
	:name: portal_tut04_step04_05
	:alt: A screenshot of the plot parameters and color picker pop-up windows showing how to adjust the visual aspects of the histograms.

**Color picker pop-up window.**

4.6. Review the final plot. 
Notice that it is possible to change which trace is “in front” using the drop-down menu to the left of the magnifying glass icon. 


Bring the g-band trace to the front.

.. figure:: /_static/portal_tut04_step04_06.png
	:width: 300
	:name: portal_tut04_step04_06
	:alt: A screenshot of the final histogram, showing both r-band and g-band magnitude distributions.

**Final histogram.**

Step 5.  Restrict all plots to objects near the rich cluster
============================================================

5.1. View the sky image, the color-magnitude diagram, and the apparent magnitude histograms for the full set of returned objects.

.. figure:: /_static/portal_tut04_step05_01.png
	:name: portal_tut04_step05_01
	:alt: A screenshot of the portal's results view showing both the color-magnitude heatmap and the magnitude histograms for all galaxies returned by the original search.

**Screenshot of results view.**

5.2. Restrict the results to only those objects within < 0.05 degrees of the cluster center by entering “< 0.05” into the constraints 
box for the ``radial_offset`` column and clicking enter. 
Notice how all of the plots automatically update. 
The CMD (center) shows the red sequence of cluster galaxies, and the histogram (right) shows the over-density of bright objects 
in the cluster. 
Cool!

.. figure:: /_static/portal_tut04_step05_02.png
	:name: portal_tut04_step05_02
	:alt: A screenshot of the portal's results view showing both the color-magnitude heatmap and the magnitude histograms for all galaxies within 0.03 degrees of the original search coordinates.

**Results within 0.03 degrees of the original search coordinates.**

Step 6.  Exercises for the learner
==================================

6.1. Return to the ADQL query in step 1.3, and re-do this tutorial but include faint extended objects down to 28th magnitude. 
Notice how the histograms change in shape.

6.2. Return to the ADQL query in step 1.3, and add u, i, z, and y-bands to the retrieved columns. 
Create an apparent magnitude histogram with all six filters. 
Create a color-magnitude diagram (or a color-color diagram!) with the bands of your choice.



