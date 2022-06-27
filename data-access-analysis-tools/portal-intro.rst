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

.. _Portal-Intro-User-Interface:

The Portal's user interface
===========================

**Try it:** Mouse-over text to view pop-up boxes with more detailed descriptions throughout the Portal interface.   

**"1. Select TAP Service"**
Leave the default (``https://data.lsst.cloud/api/tap``) to access DP0 data.

**"2. Select Query Type"**
There are three types of queries: "Single Table (UI assisted)", "Edit ADQL (advanced)", and "Image Search (ObsTAP)".
Each of these options has a different user interface, covered in the sections below.


.. _Portal-Intro-Single-Table-Queries:

Single Table Queries
====================

The default query type, and default user interface, is for "Single Table (UI assisted)" queries.

.. figure:: /_static/portal_default_view_DP02.png
    :name: portal_default_view_DP02

    The default view of the Portal's user interface for single table queries.
    
**3. Select Table**: Drop down menus of available tables.
For DP0 data, choose the "Table Collection (Schema): dp02_dc2_catalogs" in the left drop-down menu.
The default table in the right drop-down menu is the Object table.
See the :ref:`DP0-2-Data-Products-DPDD` for table descriptions and schema.
The table view at lower-right will automatically update to match the selected table.

**4. Enter Constraints**: For "Spatial" constraints, the longitude and latitude columns do not yet automatically 
update to be the correct column names for right ascension and declination for the selected table, and need to be 
entered (for the DP0.2 Object table, they are "coord_ra" and "coord_dec").
If a non-existent column name is entered the box will highlight red in indication of the error.
Choose the desired shape type for a spatial search, such as "Cone", and the appropriate instructions for the search terms will appear.
Keeping the search area to a minimum will keep query times short and returned subsets small and manageable as you learn.
It is recommended to start with 3 arcminutes. 

*Note*: The central coordinates for DC2, in decimal degrees, are: ``61.863 -35.790``.

.. figure:: /_static/portal_EnterConstraints_DP02.png
    :name: portal_enter_constraints_DP02
    
    These basic constraints should work well for all learners.

**Table View**:
The table to the right of "Enter Constraints" enables applying additional search constraints on the columns in the selected catalog table.
Use the checkboxes in the left-most column to select the data column names to be returned by the query.
Use the filter icon to only view selected data column names.
Use the constraints column to specify query parameters and only retrieve data which meets those constraints.
Some of the attributes of the table columns in the DC2 datasets are blank, but these are expected to be populated in the future Data Previews and Data Releases.

.. figure:: /_static/portal_table_view_DP02.png
    :name: portal_table_view_DP02

    The table view offers additional query options.

Some tables have a lot of data columns.
Search for desired data columns by entering terms in the boxes underneath "column_name" or "description" and pressing "enter".  
An example of a query for Object catalog data with "detect_isPrimary" = True, the g-band cModel flux > 100000
(i.e., apparent magnitudes less than about 19th mag), and an extendedness = 0 in the g-band (i.e., stars), is shown in the figure above. 
Remove filters and reset the table view at any time using the "Remove" or "Reset" buttons above the upper-right corner of the table.

**Convert to ADQL**:
If desired, convert table view queries to "ADQL Queries" using the "Populate and Edit ADQL" button at the bottom of the page.
This can enable entering more complex constraints that cannot be expressed against individual columns.

**Apply a Row Limit**:
The "Row Limit" in the bottom bar can be changed to apply an upper bound to the number of rows returned.
The Portal can work effectively with datasets with millions of rows.
However, when learning or testing queries, it is advisable to limit the number of rows (e.g., 10000 rows is useful for testing).

*Note*: Because of the implementation of the Rubin Observatory "Qserv" database, it is not recommended to use the row limit
alone in order to get a "sampling" of data.
Queries with only a row limit can run for much longer than one might intuitively expect; applying a spatial constraint is
likely to return a result more quickly.

**Example**:
The example in the image below queries the dp02_dc2_catalogs.Object table using a cone search centered on ``62.0 -37.0``
in decimal degrees (close to the approximate center of the DC2 region) with a 3 arcminutes radius.
The search allows you to provide additional constraints, and the example here limits the flux as specified in Column "constraints."
The search will return data in columns ``coord_ra``, ``coord_dec``, ``g_calibFlux``, ``r_calibFlux``, and ``i_calibFlux`` for all
objects with ``g_calibFlux``, ``i_calibFlux``, and ``i_calibFlux`` in the range you specified, between 20 and 1000 nanojansky
(i.e., between 24th and 28th magnitude).  

.. figure:: /_static/portal_example_search_DP02.png
    :name: portal_example_search_DP02

    An example query of the DC2 Object catalog.

**Search**: Press the search button at lower left when ready to execute.

.. figure:: /_static/portal_search_working.png
    :name: portal_search_working
    :width: 200

    This will show while the search is executing.

**Results View**: The search results will populate the results view, as shown in the next figure.

.. figure:: /_static/portal_search_results_DP02.png
    :name: portal_search_results_DP02

    The default view of the search results.

Across the top of the results view are many icons that control the display settings; hover over the icons and a statement
about their functionality will appear at upper-right.
Also at upper right, under the user name, are the options "tri-view", "img-tbl", "img-xy", and "xy-tbl".
These control how the results view is partitioned, and the default is "tri-view".
In the "tri-view", at top-left is a sky image with the search results overplotted: it was not a simulated DC2 image but a 2MASS image
at the time this demonstration was made, but expect it to show DC2 images in the future (and LSST images when real data is available).
As this example does not use the image at upper left, the "xy-tbl" is used to view for results.

**Plotting Data**:
To manipulate the plotted data, select the double gear "settings" icon above the x-y plot and a pop-up window will open (see the next figure).
Select other columns to use, change the symbol type and color, and so forth, and click "Apply".

**Getting Magnitudes from Fluxes**:
The flux data in the DP0.2 tables are given in units of nanojansky, but in the future apparent magnitudes will be available.
In the meantime, users can still obtain magnitudes and, as in this example, plot a color-magnitude diagram of the objects
selected according to our query.
As shown below, the following conversion is required to plot the retrieved flux values as a color-magnitude diagram:  
``-1.0857*log(r_calibFlux/3.631e12)+1.0857*log(i_calibFlux/3.631e12)`` in the "X" box,
and ``-1.0857log(g_calibFlux/3.631e12)`` box for the "Y" box.  
Here, the log function in the "expression" for the plot is actually a natural log, and so the 1.0857 factor is a ratio of 2.5 over ln(10).
The 3.631 is the standard AB conversion factor from flux to magnitude.

.. figure:: /_static/portal_results_xy_settings_DP02.png
    :name: portal_results_xy_settings_DP02
    :width: 200

    The plot settings pop-up window.

Additional cuts can be applied to the plotted data using the table query boxes, for instance where you select a different range of fluxes.  
Note that corresponding plot point for the selected row in the table is differently colored, and that hovering the mouse over the plotted data will show the x- and y-values in a pop-up window.

.. figure:: /_static/portal_results_final_DP02.png
    :name: portal_results_final_DP02

    An updated results view in which the xy plot uses the magnitude columns:  mag(r)-mag(i) on the x-axis, mag(g) on the y-axis.  

See also :ref:`DP0-2-Tutorials-Portal` for additional demonstrations of how to use the Portal's Single Table Query.

.. _Portal-Intro-ADQL-Queries:

ADQL Queries
============

**1. TAP Service**: Leave the default (``https://data.lsst.cloud/api/tap``) to access DP0 data.

**2. Select Query Type**: Select "ADQL" to query via the ADQL interface. ADQL is the `Astronomical Data Query Language <https://www.ivoa.net/documents/ADQL/>`_.
The language is used by the `IVOA <https://ivoa.net>`_ to represent astronomy queries posted to Virtual Observatory (VO) services, such as the Rubin LSST TAP service.
ADQL is based on the Structured Query Language (SQL).

**3. Advanced ADQL**: When ADQL is selected as the query type, the interface in step 3 changes to provide a free-form block into which ADQL queries can be entered directly.
The query executed in the example above can be expressed in ADQL as follows:

.. code-block:: SQL

   SELECT coord_dec,coord_ra,g_calibFlux,i_calibFlux,r_calibFlux 
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),CIRCLE('ICRS', 62, -37, 0.05))=1 
   AND (g_calibFlux >20 AND g_calibFlux <1000 AND i_calibFlux >20 AND i_calibFlux <1000 
   AND r_calibFlux >20 AND r_calibFlux <1000)

