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
If your science goal requires lower-SNR measurements (e.g. including fluxes of a given object measured during all visits to its location, 
for instance before and after a flare or explosion), then one can use the forced photometry in the ForcedSourceOnDiaObjects table instead.  

Let's say there is a specific object whose DiaSource light curve looks particularly interesting. 
In order to explore the flux of the object in all sets of single-epoch visit images as well as difference images, one can use the 
ForcedSourceOnDiaObject catalog.  The table in this catalog contains point-source forced-photometry measurements on individual 
single-epoch visit images and difference images, based on and linked to the entries in the DiaObject table.  We will use an ADQL query, where 
we will use the JOIN command to the CcdVisit table to obtain the exposure time mid-point in the 
Modified Julian Date (MJD) format (expMidptMJD).  

In this tutorial, we will create a Forced Photometry light curve of the supernova we considered in Portal Tutorial 02, one with the DiaObjectId "1252220598734556212".  

.. _DP0-2-Portal-5-Step-1:

Step 1. Plot the single-band light curve 
========================================

1.1.  Log in to the Portal Aspect of the Rubin Science Platform.  

1.2.  Click on "Edit ADQL" (advanced) button in the Select Query line.  Clear the content of the ADQL query box, if it is not empty.  

1.3.  Enter the query as below.  This query will retrieve all of the ForcedSourceOnDiaObjects table entries for the supernova (and convert the fluxes into magnitudes) in the plot made in Portal Tutorial 02.  

The ForcedSourceOnDiaObject contains forced photometry on both the difference image (psfDiffFlux, psfDiffFluxErr) 
and the processed visit image (PVI), also called the "direct" image (psfFlux, psfFluxErr).  For our specific ("supernova") application, we 
want to use the psfDiffFlux.  Specifically, the psfDiffFlux is a differential flux 
determined by measuring the flux from a difference image and therefore automatically removes the flux of the host galaxy of the supernova.  Note that since 
psfDiffFlux is a difference flux, it can go negative, and it will be apparent in a screenshot in one of the subsequent steps.  On the 
other hand, if you are interested in measuring the flux history of a variable star, you shouldn't use psfDiffFlux - this is 
becasue psfDiffFlux will subtract the average component of the star's flux.  For such application, you should use psfFlux.  

Here, another warning is warranted:  converting fluxes from the ForcedSourceOnDiaObject table to magnitudes using the scisql_nanojanskyToAbMag() function 
can be dangerous and should not be used.  This is because the scisql_nanojanskyToAbMag() function does not return any value for a negative flux as an argument, 
and thus any negative fluxes will be lost. This is especially important for variability studies, when a negative value of flux is (within errors) 
consistent with non-detection might be scientifically interesting.  However, it is OK to 
convert fluxes extracted from psfFlux entry in the ForcedSourceOnDiaObject table to magnitudes using the scisql_nanojanskyToAbMag() as such fluxes are always positive.  
Just for illustration of the scisql_nanojanskyToAbMag() function, we extract the psfFlux and psfFluxErr entries, but we will not use those in ths Tutorial.  

The JOIN command in this query is used for the ccdVisitId to join to the CcdVisit table to obtain the expMidptMJD (MJD of the mid-point of the exposure).  

.. code-block:: SQL 

   SELECT fsodo.coord_ra, fsodo.coord_dec, 
   fsodo.diaObjectId, fsodo.ccdVisitId, fsodo.band, 
   fsodo.psfDiffFlux, fsodo.psfDiffFluxErr, 
   cv.expMidptMJD
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo 
   JOIN dp02_dc2_catalogs.CcdVisit as cv 
   ON cv.ccdVisitId = fsodo.ccdVisitId 
   WHERE fsodo.diaObjectId = 1252220598734556212 
   AND fsodo.band = 'i'

1.4. Click "Search"

.. figure:: /_static/portal_tut05_step01a.png
    :name: portal_tut05_step01a

1.5.  This query will return forced flux measurements at all epochs of Rubin visits to our supernova location, but to plot such a light curve (rather than the default of your table), you need to modify the settings of the plot by clicking the settings icon as below.  

