.. This is the beginning of a new tutorial focussing on learning to study variability using features of the Rubin Portal

.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal05-Beginner:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

########################################################
05.  Making Multiband Lightcurves with Forced Photometry
########################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham and Greg Madejski

**Last verified to run:** 2023-03-24

**Targeted learning level:** intermediate 

**Introduction:**
Generally, the DiaSource table can be used to plot light curves, but it only includes detections with SNR > 5 in the difference images. 
If your science goal requires lower-SNR measurements (e.g. including fluxes of a given object measured during all visits to its location, for instance before and after a flare or explosion), then one can use the forced photometry in the ForcedSourceOnDiaObjects table instead.  

Let's say there is a specific object whose DiaSource light curve looks particularly interesting. 
In order to explore the flux of the object in all sets of single-epoch visit images as well as difference images, one can use the 
ForcedSourceOnDiaObject catalog.  The table in this catalog contains point-source forced-photometry measurements on individual 
single-epoch visit images and difference images, based on and linked to the entries in the DiaObject table.  We will use an ADQL query, where 
we will use the JOIN command to the CcdVisit table to obtain the exposure time mid-point in the 
Modified Julian Date (MJD) format (expMidptMJD).  

In this tutorial, we will create a Forced Photometry light curve of the supernova we considered in Portal Tutorial 02, one with the DiaObjectId "1252220598734556212".  There, we used the following ADQL query:  

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

Executing this query returned the table on the bottom of the screenshot below.  After appropriately modifying the chart options, we could plot the DiaSource light curve of the supernova - it is on the top part of the screenshot.  

.. figure:: /_static/portal_tut05_step00.png
    :name: portal_tut05_step00

Below, we will be examining its flux history in the ForcedSourceOnDiaObjects table.  Again, we will employ the Astronomical Data Query Language (ADQL) to query and retrieve the data.  

For more information, see `schema <https://dm.lsst.org/sdm_schemas/browser/dp02.html#ForcedSourceOnDiaObject>`_ of the ForcedSourceOnDiaObject catalog.  

.. _DP0-2-Portal-5-Step-1:

Step 1. Set the query constraints and plot the single-band light curve from the ForcedSourceOnDiaObjects table 
==============================================================================================================

1.1.  Log in to the Portal Aspect of the Rubin Science Platform.  

1.2.  Click on "Edit ADQL" (advanced) button in the Select Query line.  Clear the content of the ADQL query box, if it is not empty.  

1.3.  Enter a different ADQL query than the one given in the Intrduction - the new query is below.  This query will retrieve all of the ForcedSourceOnDiaObjects table entries for the supernova for which we retrieved the DiaSource fluxes in the plot above.  

The ForcedSourceOnDiaObject contains forced photometry on both the difference image (psfDiffFlux, psfDiffFluxErr) 
and the processed visit image (PVI), also called the "direct" image (psfFlux, psfFluxErr).  Below, we retrieve both types of fluxes for our DiaObject.  
For starters, we will work with the psfFlux entries - furter down in the tutorial, we will explain the meaning and use of the psfDiffFlux.  

The JOIN command in this query is used for the ccdVisitId to join to the CcdVisit table to obtain the expMidptMJD (MJD of the mid-point of the exposure).  

.. code-block:: SQL 

   SELECT fsodo.coord_ra, fsodo.coord_dec, 
   fsodo.diaObjectId, fsodo.ccdVisitId, fsodo.band, 
   fsodo.psfDiffFlux, fsodo.psfDiffFluxErr, 
   fsodo.psfFlux, fsodo.psfFluxErr, 
   cv.expMidptMJD, 
   scisql_nanojanskyToAbMag(fsodo.psfFlux) AS fsodoAbMag,
   scisql_nanojanskyToAbMag(fsodo.psfDiffFlux) AS fsodoDiffAbMag
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo 
   JOIN dp02_dc2_catalogs.CcdVisit as cv 
   ON cv.ccdVisitId = fsodo.ccdVisitId 
   WHERE fsodo.diaObjectId = 1252220598734556212 
   AND fsodo.band = 'i'

1.3. Click "Search"

.. figure:: /_static/portal_tut05_step01a.png
    :name: portal_tut05_step01a

This query will return forced flux measurements at all epochs of Rubin visits to our supernova location, but to plot such a light curve (rather than the default of your table), you need to modify the settings of the plot by clicking the settings icon as above.  

.. figure:: /_static/portal_tut05_step01b.png
    :name: portal_tut05_step01b

Here, you need to request the appropriate columns:  

.. figure:: /_static/portal_tut05_step01c.png
    :name: portal_tut05_step01c
    
You night want to click on "xy-tbl" in the upper right hand part of the display.  Tthe his will result in a plot as below:  

.. figure:: /_static/portal_tut05_step01d.png
    :name: portal_tut05_step01d
    
Here, a warning is warranted:  converting fluxes from the ForcedSourceOnDiaObject table to magnitudes using the scisql_nanojanskyToAbMag() function can be dangerous.  This is because the nanojanskyToAbMag() function does not return any value for a negative flux as an argument, and thus any negative fluxes will be lost. This is especially important for variability studies, when a negative value of flux is (within errors) consistent with non-deection might be scientifically interesting.  

1.4.  If you wish, you can restrict the MJD range of your Forced Photometry search to the range covered in DiaObject shown in the Ingtroduction).  This will allow you to compare the light curves retrieved from the two tables.  You can do this by changing the plot parameters in the "chart settings" window such as 930 < MJD-60000 < 1010 - this will retun the plot below:  

.. figure:: /_static/portal_tut05_step01e.png
    :name: portal_tut05_step01e

Step 2.  The Distinction Between fsodo.psfFlux and fsodo.psfDiffFlux
====================================================================

Note that we plotted just the psfFlux on the plot above, but we extracted two fluxes - the psfFlux as well as the psfDiffFlux.  The former (plotted above) is essentially a measurement of a "forced" flux measurement at a specified location.   The psfDiffFlux is a flux determined by subtracting some fiducial flux from the psfFlux.  

Exercises for the learner
=========================

Add error bars to the lightcurves. Magnitude errors can be retrieved during the execution of the ADQL command, with, e.g., scisql_nanojanskyToAbMagSigma(psFlux, psFluxErr) as psAbMagErr.
