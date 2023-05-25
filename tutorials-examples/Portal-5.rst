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

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2023-05-24

**Targeted learning level:** intermediate 

**Introduction:**
In Portal Tutorial 02, a supernova lightcurve was plotted using the measurements in the ``DiaSource`` table,
but the ``DiaSource`` table only contains measurements when the supernova is detected with ``SNR > 5`` 
in the difference image.
If your science goal requires lower-SNR measurements (e.g. including fluxes of a given object measured during all visits to its location, 
for instance before and after a flare or explosion), then use the forced photometry in the ``ForcedSourceOnDiaObject`` table instead.  

This tutorial demonstrates how to create a forced photometry lightcurve for the same supernova used in
Portal Tutorial 02, which has a ``DiaObjectId`` of ``1252220598734556212``.

.. _DP0-2-Portal-5-Step-1:

Step 1. Plot the single-band lightcurve 
=======================================

1.1. Log in to the Portal Aspect of the Rubin Science Platform.  

1.2. At upper right on the main Portal user interface, click "Edit ADQL" to switch to the ADQL query view.
(In the figure below, see the red arrow labeled number one).
Clear the content of the ADQL query box, if it is not empty.  

.. figure:: /_static/portal_tut05_step01a.png
    :name: portal_tut05_step01a
    :alt: A screenshot of the ADQL Query view of the Portal user interface.

1.3. In the ADQL Query box, enter the query as below.
This query will retrieve the coordinates, DIA object identifier, CCD visit identifier, band, and forced difference-image flux 
and its error for all rows of the ``ForcedSourceOnDiaObjects`` table which are associated with the ``diaObject`` of interest,
for i-band visits only.
It also retrieves the exposure time midpoint modified julian date for all visits by joining to the ``CcdVisit`` table.

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

