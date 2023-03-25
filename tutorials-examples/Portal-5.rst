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

#################################################################
05.  Measuring the Light Curve of an Object via Forced Photometry
#################################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham and Greg Madejski

**Last verified to run:** 2023-03-24

**Targeted learning level:** intermediate 

**Introduction:**
Generally, the DiaSource table can be used to plot light curves, but it only includes detections with SNR > 5 in the difference images. 
If your science goal requires lower-SNR measurements (e.g. including fluxes of a given object measured during all visits to its location, for instance before and after a flare or explosion), then one can use the forced photometry in the ForcedSourceOnDiaObjects table instead.  

Let's say there is a specific object whose DiaSource light curve looks particularly interesting. 
In order to explore the flux of the object in all sets of differences images, one can use the 
ForcedSourceOnDiaObject catalog.  The Table in this catalog contains point-source forced-photometry measurements on individual 
single-epoch visit images and difference images, based on and linked to the entries in the DiaObject table.  
We will use the JOIN command to the CcdVisit table to obtain the exposure time mid-point in the 
Modified Julian Date (MJD) format (expMidptMJD)

In this tutorial, we will first examine the light curve of the supernova we considered in Portal Tutorial 02, one with the DiaObjectId "1252220598734556212" -- using the DiaSource table.  We will follow with examining its flux history in the ForcedSourceOnDiaObjects table.  We will employ the Astronomical Data Query Language (ADQL) to query and retrieve the data.  

For more information, see the schema of the ForcedSourceOnDiaObject catalog.

.. _DP0-2-Portal-5-Step-1:

Step 1. Set the query constraints and plot the light curve from the DiaSource table
===================================================================================

1.1.  Log in to the Portal Aspect.

1.2.  Click on "Edit ADQL (advanced)" button.  

1.3.  Enter the same ADQL query which was used in Portal Tutorial 02 - namely 

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

1.4. Click "Search"

.. figure:: /_static/portal_tut05_step01a.png
    :name: portal_tut05_step01a


This will return the results as on the screenshot below.  

.. figure:: /_static/portal_tut05_step01b.png
    :name: portal_tut05_step01b

1.5.  You can modify the content of the plot on the upper right-hand side, by clicking the settings icon (two gears as marked on the screenshot above).    Once you clicked on it, you can modify trace as shown on the screenshot below.  Note that the scisql_nanojanskyToAbMag function is smart enough not to return any value when the argument of flux is negative.  

.. figure:: /_static/portal_tut05_step01c.png
    :name: portal_tut05_step01c
    
Clicking on "Apply" will result in the screen as below:  

.. figure:: /_static/portal_tut05_step01d.png
    :name: portal_tut05_step01c


This will plot the apparent magnitude of the object as a function of time.  This looks interesting enough that you might wish to follow up with Forced Photometry!  Can you detect the progenitor prior to the explosion?  

Step 2. Set the query constraints and plot the light curve from the ForcedSourceOnDiaObjects table 
==================================================================================================

2.1.  Click on "Edit ADQL" (advanced) button, as above.  Clear the content of the ADQL query box, if it is not empty.  

2.2.  Enter a different ADQL query this time, namely  

.. code-block:: SQL 

   SELECT fsodo.coord_ra, fsodo.coord_dec, 
   fsodo.diaObjectId, fsodo.ccdVisitId, fsodo.band, 
   fsodo.psfDiffFlux, fsodo.psfDiffFluxErr, 
   fsodo.psfFlux, fsodo.psfFluxErr, 
   cv.expMidptMJD, 
   scisql_nanojanskyToAbMag(fsodo.psfFlux) AS fsodoAbMag,
   scisql_nanojanskyToAbMag(fsodo.psfDiffFlux) AS fsodoDiffAbMag
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo 
   JOIN dp02_dc2_catalogs.CcdVisit as cv ON cv.ccdVisitId = fsodo.ccdVisitId 
   WHERE fsodo.diaObjectId = 1252220598734556212 
   AND fsodo.band = 'i'

2.3. Click "Search"

.. figure:: /_static/portal_tut05_step02a.png
    :name: portal_tut05_step02a

This query will return forced flux measurements at all epochs of Rubin visits to our supernova location, but to plot such a light curve (rather than the default  of your table), you need to modify the settings of the plot by clicking the settings icon as above.  

.. figure:: /_static/portal_tut05_step02b.png
    :name: portal_tut05_step02b

Here, you need to request the appropriate columns:  

.. figure:: /_static/portal_tut05_step02c.png
    :name: portal_tut05_step02c
    
This will result in a plot as below:  

.. figure:: /_static/portal_tut05_step02d.png
    :name: portal_tut05_step02d

2.4.  Restrict the MJD range of your Forced Photometry search to the range covered in DiaObject, to compare the light curves retrieved from the two tables by changing the plot parameters in the "chart settings" window such as 930 < MJD-60000 < 1010 - this will retun the plot below:  

.. figure:: /_static/portal_tut05_step02e.png
    :name: portal_tut05_step02e

2.5.  Possbly plot two traces on the same plot - one with fsodoAbMag and another with fsodoDiffAbMag ?

Exercises for the learner
=========================

Add error bars to the lightcurves. Magnitude errors can be retrieved during the execution of the ADQL command, with, e.g., scisql_nanojanskyToAbMagSigma(psFlux, psFluxErr) as psAbMagErr.
