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
The scientific motivation here is that a user knows the coordinates of a low-redshift SNIa (67.4579, -44.0802), and now
wants to find an i-band epoch in which this SNIa was bright *and* the seeing was good.
The user also wants to get a sense of the scatter in the astrometric precision for the coordinates in the DiaObjects catalog.
For example, perhaps the user knows there is pre-explosion JWST imaging of the host galaxy, and is looking for the best image from Rubin Observatory
with which to co-register with the JWST image in order to characterize the underlying stellar population (or progenitor star) at the SNIa's location.

This tutorial assumes a basic working knowledge of the Portal interface (e.g., the successful completion of the first Portal tutorial).
This tutorial uses the Astronomy Data Query Language (ADQL) to query and retrieve data from the DP0.2 catalogs.
ADQL is similar to SQL (Structured Query Langage), and the `documentation for ADQL <http://www.ivoa.net/documents/latest/ADQL.html>`_ includes more information about syntax and keywords.
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
   AND diasrc.filterName = 'i'

2.3. Click "Search".


.. _DP0-2-Portal-Intermediate_Step-3:

3. Make the three plots
=======================

3.1. If the Results view is showing three panels including a sky image at upper left, switch to the "xy-tbl" view using the buttons at upper right.
Use the settings icon (two gears at upper right) to open the plot parameters pop-up window, match those shown below, then click "Apply" and "Close".

.. figure:: /_static/portal_tut02_step03a.png
    :name: portal_tut02_step03a

    Plot parameters for the lightcurve.

3.2. View the r-band lightcurve for this SNIa.

.. figure:: /_static/portal_tut02_step03b.png
    :name: portal_tut02_step03b

    The r-band lightcurve for the SNIa of interest.

3.3. To add a plot of time versus seeing: use the settings icon, choose "Add New Chart" and match the parameters shown below, then click "OK".

.. figure:: /_static/portal_tut02_step03c.png
    :name: portal_tut02_step03c

    Plot parameters for the time *versus* seeing plot.

3.4. To add a plot to visualize the astrometric precision: use the settings icon, choose "Add New Chart" and match the parameters shown below, then click "OK".
Note that in both the X and Y parameters, the difference between the DiaSource coordinate and the DiaObject coordinate are divided by 3600, so that the plot axes are in arcseconds.

.. figure:: /_static/portal_tut02_step03d.png
    :name: portal_tut02_step03d

    Plot parameters for the astrometric precision plot.

3.5. View all three plots together.
In the center plot, click on the r-band epoch with the best seeing (0.75 arcsec).
Notice how the point turns orange in all three plots, and that the corresponding table row will be highlighted.

In the left-most plot, the lightcurve, notice that for this "best-seeing" epoch the SNIa had an apparent magnitude near its peak (around 22nd mag).
That makes it a suitable choice for the scientific use-case outlined in the Introduction.

In the right-most plot, the astrometric precision, notice that for this "bright / best-seeing" epoch the measured sky coordinates of the DiaSource are very close to those reported for the DiaObject.
This *does not* necessarly mean that the coordinates for the "best-seeing" epoch are more accurate, because the
coordinates of DiaObjects are *derived from* the individual DiaSources.
The point of the right-most plot is more that the overall scatter is low (less than 0.3 arcsec), and that selecting the 
"bright / best-seeing" epoch image for co-registration with images from other facilities is a wise choice.

.. figure:: /_static/portal_tut02_step03e.png
    :name: portal_tut02_step03e

    Identifying the best epoch for this scientific use-case.


.. _DP0-2-Portal-Intermediate_Step-4:

4. Exercise for the learner: obtain the visitId
===============================================

4.1. At this point, the user is ready to obtain the "bright / best seeing" epoch's images.
The simplest way to do that is with the visitId, but the ADQL query did not request that from the CcdVisit table.
Return to the ADQL query and add ccdvis.ccdVisitId and ccdvis.visitId to the query.