.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-Intermediate:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

############################################
02. Explore a SNIa Lightcurve (intermediate)
############################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham and Greg Madejski

**Last verified to run:** 2022-06-26

**Targeted learning level:** intermediate

**Introduction:** 
This notebook explores the data for a SNIa lightcurve: the i-band photometry, the seeing for each i-band epoch, and the astrometric scatter of the i-band observations.
The scientific motivation being considered here is that a user knows the coordinates of a low-redshift SNIa (67.4579, -44.0802), and now
wants to find an i-band epoch in which this SNIa was bright *and* the seeing was good.
The user also wants to get a sense of the scatter in the astrometric precision for the coordinates in the DiaObjects catalog.
For example, perhaps the user knows there is pre-explosion JWST imaging of the host galaxy, and is looking for the best image from Rubin Observatory
with which to co-register with the JWST image in order to characterize the underlying stellar population (or progenitor star) at the SNIa's location.

This tutorial assumes a basic working knowledge of the Portal interface (e.g., the successful completion of the first Portal tutorial).
This tutorial uses the Astronomy Data Query Language (ADQL) to query and retrieve data from the DP0.2 catalogs.
ADQL is similar to SQL (Structured Query Langage), and the `documentation for ADQL <http://www.ivoa.net/documents/latest/ADQL.html`_ includes more information about syntax and keywords.
For more information about the DP0.2 catalogs, visit the :ref:`DP0-2-Data-Products-DPDD` or the `DP0.2 Catalog Schema Browser <https://dm.lsst.org/sdm_schemas/browser/dp02.html>`_.



.. _DP0-2-Portal-Intermediate_Step-1:

1. Determine the DiaObject Id
=============================

1.1. Log in to the Portal Aspect.

1.2. Leave the TAP Service and Query Type as their default, and select the dp02_dc2_catalogs.DiaObject table.

1.3. Check the box for spatial constraints, and use ra and decl as the longitude and latitude columns. Leave the shape type as Cone and enter the coordinates "67.4579, -44.0802". Set the radius to 2 arcseconds.

1.4. In the table at right, select columns ra, decl, and diaObjectId to be returned.

.. figure:: /_static/portal_tut02_step01.png
    :name: portal_tut02_step01

    Initial query to obtain the DiaObjectId.

1.5. Click "Search" and view the results: there is only one DiaObject within 2 arcseconds, with coordinates "67.4579634, -44.080243" and DiaObjectId "1252220598734556212".
This is definitely the SNIa of interest to the user.


.. _DP0-2-Portal-Intermediate_Step-2:

2. Query the DiaSource table
============================

2.1. Clear the previous search and return to the main Portal interface (use the "RSP TAP Search" button at upper left).

2.2. Select Query Type as "Edit ADQL (advanced)", enter the following ADQL query.
This query will retrieve all of the DiaSource table entries (i.e., all of the individual measurements on the difference images) for this DiaObject.
This query also uses the ccdVisitId to join to the CcdVisit table and obtain the mean seeing measurement for the visit.

.. code-block:: SQL

   SELECT diasrc.ra, diasrc.decl, 
   diasrc.diaObjectId, diasrc.diaSourceId, 
   diasrc.filterName, diasrc.midPointTai, 
   scisql_nanojanskyToAbMag(diasrc.psFlux) AS psAbMag,
   ccdvis.seeing
   FROM dp02_dc2_catalogs.DiaSource AS diasrc
   JOIN dp02_dc2_catalogs.CcdVisit AS ccdvis
   ON diasrc.ccdVisitId = ccdvis.ccdVisitId
   WHERE diasrc.diaObjectId = 1252220598734556212

2.3. Click "Search".







.. _DP0-2-Portal-Advanced-Table-Join:

Complex ADQL queries: joining multiple tables
=============================================

This section demonstrates how to do the analysis from the tutorial notebook "06_Comparing_Object_and_Truth_Tables" in :ref:`DP0-2-Tutorials-Notebooks`, but using the ADQL query capability of the Portal Aspect rather than a Jupyter notebook.
You will extract data from a small region of sky in the `object` table, and simultaneously join this together with the `truth-match` table to enable comparison of the simulated and measured properties of some stars and galaxies.

This tutorial assumes that you have read the basic intro to the Portal Aspect in :doc:`/data-access-analysis-tools/portal-intro`.

After logging into the Portal Aspect, select ADQL to query via the ADQL interface.
Let's begin by executing a query on a single table.
The following figure illustrates a selection from the `object` table in a circular region of ``0.1 degree`` radius centered on ``(RA, Dec)`` = ``(62.0, -37.0)`` degrees:

.. code-block:: SQL

   SELECT objectId, coord_ra, coord_dec, 
          g_calibFlux, r_calibFlux, i_calibFlux
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(
   POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62.0, -37.0, 0.05)) = 1
   AND (g_calibFlux >1000 AND i_calibFlux>1000 AND r_calibFlux>1000)

Type the above query into the ADQL Query block and click on the "Search" button in the bottom left-corner to execute.
The search results will populate the "Results View," which should look similar to the next figure.
The query returns 492 results, with the 6 data columns you specified in the query.

