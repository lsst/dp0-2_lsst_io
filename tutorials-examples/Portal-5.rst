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

Step 1. Plot a single-band lightcurve 
=====================================

This first step is a repeat of Portal Tutorial 02, and can be skipped.

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
Click "Apply".

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

Step 2.  Plot a multi-band lightcurve
=====================================

**WARNING:** The Portal does not yet have the built-in functionality to plot a multi-band lightcurve (i.e., to color lightcurve points
by their bandpass and add a legend).
What follows is a demonstration of a temporary work-around for Portal users: convert the band (u, g, r, i, z, or y) into an
ASCII value (e.g., 121, 114, 105) and then set a colorbar for the points based on these values.
For the Notebook Aspect, see tutorial notebook 07a and 07b for multi-band lightcurve demonstrations.

2.1. Return to (or start at, if Step 1 was skipped) the ADQL Query interface and enter the query below.
Note that the only difference here compared to Step 1 is that the last line (``AND fsodo.band = 'i'``) is missing,
so that data for all bands will be returned.

.. code-block:: SQL 

   SELECT fsodo.coord_ra, fsodo.coord_dec, 
   fsodo.diaObjectId, fsodo.ccdVisitId, fsodo.band, 
   fsodo.psfDiffFlux, fsodo.psfDiffFluxErr, 
   cv.expMidptMJD
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo 
   JOIN dp02_dc2_catalogs.CcdVisit as cv 
   ON cv.ccdVisitId = fsodo.ccdVisitId 
   WHERE fsodo.diaObjectId = 1252220598734556212 

2.2. Follow steps 1.4, 1.5, and 1.6 to plot the multi-band lightcurve with identical color markers for all bands. 
The plot will appear as in the right hand side of the figure below. 
Note that there are many more points on the new plot, because all bands are included instead of just i-band.

2.3. The work-around to convert the band (u, g, r, i, z, or y) into an ASCII value (e.g., 121, 114, 105) starts with
adding a column, and setting it to be the ASCII value of the ``band`` column.
To add a new column, click the 5th icon in the results table (the vertical rectangle with a + sign), as shown in the figure below.  

.. figure:: /_static/portal_tut05_step02a.png
    :name: portal_tut05_step02a
    :alt: The results view table, with a red arrow pointing to the icon to add a column.

2.4. In the "Add a column" pop-up window, enter a name for the new column (``bands_ascii``) and the expression to convert
the character in column ``band`` into its ASCII value: ``ascii("band")``. 
Set the "Data Type" to long, then click on "Add column", as shown in the figure below.  

.. figure:: /_static/portal_tut05_step02b.png
    :width: 300
    :name: portal_tut05_step02b
    :alt: A screenshot of the pop-up window for adding a new column that is the ascii for the band.

2.5. In the results view, see the new column in a numeric format: the corresponding ASCII value of the character in the ``band`` column.
In the figure below, the new column named ``bands_ascii`` is marked with a red arrow labeled with the number one.

.. figure:: /_static/portal_tut05_step02c.png
    :name: portal_tut05_step02c
    :alt: A screenshot of the results view page showing a new column named bands_ascii.

2.6. Set the colorbar for the points based on the values in the new column ``bands_ascii``. 
Open the "Plot Parameters" pop-up window by clicking on the settings icon 
(marked with a red arrow labeled with the number two in the figure above).
Under "Trace Options" "bands_ascii" for the "Color Map" and "Rainbow" for the "Color Scale", as shown in the figure below.
Click "Apply".

.. figure:: /_static/portal_tut05_step02d.png
    :width: 300
    :name: portal_tut05_step02d
    :alt: A screenshot of the plot parameters pop-up window that shows the trace options set for a rainbow colorscale based on the new column of ascii values.

2.7. View the new version of the lightcurve with the points colored by band, as in the figure below.
Use the mouse to hover-over points in the plot, and notice that the pop-up info box for a given point includes only the
data included in the plot: x-axis value, y-axis value, and the ``bands_ascii`` value. 

.. figure:: /_static/portal_tut05_step02e.png
    :name: portal_tut05_step02e
    :alt: A screenshot of the results table and the multi-band lightcurve with points colored by band.
    
2.8. Restrict the multi-band lightcurve back down to a single filter without redoing the ADQL query.
Apply a filter to the ``band`` column of the table by entering ``= 'r'`` into the box below the header row (top of the column), 
and press enter (or return) on the keyboard (see the table view figure below).
Do it again for ``= 'g'``, and notice that the points are different, but are green both times.
The point colors are not assigned in an absolute sense, but rather the color scaling is reapplied every time the plot changes.

2.9. Restrict the multi-band lightcurve to two filters by entering ``= 'r' or 'i'``. 
See how the point colors are orange and mauve (as in the figure below). 

.. figure:: /_static/portal_tut05_step02f.png
    :name: portal_tut05_step02f
    :alt: A screenshot of the results table and a two-band lightcurve.

**Note:** While not being able to choose your own symbols or colors for data points on the plot is a temporary drawback
of the Portal, the future releases will bring improved functionality.


.. _DP0-2-Portal-5-Step-3:  

Step 3.  Exercises for the learner
==================================

3.1. Add error bars to the lightcurve. 

3.2. Try another supernova and follow the steps above (e.g., use ``diaObjectId = 1250953961339360185``).
