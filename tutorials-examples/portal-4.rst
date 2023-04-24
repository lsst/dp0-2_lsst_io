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

############################################
04. Plotting Histograms in the Portal Aspect
############################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Greg Madejski

**Last verified to run:** 2023-04-21

**Targeted learning level:** beginner

**Introduction:**
This brief tutorial will illustrate how to use the histogram function in the Portal aspect of the Rubin Science Platform.  It will consist of three parts.  One ("A") will request all observations of a given location on the sky, and will provide a histogram of the number of visits as a function of time throughout the entire time span covered in the DP0.2 data set. This might be particularly valuable for studies of variability of celestial sources, for instance the measurement of a power density spectrum, used in determining periodograms of their fluxes.  This is because the density of visits affects the window function which must be accounted for in developing a power density spectrum.  

The second ("B") will return the histogram of logarithm of fluxes of objects in a selected region of the sky.  Here, one science case might be the contribution of discrete sources (for instance those studied at a limited-size patch of the sky at high sensitivity and high spatial resolution) to background radiation from unresolved sources determined over a large area of the sky but at a lower angular resolution, which then might appear as a diffuse emission.  

The third ("C") part will illustrate how to generate a histogram of two variables.  Such two-dimentional histograms are sometimes called "heat maps."  The third dimension, representing the frequency of occurence for a specific pair of variables, is displayed via greyscale or color.  Here, we will illustrate the frequency of occurence of objects as a function of two colors.  In this example, we will use the colors represented by a difference between g and r band magnitudes (x axis) vs. difference between u and g magnitudes (y axis) in a specified region of the sky.  One use case might be to select different classes of galaxies based on their colors.  

.. _DP0-2-Portal-Histogram-Part-A:

Part A:  Generate a histogram illustrating the frequency of visits to a specific location 
=========================================================================================

.. _DP0-2-Portal-Histogram-Step-A1:

Step A1.  Enter the parameters of the query
===========================================

A1.1.  Log into the Portal Aspect

A1.2.  Once you've logged in, you should be (by default) in the query type "Single Table (UI assisted)."  Change this to "Image Search (ObsTAP)" - the third button.  

A1.3. In the "Constraints" section, select the "Calibration Level" as "2" - this is for single-epoch images (Processed Visit Images, or PVIs).  You should be (by default) in the "Image" part of the Data Product Type list - if not, that's what you need to select.  

A1.4.  For "Location" constraint, you need to select the query "Observation boundary contains point" (should be the default).  You can select any location which is within the DP0.2 sky area, say 62.0, -37.0 .  In the large table on the right, you should leave the "Output Column Selection and Constraints" as was defaulted by the Portal aspect.  

A1.5 Next, click on the "Search" button on the bottom left.  

.. figure:: /_static/portal_tut04_step01.png
	:name: portal_tut04_step01

.. _DP0-2-Portal-Histogram-Step-A2:

Step A2.  Images of the location on the sky
===========================================

A2.1.  This search will result in a number of rows in a table at the bottom of the window - you should see about 500 entries, each corresponding to a visit containing the location selected by you.  The upper left-hand window will display a rendered image of a single (4k x 4k) detector, which is the unit of "data delivery."  The upper right-hand window will show a scatter plot of the central locations of Rubin pointings on the sky which contain the data from the location selected by you (62.0, -37.0).  

A2.2.  Now you can examine images corresponding to those pointings by hovering with your computer mouse over the blue dots on the upper right-hand panel.  Once you click on any of the dots - this will highlight a row on the table on the bottom, and will render an image corresponding to the selected pointing.  Conversely, you can select a row in the table at the bottom - this will turn the location of the point on the upper left-hand plot to orange.  

A2.3.  The table contains a large amount of information.  For the purpose of this exercise, the most interesting are the "lsst_band" - this is a filter used for the given pointing.  The "lsst_detector" is telling you which detector contains that data point (ranging from 1 to 189), and "t_min" is the start time (in MJD) of the pointing.  

.. figure:: /_static/portal_tut04_step02.png
	:name: portal_tut04_step02


.. _DP0-2-Portal-Histogram-Step-A3:

Step A3.  Generating a histogram of start times of visits at the selected location
==================================================================================

A3.1.  To generate such a histogram, click on the "Add Chart" button on the top of your window.  

