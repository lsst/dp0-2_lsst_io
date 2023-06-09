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

**Last verified to run:** 2023-04-07

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

1.2. Under "TAP Searches", leave the "Use Image Search (ObsTAP)" box unchecked, and leave "View" at its default "UI assisted".

1.3. Next to "LSST DP0.2 DC2 Tables", choose the Table Collection to be "dp02_dc2_catalogs" (left drop-down menu) and the Table to be "dp02_dc2_catalogs.Object" (right drop-down menu).

1.4. Under "Enter Constraints", select the box to the left of "Spatial".
Leave the "Shape Type" as the default "Cone", and for "Coords or Obj Name" use the central coordinates of the DC2 simulation area "62, -37".
Next to "Radius", from the drop down menu choose "degrees" *and then* enter "1" in the box and press enter to set the search radius to 1 degree.

1.5. In the table at right, under "Output Column Selection and Constraints", click the box in the left-most column to select "coord_ra", "coord_dec", "detect_isPrimary", "g" "r" and "i_calibFlux", and "g" "r" and "i_extendedness". Column names are searchable. To avoid scrolling a long column list, 
enter a keyword (e.g., "calibFlux") in the box right below the "Name" column. It will list all the column names containing the given keyword. 
After selecting the needed columns (e.g., "g" "r" and "i_calibFlux"), clear the box and hit the return key to continue selecting other columns. 
Click on the funnel symbol at the top of the checkbox column to filter the table view to show selected columns only.

1.6. In the "constraints" column, enter "=1" for the "detect_isPrimary", ">360" for the fluxes, and "=0" for the extendedness parameters.
This will limit the objects returned to those with no children (i.e., the products of deblending), which are brighter than about 25th magnitude
in the g, r, and i filters, and which appear to be point-like (not extended, but *not necessarily stellar*) in those three filters as well.

At this point the boxes selecting the "extendedness" and "detect_isPrimary" parameters can be unchecked, because
it is not necessary for this tutorial to actually retrieve the data in those columns, only to constrain the query based on their values.

**Notice:** At this point, with the query all set up, clicking "Populate and Edit ADQL" will switch the Query Type to "Edit ADQL" and populate the ADQL query box, as shown in Step 3 below.

1.7. Set the "Row Limit" to 10000, to only retrieve 10000 objects for this demonstration.

.. figure:: /_static/portal_tut01_step01.png
	:name: portal_tut01_step01
	
	The above screenshot shows the constraints before clicking "Search".
	
1.8. Click "Search" at lower left.


.. _DP0-2-Portal-Beginner-Step-2:

Step 2. Create the color-magnitude diagram
==========================================

The default "Tri-view" layout shows a sky coverage map from DESC DC2 simulation at upper left, an active chart showing the spatial distribution of returned 
objects at upper right, and a table of the search results along the bottom.

.. figure:: /_static/portal_tut01_step02a.png
	:name: portal_tut01_step02a
	
	The default Results view with "Tri-view".

2.1. In the upper right corner, click "Bi-view Tables" to show only either the active chart or the sky coverage map (switching between the two by clicking the tap "Active Chart"/"Coverage") in the right along with the table in the left of the screen.

**Notice:** The objects retrieved *do not* fill in the search area (a 1 degree radius) in the default active chart of "coord_ra" versus "coord_dec".
This is because a row limit of 10000 objects was applied, and the data is partitioned into files by sky coordinate.
The query accessed these files until 10000 objects were found (i.e., the query *does not* find *all objects* that satisfy the query parameters and then choose 10000 random objects to return).

.. figure:: /_static/portal_tut01_step02b.png
	:name: portal_tut01_step02b
	:alt: This screenshot of the portal after a search query is run.  The top image shows the density of selected sources within the search area. 
	  In this case, a circle of radius that is selected by the user centered at the right ascension and declination location selected by the user. 
	  The bottom panel displays the returned objects from the search query as a table.
	
	The Results view with "Bi-view Tables" selected.
	

**Notice:** In order to plot color (r-i magnitude) versus magnitude (g), the fluxes (which are in units of nanojansky) are being converted to AB magnitudes in the next step. The `AB Magnitudes Wikipedia <https://en.wikipedia.org/wiki/AB_magnitude>`_ page provides a concise resource for users who are unfamiliar with AB magnitudes and fluxes in units of janskys.

