.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-TOPCAT-Beginner:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#######################################################################
01. API TOPCAT Bright Stars Color-Magnitude Diagram Tutorial (beginner)
#######################################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Douglas Tucker and Leanne Guy

**Last verified to run:** 2023-11-30

**Targeted learning level:** beginner

**Introduction:**
This tutorial uses the TOPCAT Virtual Observatory interface to search for bright stars in a small region of sky and create a color-magnitude diagram.
This is the same demonstration used to illustrate the Table Access Protocol (TAP) service in the first of the :ref:`DP0-2-Tutorials-Notebooks` and to 
illustrate the Portal service in the first of the :ref:`DP0-2-Tutorials-Portal`.
Beginner-level TOPCAT users looking for a more general overview of TOPCAT should refer to the `TOPCAT homepage <https://www.star.bris.ac.uk/~mbt/topcat/>`_.

It should be noted that all the functionality demonstrated in Examples 1, 2, and 3 below -- i.e., all but the interactive 3D plots of Example 4 -- is 
possible via the RSP Portal Aspect (see :doc:`/data-access-analysis-tools/portal-intro`).

.. _DP0-2-TOPCAT-Beginner-Example-1:

Example 1. Run a Simple Query
=============================

**1.1.** Follow the steps in :ref:`Data-Access-Analysis-Tools-TAP-TOPCAT-get-started` for accessing DP0.2 from TOPCAT.
At the end of these steps, there should be 2 TOPCAT windows open -- the main TOCPAT window and a "Table Access Protocol
(TAP) Query window -- like in the following figure.  (Note that the TOPCAT windows or components within the windows
can be resized by clicking and dragging window corners or component edges.)

.. figure:: /_static/API_TOPCAT_DLT_5.png
    :name: API_TOPCAT_DLT_5
    :alt: A screenshot of the Table Access Protocol (TAP) Query window in front of the main TOPCAT window.
          The Table Access Protocol (TAP) Query window shows three panels, stacked vertically.  The
	  top panel is the Metadata panel, and it shows the `dp02_dc2_catalogs.Object` table highlighted
	  in blue within the list of DP0.1 and DP0.2 schemas and tables in the left sub-panel, and a list
	  of names, types, units, index checkboxes, and descriptions for each column of the 
	  `dp02_dc2_catalogs.Object` table in the right sub-panel.
	  The middle panel is the Service Capabilities panel, and it shows that
	  the available Query Language is ADQL-2.0.  The bottom panel is the ADQL Text panel, and it 
	  indicates the current Mode is Synchronous; the bottom panels text box is currently empty.



**1.2.** Insert the following query.

.. code-block:: SQL

	SELECT TOP 10 
		coord_ra, coord_dec, detect_isPrimary, 
		r_calibFlux, r_cModelFlux, r_extendedness 
	FROM dp02_dc2_catalogs.Object
	WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), 
			CIRCLE('ICRS', 62, -37, 0.1)) = 1

into the "ADQL Text" panel of the "Table Access Protocol (TAP) Query" window, and click the "Run Query" button at the bottom of
this window:

.. figure:: /_static/TOPCAT_CMD_tutorial_01.png
    :name: TOPCAT_CMD_tutorial_01.png
    :alt: A screenshot of the Table Access Protocol (TAP) Query window.
	  A list of DP0.2 tables is shown in the top, Metadata panel.
	  A simple ADQL query is shown in the bottom, ADQL Text panel.
	  

Note that this query grabs `coord_ra`, `coord_dec`, `detect_isPrimary`, 
`r_calibFlux`, `r_cModelFlux`, and `r_extendedness` columns from the 
`dp02_dc2_catalogs.Object` table for the first 10 entries found
by the query within a 0.1-degree radius circle centered at
(RA,DEC)=(62,-37), which is near the center of the DP0.2 sky
projection.

**1.3.** TOPCAT will return a table of the results from this short, 
simple query pretty rapidly.  You can find the table highlighted
in the "Table List" panel of the main TOPCAT window:

