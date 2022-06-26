.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-Beginner:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

##################################################
01. Bright Stars Color-Magnitude Diagram (beginner)
##################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham and Greg Madejski

**Last verified to run:** 2022-06-26

**Targeted learning level:** beginner

**Introduction:**
This tutorial uses the Single-Table Query interface to search for bright stars in a small region of sky,
and then uses the Results interface to create a color-magnitude diagram.
This is the same demonstration used to illustrate the Table Access Protocol (TAP) service in the first of the :ref:`DP0-2-Tutorials-Notebooks`.
Beginner-level users looking for a more general overview of the Portal Aspect should refer to this :ref:`Data-Access-Analysis-Tools-Portal-Intro`.


.. _DP0-2-Portal-Beginner-Step-1:

Step 1. Set the query constraints
=================================

1.1. Log in to the Portal Aspect.

1.2. Under "TAP Searches", leave "1. Select TAP Service" at its default "LSST RSP https://data.lsst.cloud/api/tap", and leave "2. Select Query Type" at its default "Single Table (UI assisted)".

1.3. Next to "3. Select Table", choose the Table Collection to be "dp02_dc2_catalogs" (left drop-down menu) and the Table to be "dp02_dc2_catalogs.Object" (right drop-down menu).

1.4. Under "4. Enter Constraints", select the box to the left of "Spatial".
Set the "Longitude Column" to "coord_ra", the "Latitude Column" to "coord_dec", to match the sky coordinates column names in the Object table.
Leave the "Shape Type" as the default "Cone", and for "Coordinates or Object Name" use the central coordinates of the DC2 simulation area "62, -37".
Next to "Radius", from the drop down menu choose "degrees" *and then* enter "1" in the box and press enter to set the search radius to 1 degree.

1.5. In the table at right, under "Output Column Selection and Constraints", click the box in the left-most column to select "column_names" "coord_ra", "coord_dec", "detect_isPrimary", "g" "r" and "i_calibFlux", and "g" "r" and "i_extendedness". 
Click on the funnel symbol at the top of the checkbox column to filter the table view to show selected columns only.

1.6. In the "constraints" column, enter "=1" for the "detect_isPrimary", ">360" for the fluxes, and "=0" for the extendedness parameters.
This will limit the objects returned to those with no children (i.e., the products of deblending), which are brighter than about 25th magnitude
in the g, r, and i filters, and which appear to be point-like (not extended) in those three filters as well.

At this point the boxes selecting the "extendedness" and "detect_isPrimary" parameters can be unchecked, because
it is not necessary for this tutorial to actually retrieve the data in those columns, only to constrain the query based on their values.

1.7. Set the "Row Limit" to 10000, to only retrieve 10000 objects for this demonstration.

.. figure:: /_static/portal_tut01_step01.png
	:name: portal_tut01_step01
	
	The above screenshot shows the constraints before clicking "Search".
	
1.8. Click "Search" at lower left.


.. _DP0-2-Portal-Beginner-Step-1:

Step 2. Create the color-magnitude diagram
==========================================

2.1. The default Results view shows a sky-image at upper left (with the coordinates of returned objects marked on it),
a xy table at upper right, and a table of the results values along the bottom.
At the time this tutorial was created, the sky-image was still 2MASS and not a DC2 simulated image, so this tutorial does not involve use of the sky-image.
In the upper left corner, click "xy-tbl" to show only the default xy plot along the top (in this case, plotting the two sky coordinates columns), and the table along the bottom of the screen.

.. figure:: /_static/portal_tut01_step02a.png
	:name: portal_tut01_step02a
	
	The Results view with "xy-tbl" selected.
	
2.2. 




.. _DP0-2-Portal-Beginner-original:

Greg's Original -- Remove after updated
=======================================

After logging into the Portal Aspect, select "Single Table (UI assisted)" from the **Select Query Type**, then select the ``dp02_dc2_catalogs`` (left) and ``dp02_dc2_catalogs.Object`` (right) from the **Select Table** drop down menus.
This is demonstrated in the next figure.

