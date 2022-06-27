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
Notice how the table view at lower-right will automatically update to match the selected table.

**4. Enter Constraints**: For "Spatial" constraints, the longitude and latitude columns do not yet automatically 
update to be the correct column names for right ascension and declination for the selected table, and need to be 
entered (for the Object table, they are "coord_ra" and "coord_dec").
If a non-existent column name is entered the box will highlight red in indication of the error.
Choose the desired shape type for a spatial search, such as "Cone", and the appropriate instructions for the search terms will appear.

Keeping the search area to a minimum will keep query times short and returned subsets small and manageable as you learn.
It is recommended to start with 3 arcminutes.
Note that the central coordinates for DC2, in decimal degrees, are: ``61.863 -35.790``.

**The table view**:
The table to the right of "Enter Constraints" enables users to apply additional search constraints on the columns in the selected catalog table.
Some tables have a lot of data columns.
Search for desired data columns by entering terms (e.g., ra, Flux, or flag) in the boxes underneath "column_name" or "description" and pressing "enter" in order to view data columns of interest to you. 

Use the checkboxes in the left-most column to select the data column names to be returned by the query.
Use the funnel icon to filter the columns, and only view selected data column names.
Use the constraints column to specify query parameters and only retrieve data which meets those constraints.

Remove filters and reset the table view at any time using the "Remove" or "Reset" buttons above the upper-right corner of the table.

**ADQL conversions**:
If desired, convert table view queries to "ADQL Queries" using the "Populate and Edit ADQL" button at the bottom of the page.
This can enable entering more complex constraints that cannot be expressed against individual columns.
This will switch the user interface to the "Edit ADQL (advanced)" view.

**Row limit**:
The "Row Limit" in the bottom bar can be changed to apply an upper bound to the number of rows returned.
The Portal can work effectively with datasets with millions of rows.
However, when learning or testing queries, it is advisable to limit the number of rows (e.g., 10000 rows is useful for testing).

*Note*: Because of the implementation of the Rubin Observatory "Qserv" database, it is not recommended to use the row limit
alone in order to get a "sampling" of data.
Queries with only a row limit can run for much longer than one might intuitively expect; applying a spatial constraint is
likely to return a result more quickly.

**Example single-table query**:
The image below presents and example of how to search the DP0.2 Object catalog using a 3 arcminute cone near the DC2's central coordinates, 
returning only the five data columns "coord_ra", "coord_dec", and "g" "r" and "i_calibFlux",
and imposing the contraints that the flux must be between 20 and 1000 nanojansky (i.e., between 24th and 28th magnitude).

.. figure:: /_static/portal_example_search_DP02.png
    :name: portal_example_search_DP02

    An example query of the DC2 Object catalog.

**Search**: Press the search button at lower left when ready to execute.
The search might take a few moments.

.. figure:: /_static/portal_search_working.png
    :name: portal_search_working
    :width: 200

    This will show while the search is executing.

**Results view**: The search results will populate the results view, as shown in the figure below.
There are many icons that control the display settings; hover the mouse over any of them to see a pop-up description.
At upper right, notice the options "tri-view", "img-tbl", "img-xy", and "xy-tbl".
The default is "tri-view", which is shown below, with a sky image at upper left.
Notice that at the time this documentation was created, the sky image was 2MASS and not a simulated DC2 image.
A default "xy" plot of the sky coordinates appears at upper right, and the table of results along the bottom.

.. figure:: /_static/portal_search_results_DP02.png
    :name: portal_search_results_DP02

    The default view of the search results.

**Maniuplating the plotted data and converting fluxes to magnitudes**:
To manipulate the plotted data, select the double gear "settings" icon above the x-y plot and a pop-up window will open (see the next figure).
To create a color-magnitude diagram from the fluxes, for DP0.2 it is necessary to apply the `standard conversion from nanojansky to AB magnitude <https://en.wikipedia.org/wiki/AB_magnitude>`_ in the X and Y boxes as, e.g., "-2.5 * log10(g_calibFlux) + 31.4".
In the future, magnitudes will be available.