.. figure:: /_static/TOPCAT_CMD_tutorial_02.png
    :name: TOPCAT_CMD_tutorial_02.png
    :alt: A screenshot of the main TOPCAT window.  It is composed of four main parts.
	  1. A row of icons along the top of the window.  2. A Table List panel on the left
	  of the window; this currently shows one table, called TAP_1_dp02_dc02_catalogs.Object,
	  and it is highlighted.  3. A Current Table Properties panel on the right of the window.
	  4. A small SAMP panel just below the Current Table Properties panel.


**1.4.** If you click on the "Display table cell data" icon -- the 4th icon from the left in the row of icons at the top of the main TOPCAT window 
(it looks like a table with the first row and first column grayed out) -- a TOPCAT Table Browser window like this one will open up:

.. figure:: /_static/TOPCAT_CMD_tutorial_03.png
    :name: TOPCAT_CMD_tutorial_03.png
    :alt: A screenshot of a Table Browser window.  It shows the contents of Table 1, 
	  called TAP_1_dp02_dc02_catalogs.Object.

For this simple query, there are only 10 entries; so you can see the 
whole contents of this table.  For larger tables, vertical and horizontal 
scrollbars appear for you to view other

.. _DP0-2-TOPCAT-Beginner-Example-2:

Example 2. Run a More Detailed Query
====================================

**2.1.** Now let's run a more detailed query.  This query will grab the `coord_ra`, `coord_dec`, 
and the `calibFlux` and `calibFluxErr` columns for the top 10000 entries returned 
from the database for bright (>360 nJy), non-extended (star-like) primary objects
within 1 degree of (RA,DEC)=(62,-37).  Fill the following query:

.. code-block:: SQL

	SELECT TOP 10000
        	coord_ra, coord_dec,
        	u_calibFlux, u_calibFluxErr, 
        	g_calibFlux, g_calibFluxErr, 
        	r_calibFlux, r_calibFluxErr, 
        	i_calibFlux, i_calibFluxErr, 
        	z_calibFlux, z_calibFluxErr, 
        	y_calibFlux, y_calibFluxErr
	FROM dp02_dc2_catalogs.Object
	WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
        	        CIRCLE('ICRS', 62, -37, 1.0)) = 1
		AND detect_isPrimary = 1
		AND u_calibFlux > 360
		AND g_calibFlux > 360
		AND r_calibFlux > 360
		AND i_calibFlux > 360
		AND z_calibFlux > 360
		AND y_calibFlux > 360
		AND u_extendedness = 0
		AND g_extendedness = 0
		AND r_extendedness = 0
		AND i_extendedness = 0
		AND z_extendedness = 0
		AND y_extendedness = 0

into the "ADQL Text" panel of TOPCAT's "Table Access Protocol (TAP) 
query window like so:

.. figure:: /_static/TOPCAT_CMD_tutorial_04.png
    :name: TOPCAT_CMD_tutorial_04.png
    :alt: A screenshot of the Table Access Protocol (TAP) Query window.
	  A list of DP0.2 tables is shown in the top, Metadata panel.
	  An ADQL query is shown in the bottom, ADQL Text panel.

and click on the "Run Query" button at the bottom of the window.

**2.2.** This is a longer query than the previous one.  While the
query is running, this temporary TOPCAT "Load New Table" window 
will pop up:

.. figure:: /_static/TOPCAT_CMD_tutorial_05.png
    :name: TOPCAT_CMD_tutorial_05.png
    :alt: A screenshot of the Load New Table window.
	  It indicates that a new table, called
	  TAP_1_dp02_dc02_catalogs.Object, is being
	  loaded into TOPCAT.

It will close once the query completes.

**2.3.**  Note that, once the query completes, there is a second
table in the "Table List" panel of the main TOPCAT window:

.. figure:: /_static/TOPCAT_CMD_tutorial_06.png
    :name: TOPCAT_CMD_tutorial_06.png
    :alt: A screenshot of the main TOPCAT window.  It is composed of four main parts.
	  1. A row of icons along the top of the window.  2. A Table List panel on the left
	  of the window; this currently shows two tables, called TAP_1_dp02_dc02_catalogs.Object
	  and TAP_1_dp02_dc02_catalogs.Object; the second table is highlighted.
	  3. A Current Table Properties panel on the right of the window.
	  4. A small SAMP panel just below the Current Table Properties panel.

