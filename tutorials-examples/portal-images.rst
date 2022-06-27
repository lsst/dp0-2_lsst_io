.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-Images:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

##########################################
03. View a SNIa Host Galaxy (intermediate)
##########################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham

**Last verified to run:** 2022-06-26

**Targeted learning level:** intermediate

**Introduction:** 
This notebook demonstrates how to find the host galaxy of a SNIa in the six (ugrizy) deepCoadd images.

This tutorial assumes a basic working knowledge of the Portal interface (e.g., review of the :ref:`Portal-Intro-Image-Queries` instructions or the successful completion of the first Portal tutorial).
For more information about the DP0.2 catalogs and images, visit the :ref:`DP0-2-Data-Products-DPDD`.



.. _DP0-2-Portal-Images_Step-1:

1. Query for Images
===================

1.1. Log into the Portal Aspect and select query type "Image Search (Obs TAP)".

1.2. Under "Observation Type and Source", choose "Calibration Level" 3, which is for derived images such as deepCoadds and different images. Leave the other options to their default settings except for the "Data Product Subtype" enter "lsst.deepCoadd_calexp".

1.3. Under "Location", choose "Observation boundary contains point" from the drop-down menu and enter the coordinates "67.4579, -44.0802" - the known location of the SNIa from Portal tutorial 02.

1.4. Do not set any timing or spectral coverage constraints, and do not change the default table column selections.

.. figure:: /_static/portal_tut03_step01.png
    :name: portal_tut03_step01

    Query for the deepCoadds that cover the SNIa location.

1.5. Click "Search".


.. _DP0-2-Portal-Images_Step-2:

2. Interact with the deepCoadds
===============================

2.1. In the results view, click on "img-tbl" in the upper right corner to remove the "xy plot" from the display as it is not needed.

2.2. Above the image, click on the grid icon (hover-over text "Show full grid") to simultaneously view all six filters' deepCoadds. The default view is to center all deepCoadds on the center of the patch.

.. figure:: /_static/portal_tut03_step02a.png
    :name: portal_tut03_step02a

    The default view centers the image display on the patch center.
    
2.3. Align and lock by WCS.
Click on the "align" icon above the image (hover-over text "Image alignment drop down...") and under "Align and Lock Options" select "WCS".
Notice now that zooming and panning in one image does the same in all six images.

.. figure:: /_static/portal_tut03_step02b.png
    :name: portal_tut03_step02b

    Choose to align and lock on WCS.
 
 2.4. Mark and center the SNIa.
 Choose the "center" icon (hover-over text "Image center drop down"), and in the box next to "Center On" enter the SNIa's coordinates, "67.4579, -44.0802", and then click "Go & Mark". 
 
.. figure:: /_static/portal_tut03_step02c.png
    :name: portal_tut03_step02c

    Center on and mark the coordinates of the SNIa.
 
 2.5. 
 