.. figure:: /_static/Portal_Advanced_Single_Query.png
    :name: advanced_portal_example_search

    Results from a 0.05-degree query of the DP0.2 Object catalog.

In the tutorial notebook, you would execute the same query as above, and then queried the `truth_match` table for the same region of sky, like this:

.. code-block:: SQL
   
   SELECT coord_ra, coord_dec, match_objectId,
          g_calibFlux, r_calibFlux, i_calibFlux, truth_type, match_sep, is_variable
   FROM dp02_dc2_catalogs.MatchesTruth
   WHERE CONTAINS(
   POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62.0, -37.0, 0.05)) = 1
   AND match_objectId >= 0
   AND is_good_match = 1

Notice that you included additional constraints in the last two lines.
Objects in the `truth-match` table that do not have matches in the `object` table have "match_objectId = -1,"
while those with legitimate matches contain the ``objectId`` of the corresponding object from the `object` table in "match_objectId."
By requiring this to be greater than or equal to zero, you extract only objects with matches.
You also keep only sources satisfying the "is_good_match" flag, which is described in the schema as being "True if this object--truth matching pair satisfies all matching criteria."
(Note that "1" and "TRUE" are equivalent in ADQL.)

When exploring the notebook, you can continue by creating Python dataframes of the two tables, then matching them based on the IDs.
But in ADQL, you can do the matching of tables directly by joining on the requirement that "match_objectId" in the `truth-match` table equals the ``objectId`` from the `object` table.
This is how the JOIN is done:

.. code-block:: SQL

   SELECT obj.objectId, obj.coord_ra, obj.coord_dec, 
          obj.g_calibFlux, obj.r_calibFlux, obj.i_calib_Flux_i, obj.tract, obj.patch
          truth.g_calibFlux, truth.r_calibFlux, truth.i_calibFlux, truth.truth_type,
          truth.match_sep, truth.is_variable
   FROM dp02_dc2_catalogs.object as obj
   JOIN dp01_dc2_catalogs.truth_match as truth
   ON truth.match_objectId = obj.objectId
   WHERE CONTAINS(
   POINT('ICRS', obj.ra, obj.dec),
   CIRCLE('ICRS', 62.0, -37.0, 0.05))=1
   AND truth.match_objectid >= 0
   AND truth.is_good_match = 1

Try the above query in the ADQL window -- you should retrieve 14,424 results.

Just to confirm that things look as expected, you should plot a color-magnitude (``g`` vs. ``g-i``) and color-color (``r-i`` vs. ``g-r``) diagram.
Since you won't be using the image any more, switch to the view with only the table and an xy-plot by clicking the "xy-tbl" at the upper-right.
To plot a color-magnitude diagram, click on the double gear icon in the xy-plot panel (it should say "Chart options and tools" when you mouse over it).

Enter the values seen in the example below. You will use the "cModel" magnitudes, plotting ``g`` vs. ``g-i``, to make a color-magnitude diagram.

.. figure:: /_static/Portal_Plot_CMD.png
    :width: 200
    :name: portal_cmd_plot
    
    Example of creating a plot in the Portal.

Now create another plot by again clicking the double gear icon, and entering the following:

.. figure:: /_static/Portal_Plot_ColorColor.png
    :width: 200
    :name: portal_colorcolor_plot

    Another example of creating a plot in the Portal.

Initially, the figures look kind of smashed into the top-half of the screen.
Click the double arrow icon at the upper-right to make the figures take up the whole screen.
Then, you should have something that looks like this:

.. figure:: /_static/Portal_Plots_big.png
    :name: portal_big_plots

Those figures are a bit messy, because they contain more than 14,000 points.
Next, you will filter the points to plot only stars.
To do this, first separate the "stars" and "galaxies" using the truth_type column from the `truth-match` table.
Simulated stars have ``truth_type`` = ``2``, and galaxies have ``truth_type`` = ``1``.
If you click on the filter icon at the top of your figures, you can enter text like the following in the box that pops up.
This will keep only points with ``truth_type`` = ``1``.
Feel free to play around with filtering based on other columns!

.. figure:: /_static/Portal_Filter_Plot.png
    :width: 200
    :name: portal_filter_plot

After filtering both panels, you should get color-magnitude and color-color diagrams that look like this:

.. figure:: /_static/Portal_Plots_stars_only.png
    :name: portal_big_plots_stars_only

Hooray - the stars lie on a narrow locus in the color-color plot, as you might expect!

Finally, try comparing the measurements from the `object` table to the "true" values for some objects.
You will compare the recovered flux to the "true" value that was simulated for each object (as a ratio of the fluxes).
Once again click on the double gear icon, and create a new scatter plot with the following parameters:

.. figure:: /_static/Portal_Plot_FluxComparison.png
    :width: 200
    :name: portal_flux_comparison_plot

The resulting figure should look something like the one below. Most of the points lie along a line at y-axis values near ``1.0``, meaning that the measured fluxes are roughly equal to the simulated (input) fluxes.
That's reassuring!

One final note: in the screenshot below, you can see that hovering over a point in the figure will tell you the values of that point.
Furthermore, if you click the point, you can see that it is then highlighted in the table.

.. figure:: /_static/Portal_meas_vs_truth_flux.png
    :name: portal_meas_vs_truth_flux