**2.4.**  Like in Step 1.4 for the previous query above, 
If you click on the “Display table cell data” icon – the 
4th icon from the left in the row of icons at the top of 
the main TOPCAT window (it looks like a table with the 
first row and first column grayed out) – a TOPCAT Table 
Browser window like this one will open up:

.. figure:: /_static/TOPCAT_CMD_tutorial_07.png
    :name: TOPCAT_CMD_tutorial_07.png
    :alt: A screenshot of a Table Browser window.  It shows the contents of Table 2, 
	  called TAP_2_dp02_dc02_catalogs.Object.  This is a large table, and there
	  are both horizontal and vertical scrollbars to permit the use to scroll
	  to other parts of the table.

**2.5.**  Next, click on the "Display column metadata" 
icon -- the 6th icon from the left in the row of icons 
at the top of the main TOPCAT window (it looks like a 
table with the first row highlighted in blue).:

.. figure:: /_static/TOPCAT_CMD_tutorial_08.png
    :name: TOPCAT_CMD_tutorial_08.png
    :alt: A screenshot of the main TOPCAT window.  It is composed of four main parts.
	  1. A row of icons along the top of the window.  2. A Table List panel on the left
	  of the window; this currently shows two tables, called TAP_1_dp02_dc02_catalogs.Object
	  and TAP_1_dp02_dc02_catalogs.Object; the second table is highlighted.
	  3. A Current Table Properties panel on the right of the window.
	  4. A small SAMP panel just below the Current Table Properties panel.


Clicking on that icon will open up a Table Columns 
window like this:

.. figure:: /_static/TOPCAT_CMD_tutorial_09.png
    :name: TOPCAT_CMD_tutorial_09.png
    :alt: A screenshot of the Table Columns window.
	  It lists the name the class, the datatype, and, 
	  if available, the units and description 
	  of each of the columns in the table.

Note that each column is listed, along with various
information about that column -- e.g., its name, the   
class and datatype of its contents, its units (if any), 
and its description (if any).

**2.6.**  Let's create some columns of our own.  
Let's start by creating a column for the u-band
AB magnitude of the objects in this table.  To 
add a column, click on the big green plus ("+")
sign that is the left-most icon in the top row of
the Table Columns window from the previous step.
This will open a "Define Synthetic Column" window.

Note that the fluxes returned by our ADQL query 
are in nanojanskys; they can be converted to AB magnitudes 
via the equation, "m(AB) = -2.5*log10(flux [nanojanskys]) + 31.4".
Explicitly, for u-band, one can create a `u_calibMag`
column by filling in the following in the "Define
Synthetic Column" window like so:

.. figure:: /_static/TOPCAT_CMD_tutorial_10.png
    :name: TOPCAT_CMD_tutorial_10.png
    :alt: A screenshot of the Define Synthetic Column window.
	  Shown are the user-input values for the name and
	  the expression for the column.  In this particular
	  case, the name is u_calibMag and the expression
	  is the equation for converting flux in nano-janskys
          to AB magnitudes, where the flux is u_calibFlux.

and clicking the "OK" button.

(**Notice:** The `AB Magnitudes Wikipedia <https://en.wikipedia.org/wiki/AB_magnitude>`_ page 
provides a concise resource for users who are unfamiliar with AB magnitudes and fluxes in 
units of janskys.)

**2.7.**  Let us also calculate the error in the u-band magnitude.
Recall that magnitudes are are logarithmic quantities.  For relatively
small errors (less than about 10%) one can perform the propagation-of-
errors analysis to find sigma(mag) = (2.5/ln(10.)) * (sigma(flux)/flux), 
which can be approximated as sigma(mag) = 1.086*(sigma(flux)/flux).  
Let's use this equation to add a `u_calibMagErr` column by filling in 
the following in the "Define Synthetic Column" window like so:

