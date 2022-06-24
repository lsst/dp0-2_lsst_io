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

Across the top is a menu bar of interface options, but the DP0 data set is only accessed via the :ref:`Data-Access-Analysis-Tools-TAP` reached via the "RSP TAP Search" button.
Under **TAP Searches** there are four steps.

.. figure:: /_static/portal_default_view_DP02.png
    :name: portal_default_view_DP02

    This is the view when the DP0.2 Object table has been selected from the drop-down menus.


.. _Portal-Intro-Single-Table-Queries:

Single Table Queries
====================
**1. TAP Service**: Leave the default (``https://data.lsst.cloud/api/tap``) to access DP0 data.

**2. Select Query Type**: Select "Single Table (UI assisted)" to query via the single-table interface (default).

**3. Select Table**: Drop down menus of available tables.
For DP0 data, choose the "Table Collection (Schema): dp02_dc2_catalogs", and then choose the table to query 
(see the :ref:`DP0-2-Data-Products-DPDD` for a reminder of what tables are available).
On the right-hand side of the panel, select "dp02_dc2_catalogs.Object" from the drop-down menu.  
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

Mouse-over to view pop-up boxes with instructions throughout the Portal interface.   

Remove filters and reset the table view at any time using the "Remove" or "Reset" buttons above the upper-right corner of the table.

If desired, convert table view queries to `ADQL Queries` using the "Populate and Edit ADQL" button at the bottom of the page.
This can enable entering more complex constraints that cannot be expressed against individual columns.

**Search:** Press the search button at lower left when ready to execute.

The `Row Limit` may be changed to apply an upper bound to the number of rows returned.  For starters, you can select 10000.  
The Portal can work effectively with datasets with up to a million rows, or even more; however, in the present implementation of the RSP it is advisable
to limit the number of columns requested for queries expected to return results on such a scale: `SELECT *` for 100,000+ rows can return datasets of unwieldy total size.

*Note*: Because of the implementation of the Rubin Observatory `Qserv` database, it is not recommended to use the row limit alone in order to get a "sampling" of data.
Queries with only a row limit can run for much longer than one might intuitively expect; applying a spatial constrain is likely to return a result more quickly.

The example in the image below queries the dp02_dc2_catalogs.Object table using a cone search centered on ``62.0 -37.0`` in decimal degrees (close to the approximate center of the DC2 region) with a 3 arcminutes radius.
The search allows you to provide additional constraints, and the example here limits the flux as specified in Column "constraints."  The search will return data in columns ``coord_ra``, ``coord_dec``, ``g_calibFlux``, ``r_calibFlux``, and ``i_calibFlux`` for all objects with ``g_calibFlux``, ``i_calibFlux``, and ``i_calibFlux`` in the range you specified, between 20 and 1000 nanojansky.  

.. figure:: /_static/portal_example_search_DP02.png
    :name: portal_example_search_DP02

    An example query of the DC2 Object catalog.

.. figure:: /_static/portal_search_working.png
    :name: portal_search_working
    :width: 200

    This will show while the search is executing.

**Results View**: The search results will populate the results view, as shown in the next figure.

.. figure:: /_static/portal_search_results_DP02.png
    :name: portal_search_results_DP02

    The default view of the search results.

Across the top of the results view are many icons that control the display settings; hover over the icons and a statement about their functionality will appear at upper-right.
Also at upper right, under the user name, are the options "tri-view", "img-tbl", "img-xy", and "xy-tbl".
These control how the results view is partitioned, and the default is "tri-view".
In the "tri-view", at top-left is a sky image with the search results overplotted, but note that this is *not* a simulated DC2 image, but a 2MASS image.
Select "HiPS" and a "Change HiPS" button will appear with options for sky images to use, but none of the options are relevant for the DC2 simulated sky data.
Thus for DP0, the "xy-tbl" is the most relevant view for results.

To manipulate the plotted data, select the double gear "settings" icon above the x-y plot and a pop-up window will open (see the next figure).
Select other columns to use, change the symbol type and color, and so forth, and click "Apply".

The data in the DP0.2 tables are given in units of nanojansky.  Astronomers often prefer to display or plot data in a form of magnitudes.  Since our original goal was to plot a color-magnitude diagram of the objects selected according to our query, we can enter the following values:  
``-1.0857*log(r_calibFlux/3.631e12)+1.0857*log(i_calibFlux/3.631e12)`` in the "X" box, and ``-1.0857log(g_calibFlux/3.631e12)`` box for the "Y" box.  
Here, the log function in the "expression" for the plot is a natural log, and so the 1.0857 factor is a ratio of 2.5 over ln(10).  The 3.631 is the standard AB conversion factor from flux to magnitude.  

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
The query executed in the :ref:`Portal-Intro-Single-Table-Queries` example above can be expressed in ADQL as follows:

.. code-block:: SQL

   SELECT coord_ra, coord_dec, g_calibFlux, r_calibFlux
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(
   POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62.0, -37, 0.05))=1
   AND (g_calibFlux>1000 AND i_calibFlux>1000)