Type the above query into the ADQL Query block and click on the "Search" button in the bottom-left corner to execute.
Remember to set the "Row Limit" to be a small number, such as 10000, when testing queries.
The search results will populate the same **Results View**, as shown above using the Single Table Query interface.

**Joining with another table**:
It is often desirable to access data stored in more than just one table.
This is possible to do using a JOIN clause to combine rows from two or more tables.
In the example below, the Source and CcdVisit table are joined in order to obtain the date and seeing from the CcdVisit table
for the observations that produced the photometry in the Source table.
Any two tables can be joined so long as they have an index in common.

.. code-block:: SQL

   SELECT src.ccdVisitId, src.extendedness, src.band,
   scisql_nanojanskyToAbMag(src.psfFlux) AS psfAbMag,
   cv.obsStartMJD, cv.seeing 
   FROM dp02_dc2_catalogs.Source AS src
   JOIN dp02_dc2_catalogs.CcdVisit AS cv
   ON src.ccdVisitId = cv.ccdVisitId
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 62.0, -37, 1)) = 1
   AND src.band = 'i' AND src.extendedness = 0 AND src.psfFlux > 10000
   AND cv.obsStartMJD > 60925 AND cv.obsStartMJD < 60955
    
**Query the TAP service schema**:
Information about the LSST TAP schema can also be obtained via ADQL queries.
The following query gets the names of all the available DP0.2 tables.

.. code-block:: SQL

   SELECT *
   FROM tap_schema.tables
   WHERE tap_schema.tables.table_name like 'dp02%'

To get the detailed list of columns available in the "Object" table, their associated units and descriptions:

.. code-block:: SQL

   SELECT tap_schema.columns.column_name, tap_schema.columns.unit,
   tap_schema.columns.description
   FROM tap_schema.columns
   WHERE tap_schema.columns.table_name = 'dp02_dc2_catalogs.Object'

See also :ref:`DP0-2-Tutorials-Portal` for additional demonstrations of how to use the Portal's ADQL functionality.


.. _Portal-Intro-Image-Queries:

Image Queries
=============

This is a placeholder for further instructions about how to use the image query interface and how to interact with the search results in the Portal.

These two figures are representative of what this functionality will include.

.. figure:: /_static/portal_ImageQueryDP02.png
    :name: portal_ImageQueryDP02

    An early version of the Portal's image query interface.  


.. figure:: /_static/portal_ImageQueryCoverageDP02.png
    :name: portal_ImageQueryCoverageDP02

    An early version of the Portal's image query search results coverage map.  


