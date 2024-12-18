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

########################################################################
How to extract and plot forced photometry light curve of a variable star
########################################################################

.. Current version December 4 2024

The Rubin data set readily provides fluxes of the objects when they were detected at a ``SNR > 5``.
In some cases, the science goal on-hand requires lower-SNR measurements.
This might be the case when fluxes of a given object measured during all visits to its location are required, for instance a measurement of its flux before and after a flare or explosion.
In those cases, the forced photometry - available in the ``ForcedSourceOnDiaObject`` table - has to be used instead.
That table contains "forced" flux measurements in locations of all objects which had positive ``SNR > 5`` detections in the table ``dp02_dc2_catalogs.DiaObject``.
The table ``dp02_dc2_catalogs.DiaObject``, in turn, contains objects which were detected using the "Difference Image Analysis" (DIA) method.
The DIA method basically subtracts the fluxes of the previously undetected objects from those that showed ``SNR > 5`` detections in individual single-epoch difference images.

This example demonstrates how to create a forced photometry lightcurve for the known RR Lyrae star located at (62.1479031, -35.799138) using the Portal aspect of the Rubin Science Platform.

The individual Processed Visit Images might have very slightly different coordinates for the same object.
With this, instead of providing the RA and Dec to the light curve extraction process, it is wise to extract the data from the ``dp02_dc2_catalogs.DiaObject`` table using the object's unique DIA object identifier ``diaObjectId``.  
Determining the ``diaObjectId``  can be accomplished via the Portal Aspect of the Rubin Science Platform, by clicking on the "UI assisted" button, selecting "DP0.2 Catalogs" tab, chosing the "dp02_dc2_catalogs" on the left, and "dp02_dc2_catalogs.DiaObject" table on the right.

Only the spatial constraints need to be entered on the left, with the 62.1479038, -35.7991348 - and a 2 arcseconds radius using the "cone Shape" ("Temporal" constraints button needs to be unchecked).
For the "Output Column Selection" only the ``diaObjectId`` and ``gPSFluxNdata`` need to be checked.
(The ``gPSFluxNdata`` will return the number of observations in the ``g`` band, and if there are multiple objects in the search radius - the one with a larger mumber of data points needs to be selected.)
Pressing the "search" button will return a few ``diaObjectId`` values.  The one with a larger number of data points is 1651589610221862935.  

The ``ForcedSourceOnDiaObject`` contains fluxes of individual objects, but it does not contain the observation epochs;  however, the table ``CcdVisit`` does.
Obtaining the visit epochs will require joining two tables - specifically ``ForcedSourceOnDiaObject`` and ``CcdVisit`` on the common meta entry of ``ccdVisitId``.  
Such table joins are effectively performed using the Astronomical Data Query Language, ADQL.
Entering an ADQL query requires clicking on the "Edit ADQL" button on the upper right.  

A query given below will retrieve the coordinates, DIA object identifier, CCD visit identifier, band, and "forced" flux 
and its error for all rows of the ``ForcedSourceOnDiaObjects`` table which are associated with the ``diaObject`` of interest.
Again, the exposure time midpoint modified julian date for all visits is extracted by joining to the ``CcdVisit`` table.

.. code-block:: SQL 

   SELECT fsodo.coord_ra, fsodo.coord_dec, 
   fsodo.diaObjectId, fsodo.ccdVisitId, fsodo.band, 
   fsodo.psfFlux, fsodo.psfFluxErr, 
   cv.expMidptMJD
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo 
   JOIN dp02_dc2_catalogs.CcdVisit as cv 
   ON cv.ccdVisitId = fsodo.ccdVisitId 
   WHERE fsodo.diaObjectId =  1651589610221862935

The defalt plot will be the dec vs. RA (the plotting tool defaults to plot the data in the two leftmost columns of the table).  
The plot can be changed by opening the plot parameters pop-up window which will appear by clicking on the settings icon (a single gear above the plot window).
The example below uses ``psfFlux`` as a function of ``expMidptMJD`` (MJD time of the exposure).
Here, only one band was seleted (``r``) by selecting this under the box contaning ``band char`` in the table header.  

If a magnitude rather than flux is needed, one can use the ADQL function ``scisql_nanojanskyToAbMag()`` to convert difference image fluxes to magnitudes.

.. figure:: /_static/portal_tut05_step01d.png
    :name: portal_tut05_step01d
    :alt: A screenshot of the results view showing the table and the r-band lightcurve.

**Results view showing the table and the r-band light curve.**