.. figure:: /_static/portal_tut05_step02a.png
    :name: portal_tut05_step02a

Here, you need to request the appropriate columns and provide axis labels:   

.. figure:: /_static/portal_tut05_step02b.png
    :name: portal_tut05_step02b
    
You might want to click on "xy-tbl" in the upper right hand part of the display.  This will result in a plot as below.  Note that we requested a grid line on "y" to illustrate that "off-peak" (non-detection) points can be negative, resulting by the subtraction of two images.  

.. figure:: /_static/portal_tut05_step02c.png
    :name: portal_tut05_step02c
    
1.6.  If you wish, you can restrict the MJD range of your Forced Photometry search to the range covered in DiaObject.  This will allow you to compare the light curve you've retrieved vis-a-vis the one in Portal Tutorial 2.  You can do this by changing the plot parameters in the "Plot Parameters" window (in Chart Options) such as X Min = 930, X Max = 1010 - this will return the plot below:  

.. figure:: /_static/portal_tut05_step02d.png
    :name: portal_tut05_step02d
    
Note that a statistical analysis of the data you've extracted (such as fitting to a temporal template, or subset statistics) is currently not possible, but future versions of the Portal might allow for some such functions.  

.. _DP0-2-Portal-5-Step-2: 

Step 2.  Making a multi-band light curve on a single plot
=========================================================

2.1.  Our goal here is to plot a multi-band light curve with flux measurements in different bands appearing in different colors on the same plot.  This is not currently supported by the Portal functionality, but is in the Portal development plan, to be implemented in the future.  Beyond various bands appearing in different colors, it is envisioned that it will be possible to add a legend in the plot.  However, currently there is a relatively simple workaround - see below for the necessary steps (but if needed for e.g. making the plot publication-ready), legend needs to be added separately.  

2.2. We will start with the same query as previously, but with the last line (specifically, AND fsodo.band = 'i') missing (meaning we will not select just the "i" band data).  First, we can plot the multi-band light curve with identical color markers for all bands, following the steps outlined in Step 2.1 to plot flux vs. MJD.  This will return the plot as on the top of the screenshot below.  Note that there are many more points on the plot than you had in Step 2 - this is because you didn't restrict the ADQL search to only band "i."  

2.3  To distinguish various bands in the lightcurve, one can use the following trick:  one can add an additional column to the table generated in the previous search.  This new column would be an ASCII value of the "band" entry, which is currently in the "character" format.  To add a new column in the table, one needs to click on the 5th icon in the retrieved table, as below.  

.. figure:: /_static/portal_tut05_step03a.png
    :name: portal_tut05_step03a

This brings a new window, where you should enter a new name of the column (here it is "bands_ascii") and enter an expression converting the character in the "band" column to its ASCII value, namely ASCII("band").  It is also necessary to specify the data type - it needs to be "long" - see the screenshot below.  Click on "Add column" as below:  

.. figure:: /_static/portal_tut05_step03b.png
    :name: portal_tut05_step03b

2.4.  Clicking on "Add Column" will result in a new column in a numeric format, corresponding to the ASCII value of the character in the "band" column (now the rightmost column on the screenshot below, marked with (1)).  

.. figure:: /_static/portal_tut05_step03c.png
    :name: portal_tut05_step03c

2.5.  Now in order to have data in various filters appear in different colors, you need to change the plot parameters by clicking the two gears (marked as a red arrow with "(2)" above).  This brings a window as below, where you need to click on "Trace Options" and enter "bands_ascii" in the "Color Map" line, and "Rainbow" in the "Color Scale" line.  

.. figure:: /_static/portal_tut05_step03d.png
    :name: portal_tut05_step03d

Once you click on "Apply" - you will see the plot of the supernova light curve in various bands.  

.. figure:: /_static/portal_tut05_step03e.png
    :name: portal_tut05_step03e

Exercises for the learner
=========================

Add error bars to the lightcurves. Magnitude errors can be retrieved during the execution of the ADQL command, with, e.g., scisql_nanojanskyToAbMagSigma(psFlux, psFluxErr) as psAbMagErr.
