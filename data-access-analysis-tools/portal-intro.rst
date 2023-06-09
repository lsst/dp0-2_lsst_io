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

#####################################
Introduction to the RSP Portal Aspect
#####################################

.. This section should provide a brief, top-level description of the page.

Log in to the Portal Aspect by clicking on the "Portal" panel of the main landing page at `data.lsst.cloud <https://data.lsst.cloud>`_.

**New for DP0.2!** :ref:`Portal-Intro-Image-Queries`

.. _Portal-Intro-User-Interface:

The Portal's user interface
===========================

**Try it:** Mouse-over text to view pop-up boxes with more detailed descriptions throughout the Portal interface.
Click on any "settings" icons you see (double gears) to explore options.
The Portal is a very powerful user interface with far more options than are covered in the introduction below.

**Select TAP Service:**
Leave the default (https://data.lsst.cloud/api/tap) to access DP0.2 data.

**Select Query Type**
There are three types of queries: :ref:`Portal-Intro-Single-Table-Queries`, :ref:`Portal-Intro-ADQL-Queries`, and :ref:`Portal-Intro-Image-Queries`.
Each of these options has a different user interface, covered in the sections below.


.. _Portal-Intro-Single-Table-Queries:

UI assisted (Single Table)
==========================

The default query type, and default user interface, is for "UI assisted" queries.

.. figure:: /_static/portal_intro_DP02a.png
    :name: portal_default_view_DP02

    The default view of the Portal's user interface for UI assisted queries.
    
**Select Table**: Drop down menus of available tables.
For DP0.2 data, choose the "Table Collection (Schema): dp02_dc2_catalogs" in the left drop-down menu.
The default table in the right drop-down menu is the Object table.
See the :ref:`DP0-2-Data-Products-DPDD` for table descriptions and schema.
Notice how the table view at lower-right will automatically update to match the selected table.

**Enter Constraints**: For "Spatial" constraints, choose the desired shape type for a spatial search 
("Cone" or "Polygon"), and the appropriate instructions for the search terms will appear. For example, 
for cone search, "Coords or Obj Name" and "Radius" of search need to be entered. 

Keeping the search area small will keep query times short and return manageable subsets of objects as you learn.
It is recommended to start with 3 arcminutes.
Note that the central (RA, Dec) coordinates for DC2, in decimal degrees, are: ``61.863 -35.790``.

The longitude and latitude columns in "Position Columns" do automatically update to be the correct 
column names for right ascension and declination for the selected table. If a non-existent column name
is entered, the box will highlight red in indication of the error.

**The table view**:
The table to the right of "Enter Constraints" enables users to apply additional search constraints on the columns in the selected catalog table.
Some tables have a lot of data columns.
Search for desired data columns by entering terms (e.g., ra, Flux, or flag) in the boxes underneath "Name" 
and pressing "enter" in order to view data columns of interest to you.

Use the checkboxes in the left-most column to select the data column names to be returned by the query.
Use the funnel icon to filter the columns, and only view selected data column names.
Use the "constraints" column to specify query parameters and only retrieve data which meets those constraints.

Remove filters and reset the table view at any time using the "Reset Column Selections & Constraints" button above the upper-right corner of the table.

**ADQL conversions**:
If desired, convert UI assisted table view queries to "ADQL Queries" using the "Populate and edit ADQL" button at the bottom of the page.
This can enable entering more complex constraints that cannot be expressed against individual columns.
This will switch the user interface to the "Edit ADQL" view.

**Row limit**:
The "Row Limit" in the bottom of the page can be changed to apply an upper bound to the number of rows returned.
The Portal can work effectively with datasets with millions of rows.
However, when learning or testing queries, it is advisable to limit the number of rows (e.g., 10000 rows is useful for testing).

*Note*: Because of the implementation of the Rubin Observatory "QServ" database, it is not recommended to use 
the row limit alone in order to get a "sampling" of data. Queries with only a row limit can run for much longer 
than one might intuitively expect; applying a spatial constraint is likely to return a result more quickly.

**Example UI assisted query**:
The image below presents an example of how to search the DP0.2 Object catalog using a 3 arcminute cone near 
the DC2's central coordinates, returning only the five data columns "coord_ra", "coord_dec", and "g" "r" 
and "i_calibFlux", and imposing the contraints that the flux must be between 20 and 1000 nanojansky (i.e., 
between 24th and 28th magnitude).

.. figure:: /_static/portal_intro_DP02b.png
    :name: portal_example_search_DP02

    An example query of the DC2 Object catalog.

**Search**: Press the search button at lower left when ready to execute.
The search might take a few moments.

.. figure:: /_static/portal_intro_DP02c.png
    :name: portal_search_working
    :width: 200

    This will show while the search is executing.

**Cancel**: It is possible to cancel a query while it is executing by clicking the "Cancel" button.

**Results view**: The search results will populate the results view, as shown in the figure below.
There are three icons that control the display layout at upper right: "Tri-view", "Bi-view Images", 
and "Bi-view Tables".
The default is "Tri-view", which is shown below, with a sky image at upper left.
The color-composite image shows the relevant DC2 simulated sky region.
A default "active chart" of the sky coordinates appears at upper right, and the table of results along 
the bottom.

.. figure:: /_static/portal_intro_DP02d.png
    :name: portal_search_results_DP02

    The default view of the search results.

**Multiple queries and results**: From the results view page (see figure above), if you click on the "RSP 
TAP Search" button at upper left you can go back to the query page and execute another query by entering 
constraints and clicking "Search". (Click "Cancel" on the TAP search page to return to the results view 
without executing a new query).

The new query's results will appear as a new tab in the table of the results view page.
In the image above, you can see that this has been done, because the results view table has two tabs, and the 
sky images show symbols with two different colors. Switching between table tabs will also cause the sky image and 
active chart to switch to show the selected query results.
Delete the results for a given query by clicking on the x in the table tab.

**Manipulating the plotted data and converting fluxes to magnitudes**:
To manipulate the plotted data, select the double gear "settings" icon above the active chart and a pop-up window 
will open (see the next figure). To create a color-magnitude diagram from the fluxes, for DP0.2 it is necessary 
to apply the `standard conversion from nanojansky to AB magnitude <https://en.wikipedia.org/wiki/AB_magnitude>`_ 
in the X and Y boxes as, e.g., "-2.5 * log10(g_calibFlux) + 31.4".
In the future, magnitudes will be available.

Add a chart title and label the axes, choose a point color, and click "Apply" and then "Close".

.. figure:: /_static/portal_intro_DP02e.png
    :name: portal_results_xy_settings_DP02
    :width: 200

    The plot settings pop-up window.

At this point, additional cuts can be applied to the table data being plotted.
In the figure below, the g-band flux is limited to >100, and this imposes a sharp cutoff in the y-axis values at 
26.4 mag. Select "Bi-view Tables" to view only the plot and the table data.
Notice how the corresponding plot point for the selected row in the table is differently colored, and that 
hovering the mouse over the plotted data will show the x- and y-values in a pop-up window.

.. figure:: /_static/portal_intro_DP02f.png
    :name: portal_results_final_DP02

    An updated results view in which the plotted data has been manipulated.

**Learn more.**
See also :ref:`DP0-2-Tutorials-Portal` for additional demonstrations of how to use the Portal's UI assisted 
Query.

.. _Portal-Intro-ADQL-Queries:

Edit ADQL (advanced)
====================

ADQL is the `Astronomical Data Query Language <https://www.ivoa.net/documents/ADQL/>`_.
The language is used by the `IVOA <https://ivoa.net>`_ to represent astronomy queries posted to Virtual Observatory (VO) 
services, such as the Rubin LSST TAP service. ADQL is based on the Structured Query Language (SQL).

Selecting "Edit ADQL" will change the user interface to display an empty box where users can supply their query statement.
Scrolling down in that interface will show several examples.

**Turn a UI assisted (i.e., single table) query into ADQL.**
At any point while assembling a query using the UI assisted query interface described above, clicking on "Populate and edit ADQL" 
at the bottom of the page will transform the query into ADQL.
Note that any changes then made to the ADQL are not propogated back to the UI assisted query constraints.

**Converting fluxes to magnitudes** is much easier with the ADQL interface by using the `scisql_nanojanskyToAbMag()` 
functionality as demonstrated below.

**Query the TAP schema.**
Information about the LSST TAP schema can be obtained via ADQL queries.
For example, to get the detailed list of columns available in the "Object" table, their associated units and descriptions:

.. code-block:: SQL

   SELECT tap_schema.columns.column_name, tap_schema.columns.unit,
   tap_schema.columns.description
   FROM tap_schema.columns
   WHERE tap_schema.columns.table_name = 'dp02_dc2_catalogs.Object'

**Query the Object table,** as done with the UI assisted query interface above, with the following ADQL:

.. code-block:: SQL

   SELECT coord_dec,coord_ra,g_calibFlux,i_calibFlux,r_calibFlux
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),CIRCLE('ICRS', 62, -37, 0.05))=1
   AND (g_calibFlux >20 AND g_calibFlux <1000
   AND i_calibFlux >20 AND i_calibFlux <1000
   AND r_calibFlux >20 AND r_calibFlux <1000)