.. figure:: /_static/portal_tut04_step03.png
	:name: portal_tut04_step03

A new window will appear asking for the plot type.  Select "Histogram" here.  For the "Column or expression" select "t_min."  You can select any number of bins in the histogram - say, 100.  You will be given the full range of t_min times (Min and Max) in your table - which you can override.  Clicking "OK" will generate a new panel with a plot of history of Rubin observations at location (62.0, -37.0).  As you can see on the plot below, there is a clear seasonal pattern of the Rubin Observatory visits to your selected location.  You can augment the plot with a title and labels for axis by clicking the "Chart Options" as below.   

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

B3.1.  To generate such a histogram - as you did in part A - click on the "Add Chart" buttom on the top of your window.  In the window which just apeared, select "Histogram."  For the "Column or expression" enter "log10(g_calibFlux).

.. figure:: /_static/portal_tut04_step07.png
	:name: portal_tut04_step07
	
This will result in the plot on the upper right panel on the screenshot below.  If you wish you can add a chart with the same settings as the previous one, but with log axis for the number, select "log" for the Chart Options of the plot (as is in the left panel).  Such plot is often called "log(N) - log (S)."  

.. figure:: /_static/portal_tut04_step08.png
	:name: portal_tut04_step08

.. _DP0-2-Portal-Histogram-Part-C:  

Part C:  Generate a two-dimensional color - color histogram ("heat map") of extended sources
============================================================================================

.. _DP0-2-Portal-Histogram-Step-C1:

Step C1.  Enter the parameters of the query
===========================================

C1.1.  Here, we will use a somewhat more complex query than in parts A and B.  But for starters, as we did in the previous parts, in the "Select Query Type" select the "Single Table (UI assisted)."  In the "Select Table" field, for the "Table Collection" select "dp02_dc2_catalogs" and for the "Table" select "dp02_dc2_catalogs.Object."  In the field "Enter Constraints" select "Spatial" with "Longitude Column" to be "coord_ra" and "Lattitude Column" to be "coord_dec."  For coordinates - you can enter any location that is within the DP0.2 footprint, say 62.0, -37.0.  


.. _DP0-2-Portal-Histogram-Step-C2

Step C2.  Enter the search constraints 
======================================

C2.1.  For this part, we will need a larger number of objects, which will make the distribution of object colors more clear.  To this end, restrict the  radius to 1 degree by entering this into the "Spatial Constraints" box.  As you did before, select only bright-ish objects:  in the "Output Column Selection and Constraints" for the g_calibFlux, i_calibFlux, u_calibFlux, and r_calibFlux rows, enter >360 as the constraints.  

C2.2.  This time, add two additional constraints:  enter =1 for detect_isPrimary row (to exclude blended objects), and enter =1 for the g_extendedness row.  Such constraints presumably will favor un-blended extended objects such as individual galaxies.  You can un-click the box under the little funnel (filter icon) for the "detect_isPrimary" and "g_extendedness" rows since you only need to select on those parameters and don't need to have them returned in the output table.   Clicking "Search" as below will take about a minute, and will return a table of ~ 160000 objects.  

.. figure:: /_static/portal_tut04_step09.png
	:name: portal_tut04_step09


.. _DP0-2-Portal-Histogram-Step-C3:

Step C3.  Plot the 2-dimensional color histogram
================================================

C3.1.  Click on the two gears on the upper right-hand side of the screen, to set the plot parameters.  
For X, enter "-2.5 * log10(u_calibFux) - (-2.5 * log10(g_calibFux))" and for Y, enter "-2.5 * log10(g_calibFux) - (-2.5 * log10(r_calibFux))" - this will convert fluxes to magnitudes (and their differences) in the selected bands.  You can enter any color scale - whichever you find most compelling.  In the "Chart Options" part you can enter the chart title and axis labels.  Click "Apply" and then "Close."  

.. figure:: /_static/portal_tut04_step10.png
	:name: portal_tut04_step10

C3.2.  The resulting color-color diagram of objects in your search area will look as below.  

.. figure:: /_static/portal_tut04_step11.png
	:name: portal_tut04_step11


Beginner-level users looking for a more general overview of the Portal Aspect should refer to this :doc:`/data-access-analysis-tools/portal-intro`.


