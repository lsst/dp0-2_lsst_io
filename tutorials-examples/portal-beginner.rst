.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-Beginner:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###################################################
01. Bright Stars Color-Magnitude Diagram (beginner)
###################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham and Greg Madejski

**Last verified to run:** 2023-01-05

**Targeted learning level:** beginner

**Introduction:**
This tutorial uses the Single-Table Query interface to search for bright stars in a small region of sky,
and then uses the Results interface to create a color-magnitude diagram.
This is the same demonstration used to illustrate the Table Access Protocol (TAP) service in the first of the :ref:`DP0-2-Tutorials-Notebooks`.
Beginner-level users looking for a more general overview of the Portal Aspect should refer to this :doc:`/data-access-analysis-tools/portal-intro`.


.. _DP0-2-Portal-Beginner-Step-1:

Step 1. Set the query constraints
=================================

1.1. Log in to the Portal Aspect.

1.2. Under "TAP Searches", leave "1. Select TAP Service" at its default "LSST RSP \https://data.lsst.cloud/api/tap", and leave "2. Select Query Type" at its default "Single Table (UI assisted)".

1.3. Next to "3. Select Table", choose the Table Collection to be "dp02_dc2_catalogs" (left drop-down menu) and the Table to be "dp02_dc2_catalogs.Object" (right drop-down menu).

1.4. Under "4. Enter Constraints", select the box to the left of "Spatial".
Set the "Longitude Column" to "coord_ra", the "Latitude Column" to "coord_dec", to match the sky coordinates column names in the Object table.
Leave the "Shape Type" as the default "Cone", and for "Coordinates or Object Name" use the central coordinates of the DC2 simulation area "62, -37".
Next to "Radius", from the drop down menu choose "degrees" *and then* enter "1" in the box and press enter to set the search radius to 1 degree.

1.5. In the table at right, under "Output Column Selection and Constraints", click the box in the left-most column to select "column_names" "coord_ra", "coord_dec", "detect_isPrimary", "g" "r" and "i_calibFlux", and "g" "r" and "i_extendedness".
Click on the funnel symbol at the top of the checkbox column to filter the table view to show selected columns only.

1.6. In the "constraints" column, enter "=1" for the "detect_isPrimary", ">360" for the fluxes, and "=0" for the extendedness parameters.
This will limit the objects returned to those with no children (i.e., the products of deblending), which are brighter than about 25th magnitude
in the g, r, and i filters, and which appear to be point-like (not extended, but *not necessarily stellar*) in those three filters as well.

At this point the boxes selecting the "extendedness" and "detect_isPrimary" parameters can be unchecked, because
it is not necessary for this tutorial to actually retrieve the data in those columns, only to constrain the query based on their values.

**Notice:** At this point, with the query all set up, clicking "Populate and Edit ADQL" will switch the Query Type to "Edit ADQL (advanced)" and populate the ADQL query box, as shown in Step 3 below.

1.7. Set the "Row Limit" to 10000, to only retrieve 10000 objects for this demonstration.

.. figure:: /_static/portal_tut01_step01.png
	:name: portal_tut01_step01
	
	The above screenshot shows the constraints before clicking "Search".
	
1.8. Click "Search" at lower left.


.. _DP0-2-Portal-Beginner-Step-2:

Step 2. Create the color-magnitude diagram
==========================================

The default Results view shows a sky-image at upper left (with the coordinates of returned objects marked on it),
a xy table at upper right, and a table of the results values along the bottom.
At the time this tutorial was created, the sky-image was still 2MASS and not a DC2 simulated image, so this tutorial does not involve use of the sky-image.

2.1. In the upper left corner, click "xy-tbl" to show only the default xy plot along the top (in this case, plotting the two sky coordinates columns), and the table along the bottom of the screen.

**Notice:** The objects retrieved *do not* fill in the search area (a 1 degree radius) in the xy plot of "coord_ra" versus "coord_dec".
This is because a row limit of 10000 objects was applied, and the data is partitioned into files by sky coordinate.
The query accessed these files until 10000 objects were found (i.e., the query *does not* find *all objects* that satisfy the query parameters and then choose 10000 random objects to return).

.. figure:: /_static/portal_tut01_step02a.png
	:name: portal_tut01_step02a
	
	The Results view with "xy-tbl" selected.
	

**Notice:** In order to plot color (r-i magnitude) versus magnitude (g), the fluxes (which are in units of nanojansky) are being converted to AB magnitudes in the next step. The `AB Magnitudes Wikipedia <https://en.wikipedia.org/wiki/AB_magnitude>`_ page provides a concise resource for users who are unfamiliar with AB magnitudes and fluxes in units of janskys.

2.2. Click on the xy plot settings icon (two gears, upper right) in order to "modify trace", which means to change the plot parameters.
Set "X" to be "(-2.5 * log10(r_calibFlux)) - (-2.5 * log10(i_calibFlux))", and "Y" to be "-2.5 * log10(g_calibFlux) + 31.4".
Leave the color scale and the bins as they are, and click on "Chart Options" to show the options.
For "Chart title" enter "Color-Magnitude Diagram"; set "X Label" to "color (r-i)"; set "Y Label" to "magnitude (g)", and underneath check the "Options" box for "reverse".
Set the "X Min/Max" values to "-0.5" and "2.0", and the "Y Min/Max" values to "16.5" and "25.5".