.. figure:: /_static/TOPCAT_CMD_tutorial_11.png
    :name: TOPCAT_CMD_tutorial_11.png
    :alt: A screenshot of the Define Synthetic Column window.
	  Shown are the user-input values for the name and
	  the expression for the column.  In this particular
	  case, the name is u_calibMagErr and the expression
	  is the equation for converting flux and error in the
	  flux to error in magnitude.  

and clicking the "OK" button.

Each time you add a column, the column will appear in the "Table Columns"
window:

.. figure:: /_static/TOPCAT_CMD_tutorial_12.png
    :name: TOPCAT_CMD_tutorial_12.png
    :alt: A screenshot of the Table Columns window.
	  It lists the name the class, the datatype, and, 
	  if available, the units and description 
	  of each of the columns in the table.  Here,
	  it lists the original columns for Table 2
	  plus the two new u-band columns just added, 
          u_calibMag and u_calibMagErr, and the expressions
	  used to derive them.


**2.8.**  Repeat Steps 2.6 and 2.7 for the other filter bands 
(g,r,i,z,y).  After doing so, you will see entries for all of these
new columns in the Table Columns window, like this (where the new 
columns have been highlighted in blue):

.. figure:: /_static/TOPCAT_CMD_tutorial_13.png
    :name: TOPCAT_CMD_tutorial_13.png
    :alt:  A screenshot of the Table Columns window.
	  It lists the name the class, the datatype, and, 
	  if available, the units and description 
	  of each of the columns in the table.  Here,
	  it lists the original columns for Table 2
	  plus the twelve new u-band columns just added, 
          the calibrated magnitudes and magnitude errors
	  for the 6 LSST filter passbands, as well as 
	  the expressions used to derive these newly derived 
	  quantities.


**2.9.**  You will also see values for the new columns tabulated 
within the Table Browser (click on the "Display table cell data" 
icon in the main TOPCAT window as in Step 2.4 above):

.. figure:: /_static/TOPCAT_CMD_tutorial_14.png
    :name: TOPCAT_CMD_tutorial_14.png
    :alt: A screenshot of a Table Browser window.  It shows the contents of Table 2, 
	  called TAP_2_dp02_dc02_catalogs.Object, including the quantities just derived.  
	  This is a large table, and there are both horizontal and vertical scrollbars 
	  to permit the use to scroll to other parts of the table.


**2.10.**  As a brief aside, let's create a skyplot of the 
RA,DEC postions of the stars returned by the query.  To do
so, go back to the main TOPCAT window and click on the "Sky
plotting window" icon -- the 11th icon from the left in the
row of icons at the top of the main TOPCAT window (it looks
like a small, gridded Aitoff map projection): 
:

.. figure:: /_static/TOPCAT_CMD_tutorial_15.png
    :name: TOPCAT_CMD_tutorial_15.png
    :alt: A screenshot of the main TOPCAT window.  It is composed of four main parts.
	  1. A row of icons along the top of the window.  2. A Table List panel on the left
	  of the window; this currently shows two tables, called TAP_1_dp02_dc02_catalogs.Object
	  and TAP_1_dp02_dc02_catalogs.Object; the second table is highlighted.
	  3. A Current Table Properties panel on the right of the window.
	  4. A small SAMP panel just below the Current Table Properties panel.


TOPCAT will return with a Sky Plot window.  TOPCAT is 
generally pretty good at identifying which columns in 
a table represent (RA, DEC) coordinates, and it succeeds
in this case, plotting `coord_ra` and `coord_dec` as the 
RA and the DEC, respectively:

.. figure:: /_static/TOPCAT_CMD_tutorial_16.png
    :name: TOPCAT_CMD_tutorial_16.png
    :alt: A screenshot of the Sky Plot window.
	  It shows the RA, DEC positions of the 10000
          objects from Table 2.  Due to the details of
	  the ADQL query used to generate Table 2, all
	  the points lie within a circle of diameter 
	  1 degree.  Aside from the main plot panel, 
	  there are two other panels in the Sky Plot
	  window.  1.  A small panel in the lower right
	  with icons for Frame, Legend, Axes, STILTS, 
	  plus the name of the table from which the 
	  plotted data were taken.  2. A panel indicating
	  the table name, the Data Sky System, and the 
	  columns to be used for the longitude (RA) and
	  latitude (DEC).