Type the above query into the ADQL Query block and click on the "Search" button in the bottom-left corner to execute.
You should set the row limit to be a small number, such as 10, when first testing queries.
The search results will populate the same **Results View**, as shown above using the Single Table Query interface.
A total of 492 records should be returned, which you can interact with in the same manner as outlined in :ref:`Portal-Intro-Single-Table-Queries`.

**Joining with another table**
It is often desirable to access data stored in more than just one table.
We do this using a JOIN clause to combine rows from two or more tables.
Here, using the same query as above, we will join the data in the object table with the data in the truth table to compare the results of the processing with the input truth information.
The two tables are joined by matching the ``objectId`` across two catalogs.

.. code-block:: SQL

    SELECT obj.coord_ra as ora, obj.coord_dec as odec,
    truth.ra as tra, truth.dec as tdec,
    truth.is_good_match
    FROM dp01_dc2_catalogs.object as obj
    JOIN dp01_dc2_catalogs.truth_match as truth
    ON truth.match_objectId = obj.objectId
    WHERE CONTAINS(
    POINT('ICRS', obj.ra, obj.dec),
    CIRCLE('ICRS', 61.863, -35.79, 0.05555555555555555))=1
    

This query also includes some additional quality filtering on the match.
In the `truth_match` table, ``is_good_match`` is ``true`` (or ``1``) if an object-truth matching pair satisfies all matching criteria, or it is ``false``(or ``0``) otherwise.
``is_good_match`` for an object is defined as, separations <1 arcsec and magnitude differences <1 mag.
This reduces the number of results returned from 205 to 191.

.. figure:: /_static/portal_results_join.png
    :name: portal_results_join
    :width: 600

    The results of a JOIN.

Note that ``is_good_match`` is of type boolean whereas in the ADQL query above we selected good matches by filtering on ``truth.is_good_match`` = ``1`` . With ADQL, the "=0" (false) or "=1" (true) syntax for booleans should be used.

**Query the TAP service schema**
Information about the LSST TAP schema can also be obtained via ADQL queries.
The following query gets the names of all the available DP0.2 tables.

.. code-block:: SQL

   SELECT *
   FROM tap_schema.tables
   WHERE tap_schema.tables.table_name like 'dp01%'

To get the detailed list of columns available in the `object` table, their associated units and descriptions:

.. code-block:: SQL

   SELECT tap_schema.columns.column_name, tap_schema.columns.unit,
   tap_schema.columns.description
   FROM tap_schema.columns
   WHERE tap_schema.columns.table_name = 'dp01_dc2_catalogs.object'

This produces a subset of the data shown in the lower-right pane of the Portal's **Single Table** query screen, described above.

See also :ref:`DP0-2-Tutorials-Portal` for additional demonstrations of how to use the Portal's ADQL functionality.