**Note:** The ``ForcedSourceOnDiaObject`` table contains forced photometry on both the difference image, 
``psfDiffFlux``, and the processed visit image (PVI; "direct" image), ``psfFlux``.
As this tutorial is using a supernova it uses the ``psfDiffFlux``, which is the forced photometry on the difference image,
in which the static-sky component (the host galaxy) has been subtracted.
However, the ``psfFlux`` would be more appropriate for generating the lightcurve of a variable star, as there is no
need to subtract the static component (in this case, the variable star's average flux).

**WARNING:** Do not use the ADQL function ``scisql_nanojanskyToAbMag()`` to convert difference image fluxes to magnitudes.
This is very dangerous! 
This function does not return any value for a negative flux, and difference image fluxes can be negative (e.g., either the
object has declined in brightness compared to the template, or it is a non-detection and the flux is very small and negative).
Using the ``scisql_nanojanskyToAbMag()`` function on columns like ``psfDiffFlux`` can result in missing data.
While it is generally safe to convert forced fluxes from the PVI to magnitudes, there might be edge cases where the direct image
forced photometry is negative 
(e.g., rare cases where the source is faint or gone *and* in a region of slightly oversubtracted sky background).
It is only ever fully safe to use this function when using ``SNR > 5`` *detections* in PVIs.

1.4. Click "Search". (In the figure above, see the red arrow labeled number two).  

1.5. In the results view, see that the query has returned forced flux measurements in the table (bottom of the figure below).
To plot the lightcurve instead of the default xy plot of RA vs. Dec, open the plot parameters pop-up window by clicking on 
the settings icon (double gears, as the red arrow points in the figure below).  

.. figure:: /_static/portal_tut05_step01b.png
    :name: portal_tut05_step01b
    :alt: A screenshot of the default results view that is returned for the query.

1.6. Update the plot parameters as shown in the figure below.
Note that the grid line in the y-axis is selected.

.. figure:: /_static/portal_tut05_step01c.png
    :width: 300
    :name: portal_tut05_step01c
    :alt: A screenshot of the plot parameters pop-up window, with the parameters set to display the i-band lightcurve.
    
1.7. Remove the sky image panel of the results view by clicking on the "Bi-view Tables" button at upper right in the figure below.
Note how the grid lines in the y-axis illustrate that "off-peak" (non-detection) forced fluxes can be negative.  

.. figure:: /_static/portal_tut05_step01d.png
    :name: portal_tut05_step01d
    :alt: A screenshot of the results view showing only the table and the i-band lightcurve.
    
1.8.  Restrict the x-axis (MJD range) to only show the lightcurve around the dates of peak brightness:
reopen the plot parameters pop-up window, and under Chart Options set the ``X Min`` to be 930 and ``X Max`` to be 1010.
The result can be directly compared to the lightcurve in Portal Tutorial 2.  

.. figure:: /_static/portal_tut05_step01e.png
    :name: portal_tut05_step01e
    :alt: A screenshot of the results view in which the lightcurve date range has been limited.
    
**Note:** A statistical analysis of the lightcurve (e.g., goodness-of-fit to a template; timeseries features) is currently not possible
in the Portal, and should be done in the Notebook Aspect.

.. _DP0-2-Portal-5-Step-2: 

Step 2.  Making a multi-band lightcurve on a single plot
========================================================

Our goal here is to plot a multi-band lightcurve with flux measurements in different bands appearing in different colors on the same plot.  
This is not currently supported by the Portal functionality, but is in the Portal development plan, to be implemented in the future.  
Beyond various bands appearing in different colors, it is envisioned that it will be possible to add a legend in the plot.  
However, currently there is a relatively simple workaround - see below for the necessary steps (but if needed for e.g. making the plot publication-ready, the legend needs to be added separately).  

2.1. We will start with the same ADQL query as previously, but with the last line (specifically, ``AND fsodo.band = 'i'``) missing (meaning we will not select just the i-band data).  Start with entering the query below into the ADQL query box:  

.. code-block:: SQL 

   SELECT fsodo.coord_ra, fsodo.coord_dec, 
   fsodo.diaObjectId, fsodo.ccdVisitId, fsodo.band, 
   fsodo.psfDiffFlux, fsodo.psfDiffFluxErr, 
   cv.expMidptMJD
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo 
   JOIN dp02_dc2_catalogs.CcdVisit as cv 
   ON cv.ccdVisitId = fsodo.ccdVisitId 
   WHERE fsodo.diaObjectId = 1252220598734556212 

2.2.  First, we can plot the multi-band lightcurve with identical color markers for all bands, following the steps outlined in Step 1.5 to plot flux vs. MJD.  
This will return the plot as on the right hand side of the screenshot below.  
Note that there are many more points on the plot than you had in Step 1 - this is because you didn't restrict the ADQL search to only i-band but chose all bands.  

2.3  To distinguish various bands in the lightcurve, one can use the following trick:  one can add an additional column to the table generated in the previous search.  
This new column would be an ASCII value of the "band" entry, which is currently in the "character" format.  
To add a new column in the table, one needs to click on the 5th icon in the retrieved table, as below.  

.. figure:: /_static/portal_tut05_step02a.png
    :name: portal_tut05_step02a

This brings a new window, where you should enter a new name of the column (here it is "bands_ascii") and enter an expression converting the character in the "band" column to its ASCII value, namely ``ascii("band")``.  
It is also necessary to specify the data type - it needs to be "long" - see the screenshot below.  
Click on "Add column" as below:  

.. figure:: /_static/portal_tut05_step02b.png
    :name: portal_tut05_step02b

2.4.  Clicking on "Add Column" will result in a new column in a numeric format, corresponding to the ASCII value of the character in the "band" column (now the rightmost column on the screenshot below, marked with (1)).  

.. figure:: /_static/portal_tut05_step02c.png
    :name: portal_tut05_step02c

2.5.  Now in order to have data in various filters appear in different colors, you need to change the plot parameters by clicking the two gears (marked as a red arrow with "(2)" above).  
This brings a window as below, where you need to click on "Trace Options" and enter "bands_ascii" in the "Color Map" line, and "Rainbow" in the "Color Scale" line.  

.. figure:: /_static/portal_tut05_step02d.png
    :name: portal_tut05_step02d

Once you click on "Apply" - you will see the plot of the supernova lightcurve in various bands.  

.. figure:: /_static/portal_tut05_step02e.png
    :name: portal_tut05_step02e
    
Note that the colors displayed above are arbitrarily assigned to a given ascii value for each filter.  
You can hover over the individual points on the plot, and the displayed values will be the ascii value of the data point, and not the filter.  

2.6  Now you can select data obtained by a single filter or combination of filters without re-issuing the ADQL query.  
You can constrain it to display only e.g. the r-band filter data by inserting "r" into the little box below the headng of the "band" column on the table on the left, and pressing return.  
Note that the color of data points on the plot for a single filter will always appear in green.  
You can select multiple filters (say "r" in addition to "i") via inserting "r OR i" - this will always display the data points in orange and mauve (see below).  
While not being able to choose your own symbols  or colors for data points on the plot is a drawback, the future releases of the Portal will bring further improvements.  

.. figure:: /_static/portal_tut05_step02f.png
    :name: portal_tut05_step02f

.. _DP0-2-Portal-5-Step-3:  

Step 3.  Exercises for the learner
==================================

3.1.  Add error bars to the lightcurves. 

3.2.  Try another supernova and follow the steps above: you can try one with the ObjectId ``1250953961339360185``.  