Type the above query into the ADQL Query block and click on the "Search" button in the bottom-left corner to execute.
Remember to set the "Row Limit" to be a small number, such as 10000, when testing queries.
The search results will populate the same **Results View**, as shown above using the UI assisted Query interface.

To do the same query with magnitudes:

.. code-block:: SQL

   SELECT coord_dec, coord_ra,
   scisql_nanojanskyToAbMag(g_calibFlux) AS g_calibMag,
   scisql_nanojanskyToAbMag(i_calibFlux) AS r_calibMag,
   scisql_nanojanskyToAbMag(r_calibFlux) AS i_calibMag
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62, -37, 0.05))=1
   AND g_calibFlux BETWEEN 20 AND 1000
   AND r_calibFlux BETWEEN 20 AND 1000
   AND i_calibFlux BETWEEN 20 AND 1000

**Joining two or more tables.**
It is often desirable to access data stored in more than just one table.
This is possible to do using a JOIN clause to combine rows from two or more tables.
In the example below, the Source and CcdVisit table are joined in order to obtain the date and seeing from the CcdVisit table.
Any two tables can be joined so long as they have an index in common.

.. code-block:: SQL

   SELECT src.ccdVisitId, src.extendedness, src.band,
   scisql_nanojanskyToAbMag(src.psfFlux) AS psfAbMag,
   cv.obsStartMJD, cv.seeing
   FROM dp02_dc2_catalogs.Source AS src
   JOIN dp02_dc2_catalogs.CcdVisit AS cv
   ON src.ccdVisitId = cv.ccdVisitId
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62.0, -37, 1)) = 1
   AND src.band = 'i' AND src.extendedness = 0 AND src.psfFlux > 10000
   AND cv.obsStartMJD > 60925 AND cv.obsStartMJD < 60955

