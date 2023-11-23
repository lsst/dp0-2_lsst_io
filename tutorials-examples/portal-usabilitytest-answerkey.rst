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
.. _Tutorials-Examples-DP0-2-Portal-UsabilityTest-AnswerKey:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

################################
Portal Usability Test Answer Key
################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** 

**Last verified to run:** 

**Link to Portal usability test:** 

**Introduction:**
Anyone is welcome to do the Portal usability test and submit their responses via
the Google form linked above.

The following is the answer key for the tasks in the test.


.. _DP0-2-Portal-UTAK-task1:

Beginner Task 1
===============

1.1. Log in to the Portal Aspect of the Rubin Science Platform.  

1.2. Next to “LSST DP0.2 DC2 Tables”, choose the Table Collection to be “dp02_dc2_catalogs” (left drop-down menu) and the Table to be “dp02_dc2_catalogs.Object” (right drop-down menu).

1.3. Under “Enter Constraints”, select the box to the left of “Spatial”. Leave the “Shape Type” as the default “Cone”, and for “Coords or Obj Name” use the central coordinates of the DC2 simulation area “62, -35”. Next to “Radius”, from the drop down menu choose “arcseconds” and then enter “120”.

1.4. In the table at right, under “Output Column Selection and Constraints”, click the box in the left-most column to select “coord_ra”, “coord_dec”, “detect_isPrimary”, “g” “r” and “i_calibFlux”. 

1.5. In the “constraints” column, enter “=1” for the “detect_isPrimary”.

1.6. Set the “Row Limit” to 10000, to only retrieve 10000 objects for this demonstration.

1.7. Click “Search” at lower left.

1.8 Click on the Active Chart settings icon (two gears, upper right) in order to “modify trace”, which means to change the plot parameters. Set “X” to be “g_calibFlux - r_calibFlux”, and “Y” to be “i_calibFlux”. Click on “Chart Options” and set “X Label” to “calibFlux (g-r)” and “Y Label” to “calibFlux (i)”. 

1.9 Set the “X Min/Max” values to “-200” and “20”, and the “Y Min/Max” values to “0” and “1000”.

2.0 Click on the “save” icon to download the chart as a png.

Beginner Task 2
===============

1.1. Log in to the Portal Aspect.

1.2. Next to “LSST DP0.2 DC2 Tables”, choose the Table Collection to be “dp02_dc2_catalogs” (left drop-down menu) and the Table to be “dp02_dc2_catalogs.Object” (right drop-down menu).

1.3. Under “Enter Constraints”, select the box to the left of “Spatial”. Leave the “Shape Type” as the default “Cone”, and for “Coords or Obj Name” use the central coordinates of the DC2 simulation area “55, -32.27”. Next to “Radius”, from the drop down menu choose “arcminutes” and then enter “15”.

1.4. In the table at right, under “Output Column Selection and Constraints”, click the box in the left-most column to select “coord_ra”, “coord_dec”, “detect_isPrimary”, “g_psfFlux” “g_calibFlux” and “g_extendedness”. 

1.6. In the “constraints” column, enter “=1” for the “detect_isPrimary”.

1.7. Set the “Row Limit” to 10000, to only retrieve 10000 objects for this demonstration.

1.8. Click “Search” at lower left.

1.9 Click on the Active Chart settings icon (two gears, upper right) in order to “modify trace”, which means to change the plot parameters. Set “X” to be “g_calibFlux”, and “Y” to be “g_psfFlux”. Click on “Chart Options” and set “X Label” to “g_calibFlux” and “Y Label” to “g_psfFlux”. 

2.0 In the results table on the left, set g_extendedness = 1. 

2.1 Click on the Active Chart settings icon (two gears, upper right) and click on “Trace Options”. Click on search next to color, and select purple.

Intermediate Task 1
===================

1.1. Log into the Portal Aspect and check the “Use Image Search (ObsTAP)” box below “LSST DP0.2 DC2 Tables”.

1.2. Under “Observation Type and Source”, choose “Calibration Level” 2

1.3. Under “Location”, choose “Observation boundary contains point” from the drop-down menu and enter the coordinates “55.75, -32.27”.

1.4. Under timing constraints, choose “Overlapping specified range” and use “MJD values”. Enter the end time “59840”

1.5. Under spectral coverage choose “by filter bands” and select “i”. 

1.6  Click on “Bi-view Tables” in the upper right corner to show just one image and the table side-by-side. To display the six filters’ deepCoadds, select “Data Product” tab.

1.7. Above the image, click on the grid icon (hover-over text “Tile all images in the search result table”) to simultaneously view all 4 i band PVIs.

1.8 Click on the first image and choose the “center” icon (hover-over text “Image center drop down”), and in the box next to “Center On” enter coordinates, “55.75, -32.27”, and then click “Go”.

1.9 Click on the “align” icon above the image (hover-over text “Image alignment drop down…”) and under “Align and Lock Options” select “by WCS”.

2.0 . Click the magnifying glass with the “+” 3 times.

Intermediate Task 2
===================

1.1. On the upper right of the portal aspect, click on “Edit ADQL.”

1.2. Enter the following ADQL code into the “ADQL Query” box:

.. code-block:: SQL

	SELECT diasrc.diaObjectId, diasrc.diaSourceId,
	diasrc.filterName, diasrc.midPointTai, diasrc.psFlux, diasrc.psFluxErr
	FROM dp02_dc2_catalogs.DiaSource AS diasrc
	WHERE diasrc.diaObjectId = 1250953961339360185
	AND diasrc.filterName = 'r'

1.3 Click on the Active Chart settings icon and set “X” to be “midPointTai”, and “Y” to be “psFlux”. Under “Y”, select “Error” and enter “psFluxErr”. 

1.4 Under “Trace style” select “Connected points” and under “Trace options” enter “red” for color. 

1.5 Click on “Chart Options” and set “X Label” to “MJD of the Exposure Midpoint” and “Y Label” to “PSF Difference-Image Flux”. 

1.6 To sort the results, click on the table column “midPointTai”.  


Advanced Task 1
===============

Advanced Task 2
===============