.. figure:: /_static/Portal_aspect_DP02.png
	:name: Single_Table

Next, select the "Spatial" checkbox under **Enter Constraints**, and for the "Longitude Column" and "Latitude Column" enter ``coord-ra`` and ``coord-dec``.
Enter the coordinates of ``62.0, -37.0`` in the "Coordinates or Object Name:" area.
Choose a radius of ``3 arcminutes`` and select a row limit of ``10000``, as shown in the next figure.

.. figure:: /_static/Spacial_data_DP02.png
    :name: Spatial_data


.. _DP0-2-Portal-Beginner-Step-2:

Select columns for analysis
===========================

In the "Output Column Selection and Constraints" window on the lower right-hand side of the under **Enter Constraints**, select the following items:
``coord_ra``, ``coord_dec``, ``g_calibFlux``, ``i_calibFlux``, ``r_calibFlux``

..  ``clean``, ``dec``, ``extendedness``, ``good``, ``mag_g``, ``mag_i``, ``mag_r``, ``magerr_g``, ``magerr_i``, ``magerr_r``, and ``ra``.

A portion of this step is demonstrated in the next figure.
Use the search box under "column_name" to quickly find columns of interest: for example, type "Flux" into that box and press enter to see only column names that contain "Flux".

.. figure:: /_static/Table_column_selection_DP02.png
    :name: Table_column_selection

Then, press the filter icon to select only those items for analysis, as shown in the next figure.

.. figure:: /_static/Table_column_filter_DP02.png
    :name: Table_column_filter


.. _DP0-2-Portal-Beginner-Step-3:

Select columns constraints
==========================

After you press the filter icon, you should have only those items you selected shown in the "Output Column Selection and Constraints" table.
You may now add your column constaints to the table.
For this example, use the following values, which limi the source fluxes to the range of 30 - 1000 nanojansky: 
``coord_ra`` leave blank, ``coord_dec`` leave blank, ``g_calibFlux`` >20 and < 1000, ``i_calibFlux ``>20 and < 1000, ``r_calibFlux`` >20 and < 1000,

.. ``clean`` = 1, ``dec`` leave blank, ``xtendedness`` = 0, ``good`` = 1, ``mag_g`` <24, ``mag_i`` <24, ``mag_r`` <24, ``magerr_g`` < 0.1, ``magerr_i`` < 0.1, ``magerr_r`` < 0.1, ``ra`` (leave blank).

Then, press the "Search" button as shown in the next figure.

.. figure:: /_static/Search_with_selected_parameters_DP02.png
    :name: Search_with_selected_parameters


.. _DP0-2-Portal-Beginner-Step-4:

Select configure the graph to create a color magnitude diagram
==============================================================

The next figure shows the results of the search.
The gaps in the spatial coverage of the returned catalog objects is due to the limit of 10,000.
The gaps for your search might be different from what is shown below.

.. figure:: /_static/Results_tri_view_DP02.png
    :name: Results_tri_view

Next, click on the double gear icon on the upper right-hand window, as shown in the next figure.

.. figure:: /_static/Select_double_gear_DP02.png
    :name: Select_double_gear

Finally, change the parameters in the selection box.
Set **X** to be ``-1.0857*log(r_calibFlux/3.631e12)+1.0857*log(i_calibFlux/3.631e12)`` and set **Y** to be ``1.0857*log(g_calibFlux/3.631e12)``.
Under **Chart Options**, select "reverse" under the "Y Label".

.. figure:: /_static/Edit_chart_data_DP02.png
    :name: Edit_chart_data

After including any other information such as a "Chart title," "X Label," and "Y Label", hit "Apply."
The plot that you make will be slightly different from what is shown below, and different from the plot in the first of the :ref:`DP0-2-Tutorials-Notebooks` due to random sampling and the 10,000 maximum that we used.

.. figure:: /_static/Final_data_DP02.png
    :name: Final_data