**Learn More.**
See also :ref:`DP0-2-Tutorials-Portal` for additional demonstrations of how to use the Portal's ADQL functionality.


.. _Portal-Intro-Image-Queries:

Image Search (ObsTAP)
=====================

The "Image Search (ObsTAP)" functionality has many new features -- not just new for DP0.2, but new to the Firefly interface, 
and DP0 Delegates are among the first to use them.

Checking the "Use Image Search (ObsTAP)" box below "LSST DP0.2 DC2 Tables" will change the user interface to display query 
constraint options that are specific to the image data, as described below.

For more information about the image types available in the DP0.2 data set, see the :ref:`DP0-2-Data-Products-DPDD`.

**Enter Constraints**

Under "Observation Type and Source", the IVOA standard options for "Calibration Level" (0, 1, 2, 3, or 4) are provided.
For DP0.2, "1" is the raw (unprocessed) images, "2" is the processed visit images (PVIs; the calibrated single-epoch images 
also called calexps), and "3" are the derived image data such as difference images and deep coadds.

The "Data Product Type" should be left as "Image", and the "Instrument Name", "Collection", and "Data Product Subtype" can all be left blank.

Under "Location", only “Observation boundary contains point” was implemented at the time this documentation was written.
Recall that the central (RA, Dec) coordinates for the DC2 simulated sky region are ``61.863 -35.790``.