Note that TOPCAT automatically adjusts to an appropriate
RA, DEC range, but you can zoom in and out interactively
via your mouse or scroll wheel.  Also note that TOPCAT plots
the grid by default in sexagesimal units, but these (and
other aspects of the plot) can be modified using the Axes
button in the lower left panel of the Sky Plot window.
For more information, please consult the 
`TOPCAT documentation <http://www.star.bris.ac.uk/~mbt/topcat/>`_.

**2.11.**  Now let us return to the main goal of this tutorial --
creating a color-magnitude for the 10000 bright point sources
(mostly stars) returned by our ADQL query.  To do
so, go back to the main TOPCAT window and click on the "Plane 
plotting window" icon -- the 11th icon from the left in the
row of icons at the top of the main TOPCAT window (it looks
like a blank X/Y plot, and it sits just leftward of the
"Sky plotting window" icon):

.. figure:: /_static/TOPCAT_CMD_tutorial_17.png
    :name: TOPCAT_CMD_tutorial_17.png
    :alt: A screenshot of the main TOPCAT window.  It is composed of four main parts.
	  1. A row of icons along the top of the window.  2. A Table List panel on the left
	  of the window; this currently shows two tables, called TAP_1_dp02_dc02_catalogs.Object
	  and TAP_1_dp02_dc02_catalogs.Object; the second table is highlighted.
	  3. A Current Table Properties panel on the right of the window.
	  4. A small SAMP panel just below the Current Table Properties panel.


TOPCAT will return with a Plane Plot window, initially
plotting the first 2 numerical columns from the table.
In this case, these two columns are `coord_ra` and `coord_dec`;
so this plot looks very similar to the sky plot you just generated:

.. figure:: /_static/TOPCAT_CMD_tutorial_18.png
    :name: TOPCAT_CMD_tutorial_18.png
    :alt: A screenshot of the Plane Plot window.
	  It shows the RA, DEC positions of the 10000
          objects from Table 2.  Due to the details of
	  the ADQL query used to generate Table 2, all
	  the points lie within a circle of diameter 
	  1 degree.  Aside from the main plot panel, 
	  there are two other panels in the Plane Plot
	  window.  1.  A small panel in the lower right
	  with icons for Frame, Legend, Axes, STILTS, 
	  plus the name of the table from which the 
	  plotted data were taken.  2. A panel indicating
	  the table name and the columns to be used for 
	  the X (RA) and Y (DEC) coordinates.

**2.12.**  First, let's replace `coord_ra` and `coord_dec` 
with `r_calibMag - i_calibMag` and `g_calibMag` in the 
`X` and `Y` windows, respectively, as shown here:

.. figure:: /_static/TOPCAT_CMD_tutorial_19.png
    :name: TOPCAT_CMD_tutorial_19.png
    :alt: A screenshot of the Plane Plot window. 
	  The chart shows a color magnitude diagram, g-band AB magnitude vs r-band minus i-band color, for the objects in Table 2. 
	  This example demonstrates how to quickly explore the data returned in the search query. 
	  The plot shows a large density of stars at low r-i color, and discrete bins at redder r-i color because the simulated data are  
	  based on discrete red stellar models that were used as input into DP0.2. Real data are expected to instead show a smooth distribution of colors.


This is good!  Plotted is the `g_calibMag` vs. 
`r_calibMag - i_calibMag` color magnitude diagram
for this set of stars (and star-like objects).  (The 
"quantized" colors for objects with `r_calibMag - i_calibMag > 0.6`
is an artifact of the simulation upon which DP0.2 is based.)

**2.13.**  That said, astronomers usually prefer to plot
their color-magnitude diagrams with brighter (lower magnitude) 
objects at the top of the plot and fainter (higher magnitude) 
objects at the bottom.  You can adjust your plot to follow 
this convention by clicking on the `Axes` button in the lower-left
panel of the "Plane Plot" window and flipping the `Y` axis as 
follows:

