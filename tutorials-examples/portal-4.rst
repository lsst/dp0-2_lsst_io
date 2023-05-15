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

For more information about the DP0.2 catalogs, tables, and columns, visit the DP0.2 Data Products Definition Document (DPDD) or the DP0.2 Catalog Schema Browser.

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

.. _DP0-2-Portal-Histogram-Step-A3:

Step A3.  Generating a histogram of start times of visits at the selected location
==================================================================================

A3.1.  To generate such a histogram, click on the "Add Chart" button on the top of your window.  

.. figure:: /_static/portal_tut04_step03.png
	:name: portal_tut04_step03

A new window will appear asking for the plot type.  Select "Histogram" here.  For the "Column or expression" select "t_min."  You can select any number of bins in the histogram - say, 100.  You will be given the full range of t_min times (Min and Max) in your table - which you can override.  Clicking "OK" will generate a new panel with a plot of history of Rubin observations at location (62.0, -37.0).  As you can see on the plot below, there is a clear seasonal pattern of the Rubin Observatory visits to your selected location.  You can augment the plot with a title and labels for axis by clicking the two gears on upper right, and then modifying "Chart Options."    

.. figure:: /_static/portal_tut04_step04.png
	:name: portal_tut04_step04

The default histogram includes visits with any filter.  You can select, for instance, the "u" filter by entering it into the header of the table at the bottom of your window. You would do it by clicking on the litle black arrow in the "lsst_band" column, selecting "u" there, and clicking on the "filter" text again.  This will significantly reduce the number of entries in your table - not surprising, as the DP0.2 data set has many fewer observtions with the "u" filter as they can be made only in the dark time.  

.. figure:: /_static/portal_tut04_step05.png
	:name: portal_tut04_step05

.. _DP0-2-Portal-Histogram-Part-B:


Part B:  Generate a histogram of fluxes of objects in a selected region of the sky 
==================================================================================

.. _DP0-2-Portal-Histogram-Step-B1:

Step B1.  Enter the parameters of the query
===========================================

B1.1.  Here, we will execute a smiple query, extracting fluxes of all sources in the selected region of the sky.  Once the Portal aspect is started, in the "Select Query Type" select the "Single Table (UI assisted)."  In the "Select Table" field, for the "Table Collection" select "dp02_dc2_catalogs" and for the "Table" select "dp02_dc2_catalogs.Object."  

B1.2.  In the field "Enter Constraints" select "Spatial" with "Longitude Column" to be "coord_ra" and "Lattitude Column" to be "coord_dec."  For coordinates - you can enter any location that is within the DP0.2 footprint, say 62.0, -37.0.  

.. _DP0-2-Portal-Histogram-Step-B2:

Step B2.  Enter the search constraints
======================================

B2.1.  To reduce the number of returned objects, you might want to restrict the radius to 360 arcseconds by entering this into the "Spatial Constraints" box.  Likewise, you might wish to consider only bright-ish objects, say with a flux greater than 360 nJy.  To this end, in the "Output Column Selection and Constraints" for the g_calibFlux, i_calibFlux, and r_calibFlux rows, enter >360 as the constraints.  Clicking "Search" as below will return a table of ~ 4000 objects.  

.. figure:: /_static/portal_tut04_step06.png
	:name: portal_tut04_step06

.. _DP0-2-Portal-Histogram-Step-B3:

Step B3.  Generate the histogram of g-band fluxes
=================================================

B3.1.  To generate such a histogram - as you did in part A - click on the "Add Chart" buttom on the top of your window.  In the window which just apeared, select "Histogram."  For the "Column or expression" enter "log10(g_calibFlux)."  

.. figure:: /_static/portal_tut04_step07.png
	:name: portal_tut04_step07
	
This will result in the plot on the upper right panel on the screenshot below.  If you wish you can add a chart with the same settings as the previous one, but with log axis for the number, select "log" for the Chart Options of the plot (as is in the left panel).  Such plot is often called "log(N) - log(S)."  

.. figure:: /_static/portal_tut04_step08.png
	:name: portal_tut04_step08

.. _DP0-2-Portal-Histogram-Part-C:  

Part C:  Generate a two-dimensional color - magnitude histogram ("heat map") of extended sources
============================================================================================

.. _DP0-2-Portal-Histogram-Step-C1:

Step C1.  Enter the parameters of the query
===========================================

C1.1.  Here, we will use a somewhat more complex query than in parts A and B.  But for starters, as we did in the previous parts, in the "Select Query Type" select the "Single Table (UI assisted)."  In the "Select Table" field, for the "Table Collection" select "dp02_dc2_catalogs" and for the "Table" select "dp02_dc2_catalogs.Object."  In the field "Enter Constraints" select "Spatial" with "Longitude Column" to be "coord_ra" and "Lattitude Column" to be "coord_dec."  For coordinates - you can enter any location that is within the DP0.2 footprint, say 62.0, -37.0.  


.. _DP0-2-Portal-Histogram-Step-C2

Step C2.  Enter the search constraints 
======================================

C2.1.  For this part, we will need a larger number of objects, which will make the distribution of object color vs. magnitude more clear.  To this end, restrict the  radius to 1 degree by entering this into the "Spatial Constraints" box.  As you did before, select only bright-ish objects:  in the "Output Column Selection and Constraints" for the g_calibFlux, i_calibFlux, u_calibFlux, and r_calibFlux rows, enter >360 as the constraints.  

C2.2.  This time, add two additional constraints:  enter =1 for detect_isPrimary row (to exclude blended objects), and enter =1 for the g_extendedness row.  Such constraints presumably will favor un-blended extended objects such as individual galaxies.  You can un-click the box under the little funnel (filter icon) for the "detect_isPrimary" and "g_extendedness" rows since you only need to select on those parameters and don't need to have them returned in the output table.   Clicking "Search" as below will take about a minute, and will return a table of ~ 160000 objects.  

.. figure:: /_static/portal_tut04_step09.png
	:name: portal_tut04_step09


.. _DP0-2-Portal-Histogram-Step-C3:

Step C3.  Plot the 2-dimensional color histogram
================================================

C3.1.  Click on the two gears on the upper right-hand side of the screen, to set the plot parameters.  
For X, enter "-2.5 * log10(g_calibFux)+ 31.4" and for Y, enter "-2.5 * log10(i_calibFux) - (-2.5 * log10(u_calibFux))" - this will convert fluxes to magnitudes (and their differences) in the selected bands.  You can enter any color scale - whichever you find most compelling.  In the "Chart Options" part you can enter the chart title and axis labels.  Click "Apply" and then "Close."  

.. figure:: /_static/portal_tut04_step10.png
	:name: portal_tut04_step10

C3.2.  The resulting color-magnitude diagram of objects in your search area will look as below.  

.. figure:: /_static/portal_tut04_step11.png
	:name: portal_tut04_step11
	
You can see the distribution of galaxy colors as a function of their apparent magnitudes is not uniform.  Can you think of why?  

Beginner-level users looking for a more general overview of the Portal Aspect should refer to this :doc:`/data-access-analysis-tools/portal-intro`.


