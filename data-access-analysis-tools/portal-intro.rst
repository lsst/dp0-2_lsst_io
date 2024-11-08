.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.

.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

############################################################################
How to make a lightcurve of a clearly detected object with known coordinates
############################################################################

.. This section should provide a brief, top-level description of the page.

.. Most recent update:  November 7 2024

The Portal aspect of the Rubin Science Platform lends itself well to extracting and plotting a light curve of an object with known coordinates.
It can be accessed by clicking on the "Portal" panel on the main landing page at data.lsst.cloud.

Plotting of a light curve requires a data table which contains the obervation time.
For the simulated DP0.2 data, such table is the dp02_dc2_catalogs.DiaSource.
This table can be accessed by selecting ``DP0.2 Catalogs`` tab on the left-hand side, and the ``dp02_dc2_catalogs.DiaSource`` tab on the right.

An example here considers a low-redshift SNIa (67.4579, -44.0802) and will extract the flux data from that location only when the object was detected at ``SNR > 5``.
Such flux is derived from the processed visit image (PVI; “direct” image), ``psfFlux``.
If the flux of the object at epochs when the ``SNR < 5`` is needed, a different table using forced photometry (``ForcedSourceOnDiaObject``) needs to be used and this is covered in another "HowTo" bit.

Selecting the data for the object of interest will require entering the object coordinates in the "Spatial" constraints on the left, selecting the "Cone shape" button and a 2 arcseconds radius.  

For the output column, selection of the ``midPointTai`` will yield the time of the observation, ``psFlux`` will give the flux, and ``filterName`` will provide the filter used for the observation.
Pressing on the "funnel" icon will restrict the gtable on the right to show only the selected entries.

.. figure:: /_static/portal_tut02_step01a.png
..  :name: portal_tut02_step01a
..  :alt: Screenshot of RSP portal start page where the user can select table and constraints

**Screenshot of RSP portal start page with the selected constraaints and required output columns.**

Pressing the "Search" button will execute the search, resulting in the three-panel display.  

The right-hand plot, by default, will plot the first two columns of the table.
To plot the flux against time, it is necessary to click on the "gear" icon, and select the "midPointTai-60000" for X and "psFlux" for Y as shown below.  

.. figure:: /_static/portal_tut02_step01a.png
..  :name: portal_tut02_step01a
..  :alt: Screenshot of RSP portal start page where the user can select table and constraints

**Screenshot of RSP portal start page with the selected constraaints and required output columns.**

.. figure:: /_static/portal_tut02_step01a.png
..  :name: portal_tut02_step01a
..  :alt: Screenshot of RSP portal start page where the user can select table and constraints

**Screenshot of RSP portal start page with the selected constraaints and required output columns.**

Note that the resulting plot on the right-hand side displays flux in all filters.
It is possible to restrict the flux from a single filter by clicking the down-arrow under the "filterName" column heading in the table on the bottom, and selecting only the desired filter, say "r".  

.. _DP0-2-Portal-Intermediate_Step-2:

2. Query the DiaSource table
============================

**2.1.** Clear the previous search and return to the main Portal interface (use the "DP0.2 Catalogs" tab on top of your screen).

**2.2.** Select "View" as "Edit ADQL", enter the following ADQL query.
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

**2.3.** Click "Search".


.. _DP0-2-Portal-Intermediate_Step-3:

3. Make the three plots
=======================

**3.1.** The default Results view will show three panels including a sky image at upper left, a scatter plot of decl vs. ra on the right, and the table listing the pointings on the bottom.  To change the layout displayed on the screen, click the "hamburger" (three short lines) icon at the top left.

**3.2.** Scroll down to 'Results Layout', and click the double arrow to get a selection of layouts for the result.  For this step in this tutorial, select "Tables/Coverage Charts" option. Toggle into "Active Chart" from "Coverage" on the tab in the right side image box.  The table on the right-hand side is likely to crowd your plotting area, especially when you are displaying multiple plots.  Expand the plotting area by clicking on the dividing line between the two windows and moving it to the left.  

Use the settings icon (a gear at upper right) to open the plot parameters pop-up window, match those shown below, then click "Apply" and "Close".  

.. figure:: /_static/portal_tut02_step03a.png
    :width: 300
    :name: portal_tut02_step03a
    :alt: Plot parameters pop-up window, user can select various parameters then click apply and close to generate a light curve.


**Plot parameters for the lightcurve.**


**3.3.** View the i-band lightcurve for this SNIa.

.. figure:: /_static/portal_tut02_step03b.png
    :name: portal_tut02_step03b
    :alt: Image of the i-band lightcurve for the supernova being investigated.


**The i-band lightcurve for the SNIa of interest.**


**3.4.** To add a plot of seeing versus time: click on the "+" sign on the upper-left corner of the active chart, and match the parameters shown below, then click "OK".

.. figure:: /_static/portal_tut02_step03c.png
    :width: 300
    :name: portal_tut02_step03c
    :alt: Screenshot for dialog box to add a new chart, user can select parameters and click okay to generate a new plot.

**Plot parameters for the seeing versus time plot.**

**3.5.** To add a plot to visualize the astrometric scatter:  again, click on the "+" sign on the upper-left corner of the active chart, and match the parameters shown below, then click "OK".
Note that in both the X and Y parameters, the difference between the DiaSource coordinate and the DiaObject coordinate are multiplied by 3600, so that the plot axes are in arcseconds: ``((ra-67.4579634)*cos(decl*(pi()/180)))*3600`` and ``(decl+44.080243)*3600``.