.. figure:: /_static/TOPCAT_CMD_tutorial_20.png
    :name: TOPCAT_CMD_tutorial_20.png
    :alt: A screenshot of the Plane Plot window. 
	  The chart shows a color magnitude diagram, g-band AB magnitude vs r-band minus i-band color, for the objects in Table 2. 
	  In this rendition, the Y-axis has been flipped; so that bright stars (with small magnitudes) are near the top of the plot 
	  and faint stars (with large magnitudes) are near the bottom.
	  This example demonstrates how to quickly explore the data returned in the search query. 
	  The plot shows a large density of stars at low r-i color, and discrete bins at redder r-i color because the simulated data are  
	  based on discrete red stellar models that were used as input into DP0.2. Real data are expected to instead show a smooth distribution of colors.


**2.14.**  Finally, to guide the eye, you might wish to add a 
grid to the plot.  To do so, click on the `Grid` button 
at the top of the bottom-right panel of the "Plane Plot" 
window and check the "Draw Grid" option like so:

.. figure:: /_static/TOPCAT_CMD_tutorial_21.png
    :name: TOPCAT_CMD_tutorial_21.png
    :alt: A screenshot of the Plane Plot window. 
	  The chart shows a color magnitude diagram, g-band AB magnitude vs r-band minus i-band color, for the objects in Table 2. 
	  In this rendition, the Y-axis has been flipped; so that bright stars (with small magnitudes) are near the top of the plot 
	  and faint stars (with large magnitudes) are near the bottom.  In addition, a grid has been added to the plot.
	  This example demonstrates how to quickly explore the data returned in the search query. 
	  The plot shows a large density of stars at low r-i color, and discrete bins at redder r-i color because the simulated data are  
	  based on discrete red stellar models that were used as input into DP0.2. Real data are expected to instead show a smooth distribution of colors.



TOPCAT has many options for modifying your plots --
substantially more than can be adequately described in a short
tutorial like this -- so it is again recommended that the interested
user consult the `TOPCAT documentation <http://www.star.bris.ac.uk/~mbt/topcat/>`_.


Example 3. Interact with Multiple Plots/Tables
==============================================

Another strength of TOPCAT is that the data from a given 
table are linked across the plots based on that table.
For instance, let's look at plots from the table returned
from the Example 2 ADQL query above.  You already have two 
plots from this table -- a Sky Plot showing the RA,DEC
positions of the 10000 entries contained within that table, 
and a Plane Plot showing the `g_calibMag` vs. 
`r_calibMag - i_calibMag` color magnitude diagram for 
these same 10000 entries.  Let's also add a third plot --
a Plane Plot of `g_calibMagErr` vs `g_calibMag` for those
10000 objects.   

**3.1.**  As in Step 2.11 above, click on the "Plane 
plotting window" icon in the main TOPCAT window.:

.. figure:: /_static/TOPCAT_CMD_tutorial_22.png
    :name: TOPCAT_CMD_tutorial_22.png
    :alt: A screenshot of the main TOPCAT window.  It is composed of four main parts.
	  1. A row of icons along the top of the window.  2. A Table List panel on the left
	  of the window; this currently shows two tables, called TAP_1_dp02_dc02_catalogs.Object
	  and TAP_1_dp02_dc02_catalogs.Object; the second table is highlighted.
	  3. A Current Table Properties panel on the right of the window.
	  4. A small SAMP panel just below the Current Table Properties panel.

