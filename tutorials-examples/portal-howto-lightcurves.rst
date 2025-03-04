.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-howto-lightcurves:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###############################
08.3. How to plot a light curve
###############################

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-03-04

**Targeted learning level:** intermediate

**Introduction:**
This tutorial demonstrates how to plot the light curve of a difference image analysis object (``diaObject``).
In this demonstration, an RR Lyrae star is used.
This star has coordinates RA, Dec = 62.1479031, -35.7991348 deg and an object identifier number ``diaObjectId`` = 1651589610221862935.
As is appropriate for variable stars, the forced photometry fluxes from PSF model fits in the direct (not difference) images are used.

**1. Execute the query.**
Go to the Portal's DP0.2 Catalogs tab, switch to the ADQL interface, and execute the query below.
The query will return the modified julian date (MJD) from the ``CcdVisitId`` table,
and the forced PSF flux on the direct image (``psfFlux``)
from the ``ForcedSourceOnDiaObject`` table, for the target star only.
It will also return the flux error and the band (filter) of the observation.

.. code-block:: SQL 

   SELECT cv.expMidptMJD, fsodo.psfFlux, fsodo.psfFluxErr, fsodo.band 
   FROM dp02_dc2_catalogs.ForcedSourceOnDiaObject as fsodo
   JOIN dp02_dc2_catalogs.CcdVisit as cv
   ON cv.ccdVisitId = fsodo.ccdVisitId
   WHERE fsodo.diaObjectId = 1651589610221862935


**2. The default plot is an all-filter light curve.**
The first two columns, date and flux, are plotted on the x- and y-axes of the default Active Chart for all filters (Figure 1).

.. figure:: /_static/portal-howto-lightcurves-1.png
    :name: portal-howto-lightcurves-1
    :alt: A screenshot of the default results view showing the light curve from all filters.

    Figure 1: The default results view showing the light curve with all filters as blue points.


**3. Plot a single-filter light curve.**
In the table header, in the "band" column, click on the constraint box and then select "i" in the pop-up window and click "Apply".
The plot will update to display i-band fluxes only (Figure 2).

.. figure:: /_static/portal-howto-lightcurves-2.png
    :name: portal-howto-lightcurves-2
    :alt: A screenshot of the results view with only i-band data selected.

    Figure 2: The results view with only i-band data selected and plotted.


**4. Color markers by band in a multi-band light curve.**
To set marker color based on band (filter),
create a new column in which the band is represented as a number (Figure 3)
and then a color map based on those numbers (Figure 4).
The plot will then display points colored by band (Figure 5).

.. figure:: /_static/portal-howto-lightcurves-3.png
    :name: portal-howto-lightcurves-3
    :width: 300
    :alt: A screenshot of the "Add a column" pop-up window.

    Figure 3: The "Add a column" pop-up window to create a new column of integer numbers to represent each band.


.. figure:: /_static/portal-howto-lightcurves-4.png
    :name: portal-howto-lightcurves-4
    :alt: A screenshot of the "Plot Parameters" pop-up window.

    Figure 4: The "Plot Parameters" pop-up window with the Trace Options set to define a color map based on the new "bands_ascii" column.


.. figure:: /_static/portal-howto-lightcurves-5.png
    :name: portal-howto-lightcurves-5
    :alt: A screenshot of the results view with plotted points colored by band.

    Figure 5: The results view with the new "bands_ascii" column and the plotted points colored by the Rainbow color map.


**Notice: **
In the future, the trick of creating an ascii column to represent band as an integer will not be needed.
The development of Portal functionality to plot multi-band light curves in which points are colored by filter is planned.

Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.