Under "Timing", users can specify a range of the time of observation (this is only relevant for PVIs/calexps) 
and/or exposure duration.

Under "Spectral Coverage", users can provide a wavelength in, e.g., nanometers as a means of specifying the image band.

**Output Column Selection and Constraints**

The default is for all columns to be selected (i.e., have blue checks in the leftmost column).
It is recommended to always return all metadata because the Portal requires some columns in order for the some of the 
Results view functionality to work.

**Example (PVIs/calexps)**

The image below shows an example query for all r-band PVIs (calexps) that overlap the central coordinates of DC2, 
which were obtained with a modified Julian date between 60000 and 60500.
Note that the "r" filter constraint is applied in the table at right.

.. figure:: /_static/portal_intro_DP02g.png
    :name: portal_ImageQueryDP02

    The default interface for the "Image Search (ObsTAP)" queries, with example search parameters.
    
Click on the "Search" button.

**Results View**

The default results appear in the tri-view format, with the image at upper left, an Active Chart plot at upper right, and the table of metadata below.
The first row of the table is highlighted by default, with that image showing at upper left.
The Active Chart plot default is RA versus Declination, with the location of the highlighted table row shown in orange and the rest in blue.
    
.. figure:: /_static/portal_intro_DP02h.png
    :name: portal_ImageQueryResultsDP02

    Results for the example search parameters.

**Manipulating the Active Chart plot** is the same process as shown for the :ref:`Portal-Intro-Single-Table-Queries` results: 
click on the "settings" icon (double gears) in the upper right corner to change the column data being plotted, alter the plot style, add axes labels, etc.

**Interacting with the images** begins with just hovering the mouse over the sky image and noting the RA, Dec, and pixel value appear at the bottom.
Use the magnifying glass icons in the upper left corner to zoom in and out. You may need to hover over the image for these upper left magnifying 
glasses to appear. Click and drag the image to pan.
Above the magnifying glass icons, use the back and forth arrows to navigate between HDU (header data units) 1, 2, and 3: the image, mask, and variance data.
Click on another row in the table, to display an image of a different part of the sky.
At upper right, click on "Bi-view Tables" to show a choice of the Active Chart plot, sky coverage, or the image and the table side-by-side.

.. figure:: /_static/portal_intro_DP02i.png
    :name: portal_ImageQuery_sidebyside_DP02

    Display the image in row three of the table (with the view format set to "Bi-view Tables").

**Image tools**:
There are many tools available for users, the following demonstrates use of just one.
First, zoom in on a bright star in one of the images.
Select the "tools" icon (wrench and ruler), and from the pop-up window choose to "Extract" using a line.
Draw a line on the image across the star to extract the pixel values and show an approximate shape of the point-spread function for the star.
The plot reveals that this particular star is saturated.
Click on "Pin Table" to add a table of pixel data as a new tab in the right half of the view.
To make the line go away, click on the "layers" icon (the one for which the hover-over text reads:  "Manipulate overlay display...") and in the pop-up window, next to "Extract Line 1 - HDU#1", click on "Delete".

.. figure:: /_static/portal_intro_DP02j.png
    :name: portal_ImageQuery_tools_DP02

    Use the image display tool to extract a line cut.

**Image grid display**:
Above the image use the grid icon (hover-over text "Tile all images in the search result table") to show up to eight of the images side-by-side.
Notice that it is possible to pan and zoom in each of these grid windows. This functionality is only available with the "Tri-view" layout. 
The default view is "Show single image at full size".

**Coverage window**:
Above the image, notice that the default tab view is "Data Product", and instead click on "Coverage".
The bounding boxes of all images listed in the table are shown, with the image in the selected row highlighted.
The color-composite background shows the relevant DC2 simulated sky region.

.. figure:: /_static/portal_intro_DP02k.png
    :name: portal_ImageQueryCoverageDP02

    The coverage outlines of images returned by the ObsTAP search, overlayed on the relevant DC2 simulated sky region.

**Learn More.**
See also :ref:`DP0-2-Tutorials-Portal` for a tutorial using additional image types and more of the Portal's image-related functionality.
