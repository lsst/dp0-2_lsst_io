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

#######################################################################
01. API TOPCAT Bright Stars Color-Magnitude Diagram Tutorial (beginner)
#######################################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Douglas Tucker and Leanne Guy

**Last verified to run:** 2023-11-13

**Targeted learning level:** beginner

**Introduction:**
This tutorial uses the TOPCAT Virtual Observatory interface to search for bright stars in a small region of sky and create a color-magnitude diagram.
This is the same demonstration used to illustrate the Table Access Protocol (TAP) service in the first of the :ref:`DP0-2-Tutorials-Notebooks` and to 
illustrate the Portal service in the first of the :ref:`DP0-2-Tutorials-Portal`.
Beginner-level TOPCAT users looking for a more general overview of TOPCAT should refer to the `TOPCAT homepage <https://www.star.bris.ac.uk/~mbt/topcat/>`_.

.. _DP0-2-TOPCAT-Beginner-Step-1:

Step 1. Run a Simple Query
==========================

**1.1.** Follow the steps in :ref:`Data-Access-Analysis-Tools-TAP-TOPCAT-Step-by-Step` for accessing DP0.2 from TOPCAT.
At the end of these steps, you should have 2 TOPCAT windows open -- the main TOCPAT window and a "Table Access Protocol
(TAP) Query window -- like the following:

.. figure:: /_static/API_TOPCAT_DLT_5.png
    :name: API_TOPCAT_DLT_5
    :alt: TBD

Note that you can use your mouse to change the size of the TOPCAT windows as well as the size the panels within those windows.

**1.2.** Insert the following query: 

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
    :alt: TBD

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
    :alt: TBD

**1.4.** If you click on the "Display table cell data" icon -- the 4th icon from the left in the row of icons at the top of the main TOPCAT window 
(it looks like a table with the first row and first column grayed out) -- a TOPCAT Table Browser window like this one will open up:

.. figure:: /_static/TOPCAT_CMD_tutorial_03.png
    :name: TOPCAT_CMD_tutorial_03.png
    :alt: TBD

For this simple query, there are only 10 entries; so you can see the 
whole contents of this table.  For larger tables, vertical and horizontal 
scrollbars appear for you to view other

.. _DP0-2-TOPCAT-Beginner-Step-2:

Step 2. Run a More Detailed Query
=================================

**2.1.** Now let's run a more detailed query.  This query will grab the `coord_ra`, `coord_dec`, 
and the `calibFlux` and `calibFluxErr` columns for the top 10000 entried returned 
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
    :alt: TBD

and click on the "Run Query" button at the bottom of the window.

**2.2.** This is a longer query than the previous one.  While the
query is running, this temporary TOPCAT "Load New Table" window 
will pop up:

.. figure:: /_static/TOPCAT_CMD_tutorial_05.png
    :name: TOPCAT_CMD_tutorial_05.png
    :alt: TBD

It will close once the query completes.

**2.3.**  Note that, once the query completes, there is a second
table in the "Table List" panel of the main TOPCAT window:

.. figure:: /_static/TOPCAT_CMD_tutorial_06.png
    :name: TOPCAT_CMD_tutorial_06.png
    :alt: TBD


**2.4.**  Like in Step 1.4 for the previous query above, 
If you click on the “Display table cell data” icon – the 
4th icon from the left in the row of icons at the top of 
the main TOPCAT window (it looks like a table with the 
first row and first column grayed out) – a TOPCAT Table 
Browser window like this one will open up:

.. figure:: /_static/TOPCAT_CMD_tutorial_07.png
    :name: TOPCAT_CMD_tutorial_07.png
    :alt: TBD

**2.5.**  Next, click on the "Display column metadata" 
icon -- the 6th icon from the left in the row of icons 
at the top of the main TOPCAT window (it looks like a 
table with the first row highlighted in blue).:

.. figure:: /_static/TOPCAT_CMD_tutorial_08.png
    :name: TOPCAT_CMD_tutorial_08.png
    :alt: TBD

Clicking on that icon will open up a Table Columns 
window like this:

.. figure:: /_static/TOPCAT_CMD_tutorial_09.png
    :name: TOPCAT_CMD_tutorial_09.png
    :alt: TBD

Note that each column is listed, along with various
information about that column -- e.g., its name, the   
class and datatype of its contents, its units (if any), 
and its description (if any).

**2.6.**  Let's create some columns of our own.  
Let's start by creating a column for the u-band
AB magnitude of the objects in this table.  To 
add a column, we click on the big green plus ("+")
sign that is the left-most icon in the top row of
the Table Columns window from the previous step.
This will open a "Define Synthetic Column" window.

