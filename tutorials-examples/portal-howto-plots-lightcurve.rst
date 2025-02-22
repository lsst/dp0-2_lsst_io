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

###########################################################
08.3. How to extract and plot forced photometry light curve
###########################################################
**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** intermediate

**Introduction:**
This tutorial demonstrates how to create a light curve of an object in all observations where it was not detected at a ``SNR > 5`` - for instance a measurement of a flux of a star which is on occasion extremely faint.
In those cases, the forced photometry - available in the ``ForcedSourceOnDiaObject`` table - has to be used instead.
That table contains "forced" flux measurements in locations of all objects which had positive ``SNR > 5`` detections in the table ``dp02_dc2_catalogs.DiaObject``.

This example demonstrates how to create a forced photometry lightcurve of a RR Lyrae star located at (62.1479031 -35.7991348).

**1.  Note the need to determine the Object ID for the object of interest.** Note that the individual Processed Visit Images might have very slightly different coordinates for the same object, so it is wise to extract the data from the ``dp02_dc2_catalogs.DiaObject`` table using the object's unique DIA object identifier ``diaObjectId``.  

**2. Select the relevant table containing the** ``diaObjectId``.  After logging into the Portal aspect of the Rubin Science Platform, click on the "UI assisted" button, select "DP0.2 Catalogs" tab, chose the "dp02_dc2_catalogs" on the left, and "dp02_dc2_catalogs.DiaObject" table on the right.  

**3. Determine the object's** ``diaObjectId``.  For spatial constraints, enter 62.1479031, -35.7991348 and a 2 arcseconds radius using the "cone Shape" ("Temporal" constraints button needs to be unchecked).
For the "Output Column Selection" check the ``diaObjectId`` box and the ``nDiaSources`` - the latter will tell you the number of observations of each ``diaObjectId``.
In the case if there were multiple ``diaObjectId`` entries, you will select the one with the largest number of observations.
Pressing the "search" button will return two entries.  The one with the larger number of observations has the ``diaObjectId`` of 1651589610221862935.

.. figure:: /_static/portal-howto-plots-RRLyrae-lc-1.png
    :name: Howto_RRLyrae_lightcurve_1
    :alt: A screenshot of the results view showing the table of RA, Dec and number of observations of an object at the selected location.

    Figure 1: A screenshot of the results view showing the table of RA, Dec and number of observations of an object at the selected location.


**4.  Select the tables containing fluxes and observation epochs of the object and determine the common meta entry.**
``ForcedSourceOnDiaObject`` contains fluxes of individual objects, but it does not contain the observation epochs;  however, the table ``CcdVisit`` does.
Obtaining the visit epochs will require joining two tables - specifically ``ForcedSourceOnDiaObject`` and ``CcdVisit`` on the common meta entry of ``ccdVisitId``.
Such table joins are effectively performed using the Astronomical Data Query Language, ADQL.
Click on the "Edit ADQL" button on the upper right.  

**5.  Enter the query to  retrieve the required data.**
This query extracts coordinates, DIA object identifier, CCD visit identifier, band, and forced PSF flux 
and its error for all rows of the ``ForcedSourceOnDiaObjects`` table which are associated with the ``diaObject`` of interest, for visits with ll filters (bands).  
Again, the exposure time midpoint modified Julian date for all visits is extracted by joining to the ``CcdVisit`` table.

.. code-block:: SQL 

   SELECT fsodo.coord_ra, fsodo.coord_dec, 
   fsodo.diaObjectId, fsodo.ccdVisitId, fsodo.band, 
   fsodo.psfFlux, fsodo.psfFluxErr, 
   cv.expMidptMJD
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo 
   JOIN dp02_dc2_catalogs.CcdVisit as cv 
   ON cv.ccdVisitId = fsodo.ccdVisitId 
   WHERE fsodo.diaObjectId = 1651589610221862935

**6.  Create the default plot.**  Click on "Search".  The default plot will be the dec vs. RA (the plotting tool defaults to plot the data in the two leftmost columns of the table).  

**7.  Modify the plot to display the light curve.**  Change the plot by opening the plot parameters pop-up window which will appear by clicking on the settings icon (a single gear above the plot window).

For y-axis, use ``psfFlux`` and for the x-axis, use ``expMidptMJD-60000`` to make it more clear.
Add error bars for the y-axis (extracted as PSF flux error).

.. figure:: /_static/portal-howto-plots-RRLyrae-lc-2.png
    :name: Howto_RRLyrae_lightcurve_2
    :alt: A screenshot of the results view showing the table and the lightcurve.

    Figure 2: Results view showing the table and the light curve.

**8.  Restrict the light curve to be only for the i-band observations.**  
Click on the header of the "band" column on the table in the lower part of the screen.
Enter a checkmark by the ``i`` entry and hit "apply".
Note that the fainter flux entries disappeared.
Those were measurements in the bands where the star is generally very faint at all times.

.. figure:: /_static/portal-howto-plots-RRLyrae-lc-3.png
    :name: Howto_RRLyrae_lightcurve_3
    :alt: A screenshot of the results view showing the table and the lightcurve restricerted to the i-band.  

    Figure 3: Results view showing the table and the light curve restricted to the ``i`` band.