.. figure:: /_static/portal_tut01_step02b.png
	:name: portal_tut01_step02b
	
	Set the plot parameters.

2.3. Click "Apply" and then "Close" the pop-up window, and look at the color-magnitude plot.

.. figure:: /_static/portal_tut01_step02c.png
	:name: portal_tut01_step02c
	
	The color-magnitude diagram.

**Notice:** The default plot style is a a two-dimensional histogram, which is appropriate for very large data sets.
In this case, with only 10000 object retrieved, create a scatter plot for comparison.

**Notice:** The simulated data is visibly quantized in the above plot, and this will not be the case with real data.
The discrete sequences at red colors, (g-i) > 0.5, come from the discretized procedure used to simulate low-mass stars in the DP0.2 data set.

2.4. Click on the xy plot settings icon (two gears, upper right) again, but this time choose "Add New Chart".
Leave "Plot Type" at the default, "Scatter", and then set the "X" and "Y" to the same equation as in Step 2.2.
Use the same "Chart Options" except give it a different "Chart title", such as "Scatter CMD".

.. figure:: /_static/portal_tut01_step02d.png
	:name: portal_tut01_step02d
	
	Set the new chart parameters for a scatter plot.

2.5. Click "OK" and "Close", and look at the new color-magnitude plot.

.. figure:: /_static/portal_tut01_step02e.png
	:name: portal_tut01_step02e
	
	The color-magnitude diagrams, including the new scatter plot (right).

2.6. Interact with the plot.
Hover over the data points with a mouse and see the x and y values appear in a pop-up window.
Select a row in the table and it appears as a different color in the plot, and vice-versa: select a point in the plot and it is highlighted in the table below.


.. _DP0-2-Portal-Beginner-Step-3:

Step 3. Do the same query with ADQL
===================================

3.1. Clear the search results and return to the main Portal interface.
Under "2. Select Query Type" select "Edit ADQL (advanced)", and enter the following in the box under "ADQL Query".

.. code-block:: SQL

   SELECT coord_dec,coord_ra,g_calibFlux,i_calibFlux,r_calibFlux
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS (POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 62.0, -37.0, 1)) = 1
   AND detect_isPrimary =1
   AND g_calibFlux >360 AND g_extendedness =0
   AND i_calibFlux >360 AND i_extendedness =0
   AND r_calibFlux >360 AND r_extendedness =0

3.2. At the bottom of that page, set the "Row Limit" to 10000 and then click "Search" at lower left.
The Portal will transition to the "Results View" as in Step 2, above.

**Notice:** although the same "Row Limit" of 10000 was applied both in Step 1.7 and Step 3.2,
the two searches will not return the exact same rows.
Queries which return only a subset of all possible results, in this case 10000 out of all possible rows,
will return random subsets.



.. _DP0-2-Portal-Beginner-Step-4:

Step 4. Transfer ADQL queries or results from the Portal to the Notebook Aspect
===============================================================================

4.1. As described under Step 1.6, once a query is all set up in the Portal using the "Single Table (UI assisted)",
click "Populate and Edit ADQL" to switch the Query Type to "Edit ADQL (advanced)" and populate the ADQL query box.
Shown below is the same query as in Step 3.1 above:  

.. figure:: /_static/portal_tut01_step04a.png  
	:name: portal_tut01_step04a
	
To execute the query in the Portal, click the "Search" button.

To execute the query in the Notebook Aspect, copy-paste the ADQL statement into the code cell of any notebook that
which uses the TAP service, as demonstrated in Section 2.3 of the first tutorial notebook, 01 Introduction to DP0.2.

4.2. It is also possible to obtain a URL for direct access to the query results.
This URL can be used from the Notebook Aspect; this is an especially useful feature for 
queries that are large, complex, or time-consuming to execute (for instance, multiple table joins),
or for sharing query results with colleagues.

As an example, the image below displays the Results View for a small query using just a 0.05 degree radius.

.. figure:: /_static/portal_tut01_step04b.png  
	:name: portal_tut01_step04b

Click on the "info" button (letter "i" in a circle), and a pop-up window will appear:

.. figure:: /_static/portal_tut01_step04c.png  
	:name: portal_tut01_step04c

The "Job Link" in the pop-up is the URL to the query results.
Click on the clipboard icon to copy the URL to your clipboard.

As demonstrated in Section 5.4 of the second tutorial notebook, 02 Catalog Queries with TAP,
the URL can be pasted into a code cell and the query results retrieved using the following commands:

.. code-block:: SQL

	retrieved_job = retrieve_query('https://data.lsst.cloud/api/tap/async/myjob12345')
	retrieved_results = retrieved_job.fetch_result().to_table().to_pandas()

This results in having the same data in your notebook which you first obtained via the Portal Aspect.