Add a chart title and label the axes, choose a point color, and click "Apply" and then "Close".

.. figure:: /_static/portal_results_xy_settings_DP02.png
    :name: portal_results_xy_settings_DP02
    :width: 200

    The plot settings pop-up window.

At this point, additional cuts can be applied to the table data being plotted.
In the figure below, the g-band flux is limited to >100, and this imposes a sharp cutoff in the y-axis values at 26.4 mag.
Select "xy-tbl" to view only the plot and the table data.
Notice how the corresponding plot point for the selected row in the table is differently colored, and that hovering the mouse over the plotted data will show the x- and y-values in a pop-up window.

.. figure:: /_static/portal_results_final_DP02.png
    :name: portal_results_final_DP02

    An updated results view in which the plotted data has been manipulated.  

**Learn more.**
See also :ref:`DP0-2-Tutorials-Portal` for additional demonstrations of how to use the Portal's Single Table Query.

.. _Portal-Intro-ADQL-Queries:

ADQL Queries
============

ADQL is the `Astronomical Data Query Language <https://www.ivoa.net/documents/ADQL/>`_.
The language is used by the `IVOA <https://ivoa.net>`_ to represent astronomy queries posted to Virtual Observatory (VO) services, such as the Rubin LSST TAP service.
ADQL is based on the Structured Query Language (SQL).

Selecting "Edit ADQL (advanced)" will change the user interface to display an empty box where users can supply their query statement.
Scrolling down will show several examples.

**Turn a single table query into ADQL.**
At any point while assembling a query using the single table query interface described above, clicking on "Edit and Populate ADQL" will transform
the query into ADQL.
Note that any changes then made to the ADQL are not propogated back to the single table query constraints.

**Converting fluxes to magnitudes** is much easier with the ADQL interface by using the `scisql_nanojanskyToAbMag()` functionality as demonstrated below.

**Query the TAP schema.**
Information about the LSST TAP schema can be obtained via ADQL queries.
For example, to get the detailed list of columns available in the "Object" table, their associated units and descriptions:

.. code-block:: SQL

   SELECT tap_schema.columns.column_name, tap_schema.columns.unit,
   tap_schema.columns.description
   FROM tap_schema.columns
   WHERE tap_schema.columns.table_name = 'dp02_dc2_catalogs.Object'

In the results view, 

**Query the Object table,** as done with the single table query interface above, with the following ADQL:

.. code-block:: SQL

   SELECT coord_dec,coord_ra,g_calibFlux,i_calibFlux,r_calibFlux 
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),CIRCLE('ICRS', 62, -37, 0.05))=1 
   AND (g_calibFlux >20 AND g_calibFlux <1000 
   AND i_calibFlux >20 AND i_calibFlux <1000 
   AND r_calibFlux >20 AND r_calibFlux <1000)

Type the above query into the ADQL Query block and click on the "Search" button in the bottom-left corner to execute.
Remember to set the "Row Limit" to be a small number, such as 10000, when testing queries.
The search results will populate the same **Results View**, as shown above using the Single Table Query interface.

To do the same query with magnitudes: 

.. code-block:: SQL

   SELECT coord_dec, coord_ra, 
   scisql_nanojanskyToAbMag(g_calibFlux) AS g_calibMag, 
   scisql_nanojanskyToAbMag(i_calibFlux) AS r_calibMag, 
   scisql_nanojanskyToAbMag(r_calibFlux) AS i_calibMag 
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62, -37, 0.05))=1 
   AND scisql_nanojanskyToAbMag(g_calibFlux) < 28
   AND scisql_nanojanskyToAbMag(r_calibFlux) < 28
   AND scisql_nanojanskyToAbMag(i_calibFlux) < 28
   AND scisql_nanojanskyToAbMag(g_calibFlux) > 24
   AND scisql_nanojanskyToAbMag(r_calibFlux) > 24
   AND scisql_nanojanskyToAbMag(i_calibFlux) > 24

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