Then replace the column names in the `X` and `Y` windows
in the lower-right panel of the "Plane Plot" window with
`g_calibMag` and `g_calibMagErr, respectively.  If you want,
you can also also add a grid to the plot (as described in 
Step 2.14 above):

.. figure:: /_static/TOPCAT_CMD_tutorial_23.png
    :name: TOPCAT_CMD_tutorial_23.png
    :alt: A screenshot of the Plane Plot window. 
	  Plotted are the g-band AB magnitude error
	  versus the g-band AB magnitude.  The g-band
	  AB magnitude ranges from about 16 to 25.
          The g-band AB magnitude starts out near zero
          but starts to increase exponentially around
	  22th magnitude, reaching 0.10 around 25th 
	  magnitude.

**3.2.** Finally, let's look at all 3 plots together --
the one "Sky Plot" and the 2 "Plane Plots" -- plus the "Table
Browser" from Step 2.9.  Using the mouse, you can adjust the
size of these windows so they all can be viewed simultaneously.
Now either click on a symbol in one of the plots.  (In the following
plot, a point near `r_calibMag-i_calibMag=1.0`, `g_calibMag=24.2` was clicked 
in the color-magnitude plot.)  A small black circle with cross-hairs will appear
around that particular symbol in that particular plot.  **What's more, 
a small black circle with cross-hairs will also appear around the symbol 
for that particular object in the other plots.  Its row entry in the
the "Table Browser" will also be highlighted.**:

.. figure:: /_static/TOPCAT_CMD_tutorial_24.png
    :name: TOPCAT_CMD_tutorial_24.png
    :alt: A screen shot showing a Sky Plot window and two 
	  Plane Plot windows -- one of the color-magnitude
	  diagram and another of the g-band magnitude error
	  versus magnitude plot.  Also shown is a Table 
	  Browser window.  All of these are for the data
	  in Table 2.  In the color-magnitude plot, a symbol
	  is marked by a black circle with cross-hairs.
	  There is also a symbol marked by a black circle with
	  cross-hairs in the other two plots.  These are all
	  for the same object from Table 2.  Note also that
	  there is a row highlighted in the Table Browser.
          This is the row for that same object marked by 
	  the black circle with cross-hairs in the 3 plots.
	  

This data linkage works not only for single objects but for
subsets of points that one can define for the table via the
TOPCAT interface.  The interested user is again directed to 
the `TOPCAT documentation <http://www.star.bris.ac.uk/~mbt/topcat/>`_.


Example 4. Create Interactive 3D Plots
======================================

As the final example in this tutorial, let's look at the 
TOPCAT's interactive 3D plot functionality.  For continuity,
let us make use of the data set already downloaded in Example 2
and used in both Examples 2 and 3.

**4.1.**  First, return to the main TOPCAT window and click 
on the  "3D plotting window using Cartesian coordinates" icon --
it is the 13th icon from the left in the top row of the 
TOPCAT window, and it looks like a 2D rendering of a cube:

.. figure:: /_static/TOPCAT_CMD_tutorial_25.png
    :name: TOPCAT_CMD_tutorial_25.png
    :alt: A screenshot of the main TOPCAT window.  It is composed of four main parts.
	  1. A row of icons along the top of the window.  2. A Table List panel on the left
	  of the window; this currently shows two tables, called TAP_1_dp02_dc02_catalogs.Object
	  and TAP_1_dp02_dc02_catalogs.Object; the second table is highlighted.
	  3. A Current Table Properties panel on the right of the window.
	  4. A small SAMP panel just below the Current Table Properties panel.

Upon clicking that icon, TOPCAT will open a "Cube Plot" 
windown, automatically using the first 3 numeric columns
of the table -- in this case, `coord_ra`, `coord_dec`, and 
`u_calibFlux` for the inputs to the `X`, 'Y`, and `Z` 
coordinates, respectively:

.. figure:: /_static/TOPCAT_CMD_tutorial_26.png
    :name: TOPCAT_CMD_tutorial_26.png
    :alt: A screen shot of a Cube Plot.  Shown is a 2D 
	  rendering of a 3D cube.  Plotted are RA and DEC
	  for the X and Y axes, respectively, and the 
	  u-band flux for the Z axis.

**4.2.**  Next, replace the contents of the `X`, 'Y', 
and 'Z' windows in the lower-right panel of the "Cube
Plot" window with `r_calibMag-i_calibMag`, 
`g_calibMag-r_calibMag`, and `u_calibMag-g_calibMag`,
respectively, as follows:

.. figure:: /_static/TOPCAT_CMD_tutorial_27.png
    :name: TOPCAT_CMD_tutorial_27.png
    :alt: A screen shot of a Cube Plot.  Shown is a 2D 
	  rendering of a 3D cube.  Plotted are the AB
	  colors r-i, g-r, and u-g along the X, Y, and
	  Z axes, respectively.  The stellar locus is 
	  almost one-dimenstional, and it 
	  snakes from one corner of the cube to the opposite
	  corner of the cube.  The disceteness of the locus
	  for the red stars is also noticeable here.