.. figure:: /_static/portal_tut02_step03d.png
    :width: 300
    :name: portal_tut02_step03d
    :alt: Dialog box to add plot parameters for an astrometric scatter plot.

**Plot parameters for the astrometric scatter plot.**

**3.6.** View all three plots together.
Plots might appear in a different order than as shown in the figure below.
In the plot labeled "seeing", click on the i-band epoch with the best seeing (0.75 arcsec).
Notice how the point turns orange in all three plots, and that the corresponding table row will be highlighted.

In the lightcurve plot, notice that for this "best-seeing" epoch the SNIa had an apparent magnitude near its peak (around 22nd mag).
That makes it a suitable choice for the scientific use-case outlined in the Introduction.

In the plot showing the astrometric scatter, notice that for this "bright / best-seeing" epoch the measured sky coordinates of the DiaSource are very close to those reported for the DiaObject.  
This *does not* necessarily mean that the coordinates for the "best-seeing" epoch are more accurate, because the
coordinates of DiaObjects are *derived from* the individual DiaSources.
The point of this plot is more that the overall scatter is less than 0.3 arcsec, and that selecting the
"bright / best-seeing" epoch image for co-registration with images from other facilities is a wise choice.

.. figure:: /_static/portal_tut02_step03e.png
    :width: 1200
    :name: portal_tut02_step03e
    :alt: Image demonstrating how selecting a row can provide information for making decisions.

**Identifying the best epoch for this scientific use-case.**


.. _DP0-2-Portal-Intermediate_Step-4:

4. Exercises for the learner
============================

**4.1.** **Obtain the visitId.** 
At this point, the user is ready to obtain the "bright / best seeing" epoch's images.
The simplest way to do that is with the visitId, but the ADQL query did not request that from the CcdVisit table.
Return to the ADQL query and add ccdvis.ccdVisitId and ccdvis.visitId to the query.

**4.2.** **Add magnitude error bars.** 
To retrieve magnitude errors from the DiaSource catalog, return to step 2.2 and add to the ADQL statement:
``scisql_nanojanskyToAbMagSigma(diasrc.psFlux, diasrc.psFluxErr) AS psAbMagErr``.
When you get to step 3.1, for the Y error choose "Symm" from the drop-down menu, and then in the new box that appears to the right, enter "psAbMagErr".
When you click "Apply" to create the plot, the points will have error bars.
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

#######################################
How to perform an image search (ObsTAP)
#######################################

.. This section should provide a brief, top-level description of the page.

.. Most recent update:  October 9 2024

=====================

Once logged into the Portal aspect of the Rubin Science Platform, searches for images at a specific location or observing time can be conducted by (currently) clicking in the "DP0.2 Images" tab on top of the screen.
Clicking on that tab will change the user interface to display query constraint options that are specific to the image data.

Additional information about the image types available in the Rubin data set is available in the :ref:`DP0-2-Data-Products-DPDD`.

**Observation Types**

The IVOA standard options provide multiple choice for "Calibration Level" (0, 1, 2, 3, or 4).
For Rubin data, "1" is for the raw (unprocessed) images, "2" is for the processed visit images (PVIs; the calibrated single-epoch images 
also called calexps), and "3" is for the derived image data such as difference images and co-added multiple PVIs ("deep coadds").

The "Data Product Type" should be left as "Image", and the "Instrument Name", "Collection", and "Data Product Subtype" can all be left blank.

Under "Location", only “Observation boundary contains point” was implemented at the time this documentation was written.

.. Recall that the central (RA, Dec) coordinates for the DC2 simulated sky region are ``61.863 -35.790``.

Under "Timing", users can specify a range of the time of observation (this is only relevant for PVIs/calexps) and/or exposure duration.

Under "Spectral Coverage", users can select one or more filters, or the wavelength in, e.g., nanometers as a means of specifying the image band.

**Output Column Selection and Constraints**

The default is for all columns to be selected (i.e., have blue checks in the leftmost column).
It is recommended to always return all metadata because the Portal requires some columns in order for the some of the "Results" view functionality to work.  

**Example (PVIs/calexps)**

The screenshot below shows an example query for all PVIs (calexps) that overlap a specified location (here:  61.863 -35.790)
which were obtained with a modified Julian date between 60000 and 60500.

.. figure:: /_static/portal_intro_DP02g.png
    :name: portal_ImageQueryDP02
    :alt: Screenshot of the user interface query for the portal aspect.  The user can select the type of service to use for the query and enter constraints to access the data they need.  
	The default interface for the "Image Search (ObsTAP)" queries, with example search parameters.
    
Clicking on the "Search" button retrieves observations in all filters.  

**Results View**

The default results appear in the tri-view format, with the image at upper left, an Active Chart plot at upper right, and the table of metadata below.
The first row of the table is highlighted by default, with the corresponding image showing at upper left.
Clicking on another row in the displayed table will result in displaying the image corresponding to that particular exposure.
The Active Chart plot default is RA versus Declination, with the location of the highlighted table row shown in orange and the rest in blue.  
It is possible to restrict the retrieved images to be only those in the 'r' filter by clicking the down-arrow below the table column heading "lsst_band" and selecting "r" from the drop-down menu.  
    
.. figure:: /_static/portal_intro_DP02h.png
    :name: portal_ImageQueryResultsDP02
    :alt: A screenshot of the results view from submitting the query described above.  The upper left image is an image of the sky.  The upper right image shows the cartesian scatter plot resulting from the query.  The bottom section is the data table resulting from the query.  
	Results for the example search parameters.  

**Manipulating the Active Chart plot** 

This can be done via clicking on the "settings" icon (single gear) in the upper right corner to change the column data being plotted, alter the plot style, add axes labels, etc.