We note that the fluxes returned by our ADQL query 
are in nanojanskys; we can convert them to AB magnitudes 
via the equation, "m(AB) = -2.5*log10(flux [nanojanskys]) + 31.4".
Explicitly, for u-band, we can create a `u_calibMag`
column by filling in the following in the "Define
Synthetic Column" window like so:

.. figure:: /_static/TOPCAT_CMD_tutorial_10.png
    :name: TOPCAT_CMD_tutorial_10.png
    :alt: TBD

and clicking the "OK" button.

(**Notice:** The `AB Magnitudes Wikipedia <https://en.wikipedia.org/wiki/AB_magnitude>`_ page 
provides a concise resource for users who are unfamiliar with AB magnitudes and fluxes in 
units of janskys.)

**2.7.**  Let us also calculate the error in the u-band magnitude.
Recall that magnitudes are are logarithmic quantities.  For relatively
small errors (less than about 10%) one can perform the propagation-of-
errors analysis to find sigma(mag) = (2.5/ln(10.)) * (sigma(flux)/flux), 
or approximately igma(mag) = 1.086*(sigma(flux)/flux).  Let's use this
equation to add a `u_calibMagErr` column by filling in the following
in the "Define Synthetic Column" window like so:

.. figure:: /_static/TOPCAT_CMD_tutorial_11.png
    :name: TOPCAT_CMD_tutorial_11.png
    :alt: TBD

and clicking the "OK" button.

Each time you add a column, the column will appear in the "Table Columns"
window:

.. figure:: /_static/TOPCAT_CMD_tutorial_12.png
    :name: TOPCAT_CMD_tutorial_12.png
    :alt: TBD


**2.8.**  Repeat Steps 2.6 and 2.7 for the other filter bands 
(g,r,i,z,y).  After doing so, you will see entries for all of these
new columns in the Table Columns window, like this (where we have
highlighted the new columns in blue):

.. figure:: /_static/TOPCAT_CMD_tutorial_13.png
    :name: TOPCAT_CMD_tutorial_13.png
    :alt: TBD


**2.9.**  You will also see values for the new columns tabulated 
within the Table Browser (click on the "Display table cell data" 
icon in the main TOPCAT window as in Step 2.4 above):

.. figure:: /_static/TOPCAT_CMD_tutorial_14.png
    :name: TOPCAT_CMD_tutorial_14.png
    :alt: TBD


** Stopped with adding text here (2023-11-14).  Continue later.**

**2.10.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_15.png
    :name: TOPCAT_CMD_tutorial_15.png
    :alt: TBD

**2.11.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_16.png
    :name: TOPCAT_CMD_tutorial_16.png
    :alt: TBD

**2.12.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_17.png
    :name: TOPCAT_CMD_tutorial_17.png
    :alt: TBD

**2.13.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_18.png
    :name: TOPCAT_CMD_tutorial_18.png
    :alt: TBD

**2.14.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_19.png
    :name: TOPCAT_CMD_tutorial_19.png
    :alt: TBD

**2.15.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_19.png
    :name: TOPCAT_CMD_tutorial_19.png
    :alt: TBD

**2.16.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_20.png
    :name: TOPCAT_CMD_tutorial_20.png
    :alt: TBD

**2.17.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_21.png
    :name: TOPCAT_CMD_tutorial_21.png
    :alt: TBD


Step 3. Interact with Multiple Plots/Tables
===========================================

**3.1.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_22.png
    :name: TOPCAT_CMD_tutorial_22.png
    :alt: TBD

**3.2.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_23.png
    :name: TOPCAT_CMD_tutorial_23.png
    :alt: TBD

**3.3.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_24.png
    :name: TOPCAT_CMD_tutorial_24.png
    :alt: TBD

Step 4. Create Interactive 3D Plots
===================================

**4.1.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_25.png
    :name: TOPCAT_CMD_tutorial_25.png
    :alt: TBD

**4.2.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_26.png
    :name: TOPCAT_CMD_tutorial_26.png
    :alt: TBD

**4.3.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_27.png
    :name: TOPCAT_CMD_tutorial_27.png
    :alt: TBD

**4.4.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_28.png
    :name: TOPCAT_CMD_tutorial_28.png
    :alt: TBD

**4.5.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_29.png
    :name: TOPCAT_CMD_tutorial_29.png
    :alt: TBD

**4.6.**  ...:

.. figure:: /_static/TOPCAT_CMD_tutorial_30.png
    :name: TOPCAT_CMD_tutorial_30.png
    :alt: TBD