Now you have a 3D color-color-color diagram for the
10000 stars (and other point sources) 
downloaded in Example 2.

**4.3.**  You can add more information to this plot
by color-coding the individual symbols.  To do this,
click on the "Form" button in the lower-right panel
of the "Cube Plot" window; then, in the "Shading" 
subpanel that appears, choose "aux" in the "Mode"
down-down menue and insert `i_calbMag` in the 
"Aux" window, like so:

.. figure:: /_static/TOPCAT_CMD_tutorial_28.png
    :name: TOPCAT_CMD_tutorial_28.png
    :alt: A screen shot of a Cube Plot.  Shown is a 2D 
	  rendering of a 3D cube.  Plotted are the AB
	  colors r-i, g-r, and u-g along the X, Y, and
	  Z axes, respectively.  The stellar locus is 
	  almost one-dimenstional, and it 
	  snakes from one corner of the cube to the opposite
	  corner of the cube.  The symbols are color-coded
          using the Inferno palette to show i-band magnitude, 
	  with the brighter objects appearing lighter and
          yellower, and the fainter objects appearing 
          darker and browner.  At the blue corner of 
	  the cube, a large fraction of objects appear 
          to be relatively faint (i-band AB magnitude 
          fainter than about 22nd magnitude).

As you see, the result is a 3D color-color-color
plot with the value of `i_calibMag` encoded in 
the color of each symbol.  A color bar also 
appears; by default, it uses the "Inferno"
color look-up table.

**4.4.**  What if you wish to use a different
color look-up table for your auxiliary axis?
In that case, click on "Aux Axis" in the 
left-lower panel of the Cube Plot window.  In 
the new lower-right panel panel that appears, 
choose a different color paletter from the
"Aux Shader" drop-down menu.  In the following
case, the "Rainbow" color palette was chosen:

.. figure:: /_static/TOPCAT_CMD_tutorial_29.png
    :name: TOPCAT_CMD_tutorial_29.png
    :alt: A screen shot of a Cube Plot.  Shown is a 2D 
	  rendering of a 3D cube.  Plotted are the AB
	  colors r-i, g-r, and u-g along the X, Y, and
	  Z axes, respectively.  The stellar locus is 
	  almost one-dimenstional, and it 
	  snakes from one corner of the cube to the opposite
	  corner of the cube.  The symbols are color-coded
          using the Rainbow palette to show i-band magnitude, 
	  with the brighter object symbols appearing red, 
          and the fainter object symbols appearing 
          blue, purple, or even black.  

**4.5.**  Finally, TOPCAT *is* interactive.  If 
you haven't done so already, use your mouse to 
"click-and-drag" a point in the plot window to
rotate the plot to a different configuration; e.g.:

.. figure:: /_static/TOPCAT_CMD_tutorial_30.png
    :name: TOPCAT_CMD_tutorial_30.png
    :alt: A screen shot of a Cube Plot.  Shown is a 2D 
	  rendering of a 3D cube.  Plotted are the AB
	  colors r-i, g-r, and u-g along the X, Y, and
	  Z axes, respectively.  The stellar locus is 
	  almost one-dimenstional, and it 
	  snakes from one corner of the cube to the opposite
	  corner of the cube.  The symbols are color-coded
          using the Rainbow palette to show i-band magnitude, 
	  with the brighter object symbols appearing red, 
          and the fainter object symbols appearing 
          blue, purple, or even black.  The plot has
          been rotated arbitrarily relative to the 
          rotation of the previous plot.

As with the 2D plots, you can also zoom in or
out using the mouse or a scroll wheel.

To conclude, TOPCAT is a very powerful interactive
graphical tool with many useful features.  The 
interested user is encouraged to explore more
by consulting the 
`TOPCAT documentation <http://www.star.bris.ac.uk/~mbt/topcat/>`_.