2.2. Click on the Active Chart settings icon (two gears, upper right) in order to "modify trace", which means to change the plot parameters.
Set "X" to be "(-2.5 * log10(r_calibFlux)) - (-2.5 * log10(i_calibFlux))", and "Y" to be "-2.5 * log10(g_calibFlux) + 31.4".
Leave the options on "Trace Options" as they are, and click on "Chart Options" to show the options.
For "Chart title" enter "Color-Magnitude Diagram"; set "X Label" to "color (r-i)"; set "Y Label" to "magnitude (g)", and underneath check the "Options" box for "reverse".
Set the "X Min/Max" values to "-0.5" and "2.0", and the "Y Min/Max" values to "16.5" and "25.5".

.. figure:: /_static/portal_tut01_step02c.png
	:name: portal_tut01_step02c
	:alt: A screenshot of the portal aspect showing the interface that allows the user to create charts from the data returned by the query. 
	  Creating plots from the data in this way is an easy and functional way to explore the data. 
	  The interface allows the user to: input functions of the returned data to plot, choose a color scheme, edit the binning, create labels and edit the axis scaling. 
	:width: 300
	
	Set the plot parameters.

2.3. Click "Apply" and then "Close" the pop-up window, and look at the color-magnitude plot.

.. figure:: /_static/portal_tut01_step02d.png
	:name: portal_tut01_step02d
	:alt: A screenshot of the chart created from the data returned by the query using the xy interface of the portal aspect. 
	  The chart shows a color magnitude diagram, g-band AB magnitude vs r-band minus i-band color, for the objects returned by the search query. 
	  This example demonstrates how to quickly explore the data returned in the search query. 
	  The plot shows a large density of stars at low r-i color, and discrete bins at redder r-i color because the simulated data is 
	  based on discrete red stellar models that were used as input into DP0.2. Real data is expected to instead show a smooth distribution of colors.
	
	The color-magnitude diagram.

**Notice:** The default plot style is a scatter plot, which is appropriate for our data set of a modest size (such as 10000 objects retrieved here).  
It is also possible to create a two-dimensional histogram, appropriate for large data sets (a "heat map") which we will make in Step 2.4.  

**Notice:** The simulated data is visibly quantized in the above plot, and this will not be the case with real data.
The discrete sequences at red colors, (g-i) > 0.5, come from the discretized procedure used to simulate low-mass stars in the DP0.2 data set.

2.4. Click on the xy plot settings icon (two gears, upper right) again, but this time choose "Add New Chart."  
Change the "Plot Type" to "Heatmap", and then set the "X" and "Y" to the same equation as in Step 2.2.
Use the same "Chart Options" except give it a different "Chart title", such as "Heatmap Color-Magnitude Diagram."  

.. figure:: /_static/portal_tut01_step02e.png
	:name: portal_tut01_step02e
	:alt: Screenshot of dialog box where the user can set new chart parameters for the heat map.
	:width: 300
	
	Above, we set the new chart parameters for a heatmap plot.

2.5. Click "OK" and "Close", and look at the new color-magnitude plot.  For completeness, you might wish to update the title of the plot you generated previously to "Scatter Color-Magnitude Diagram."  

.. figure:: /_static/portal_tut01_step02f.png
	:name: portal_tut01_step02f
	:alt: Color magnitude diagrams generated from the previously mad scatter plot and heatmap.
	
	The color-magnitude diagrams, including the previously made scatter plot (left) and the heatmap (right).

2.6. Interact with the plot.
Hover over the data points with a mouse either on the Coverage map (see the coordinates change in the bottom of the map) or the Active Chart (see the x and y values appear in a pop-up window). 
Select a row in the table and it appears as a different color in the plot(s), and vice-versa: select a point in a plot and it is highlighted in the table below.


.. _DP0-2-Portal-Beginner-Step-3:

Step 3. Do the same query with ADQL
===================================

3.1. Clear the search results and return to the main Portal interface.
In the upper right, select "Edit ADQL" for "View", and enter the following in the box under "ADQL Query".

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

4.1. As described under Step 1.6, once a query is all set up in the Portal using the "UI assisted",
click "Populate and Edit ADQL" to switch the Query Type to "Edit ADQL" and populate the ADQL query box.
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

The "UWS JOB URL" in the pop-up is the URL to the query results.
Click on the clipboard icon to copy the URL to your clipboard.

As demonstrated in Section 5.4 of the second tutorial notebook, 02 Catalog Queries with TAP,
the URL can be pasted into a code cell and the query results retrieved using the following commands:

.. code-block:: SQL

	retrieved_job = retrieve_query('my_portal_url')
	retrieved_results = retrieved_job.fetch_result().to_table().to_pandas()

This results in having the same data in your notebook which you first obtained via the Portal Aspect.

We note that URLs will not be accessible indefinitely, but rather are intended to serve the use case of immediate access and analysis. 
To preserve and recreate queries at a later date, it is recommended to save the ADQL-formatted query as described in step 1.6.
