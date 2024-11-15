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

#####################################################
How to extract and plot forced photometry light curve
#####################################################

The Rubin data set readily provides fluxes of the objects where they were detected at a ``SNR > 5``.  In some cases, the 
science goal on-hand requires lower-SNR measurements.  This might be the case when fluxes of a given object measured during all visits to its location are required.  
A good example would be a measurement of a source flux before and after a flare or explosion.  
In those cases, the forced photometry - available in the ``ForcedSourceOnDiaObject`` table - has to be used instead.  

This tutorial demonstrates how to create a forced photometry lightcurve for the same supernova used in
Portal Tutorial 02, which has a ``DiaObjectId`` of ``1252220598734556212``.

**1.1.** Log in to the Portal Aspect of the Rubin Science Platform, and select "DP0.2 Catalogs" tab.  

**1.2.** At upper right on the main Portal user interface, click "Edit ADQL" to switch to the ADQL query view.
(In the figure below, see the red arrow.)  
Clear the content of the ADQL query box, if it is not empty.  

.. figure:: /_static/portal_tut05_step01a.png
    :name: portal_tut05_step01a
    :alt: A screenshot of the ADQL Query view of the Portal user interface.

    Figure 1: RSP Portal aspect with "DP0.2 catalogs" selected.

**1.3.** In the ADQL Query box, enter the query as below.
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

**1.4.** Click "Search".  

**1.5.** Set the view of the "Results" panel by clicking on the "hamburger" icon (three horizontal lines on the top left).  
Click on the double-arrow in the "Results Layout" box, and click on the "Coverage Charts Tables" box.  
In the results view, see that the query has returned forced flux measurements in the table (right hand side of the figure below), and the "coverage" panel on the left-hand side.  

.. figure:: /_static/portal_tut05_step01b.png
    :name: portal_tut05_step01b
    :alt: A screenshot of the default results view that is returned for the query.

    Figure 2: Screenshot illustrating the results of the query, with the selection of "coverage" on the left, and "table" on the right.

**1.6.**  To plot the lightcurve instead of the "coverage" image (default), click on the "Active Chart" tab.  
The defalt plot will be the dec vs. RA (the plotting chart defaults to plot the data in the two leftmost columns of the table).  
To change the plot, open the plot parameters pop-up window by clicking on 
the settings icon (a single gear above the plot window).  


**1.7.** Update the plot parameters as shown in the figure below.
Note that the grid line in the y-axis is selected.
Click "Apply".  
Note how the grid lines in the y-axis illustrate that "off-peak" (non-detection) forced fluxes can be negative.  

.. figure:: /_static/portal_tut05_step01c.png
    :width: 300
    :name: portal_tut05_step01c
    :alt: A screenshot of the plot parameters pop-up window, with the parameters set to display the i-band lightcurve.

    Figure 3: Plot parameters selection in the pop-up window, set to display the i-band lightcurve.

.. figure:: /_static/portal_tut05_step01d.png
    :name: portal_tut05_step01d
    :alt: A screenshot of the results view showing the table and the i-band lightcurve.

    Figure 4: Results view showing the table and the i-band light curve.
