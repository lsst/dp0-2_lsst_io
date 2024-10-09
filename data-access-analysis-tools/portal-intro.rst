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

#####################################
Introduction to the RSP Portal Aspect
#####################################

.. This section should provide a brief, top-level description of the page.

.. Most recent update:  October 9 2024

Image Search (ObsTAP)
=====================

You can perform image searches by clicking in the "DP0.2 Images" tab on top of the screen.  
This functionality has many new features -- not just new for DP0.2, but new to the Firefly interface, and DP0 Delegates are among the first to use them.
Clicking on that tab will change the user interface to display query constraint options that are specific to the image data, as described below.

For more information about the image types available in the DP0.2 data set, see the :ref:`DP0-2-Data-Products-DPDD`.

**Enter Constraints**

Under "Observation Type and Source", the IVOA standard options for "Calibration Level" (0, 1, 2, 3, or 4) are provided.
For DP0.2, "1" is the raw (unprocessed) images, "2" is the processed visit images (PVIs; the calibrated single-epoch images 
also called calexps), and "3" are the derived image data such as difference images and deep coadds.

The "Data Product Type" should be left as "Image", and the "Instrument Name", "Collection", and "Data Product Subtype" can all be left blank.

Under "Location", only “Observation boundary contains point” was implemented at the time this documentation was written.
Recall that the central (RA, Dec) coordinates for the DC2 simulated sky region are ``61.863 -35.790``.

Under "Timing", users can specify a range of the time of observation (this is only relevant for PVIs/calexps) 
and/or exposure duration.

Under "Spectral Coverage", users can provide a wavelength in, e.g., nanometers as a means of specifying the image band.

**Output Column Selection and Constraints**

The default is for all columns to be selected (i.e., have blue checks in the leftmost column).
It is recommended to always return all metadata because the Portal requires some columns in order for the some of the 
"Results" view functionality to work.  

**Example (PVIs/calexps)**

The screenshot below shows an example query for all PVIs (calexps) that overlap the central coordinates of DC2, 
which were obtained with a modified Julian date between 60000 and 60500.

.. figure:: /_static/portal_intro_DP02g.png
    :name: portal_ImageQueryDP02
    :alt: Screenshot of the user interface query for the portal aspect.  The user can select the type of service to use for the query and enter constraints to access the data they need.  
	The default interface for the "Image Search (ObsTAP)" queries, with example search parameters.
    
Click on the "Search" button.  Note that this search retrieves observations in all filters.  

**Results View**

The default results appear in the tri-view format, with the image at upper left, an Active Chart plot at upper right, and the table of metadata below.
The first row of the table is highlighted by default, with the corresponding image showing at upper left.
The Active Chart plot default is RA versus Declination, with the location of the highlighted table row shown in orange and the rest in blue.  
You can restrict the retrieved images to be only those in the 'r' filter by clicking the down-arrow below the table column heading "lsst_band" and selecting "r" from the drop-down menu.  
    
.. figure:: /_static/portal_intro_DP02h.png
    :name: portal_ImageQueryResultsDP02
    :alt: A screenshot of the results view from submitting the query described above.  The upper left image is an image of the sky.  The upper right image shows the cartesian scatter plot resulting from the query.  The bottom section is the data table resulting from the query.  
	Results for the example search parameters.  

**Manipulating the Active Chart plot** is the same process as shown for the :ref:`Portal-Intro-Single-Table-Queries` results: 
click on the "settings" icon (single gear) in the upper right corner to change the column data being plotted, alter the plot style, add axes labels, etc.

**Interacting with the images** begins with just hovering the mouse over the sky image and noting the RA, Dec, and pixel value appear at the bottom.
Use the magnifying glass icons in the upper left corner to zoom in and out. 
You might need to hover over the image for these magnifying glasses to appear on the upper left.  
Click and drag the image to pan.
Above the magnifying glass icons, use the back and forth arrows to navigate between HDU (header data units) 1, 2, and 3: the image, mask, and variance data.
Click on another row in the table, to display an image of a different part of the sky.
At upper left, click on the "hamburger" menu, and in the "Results Layout" tab, select "Tables / Coverage Images Charts" option.  
On the right-hand side, select "Data Product: ivoa.ObsCore" tab.  
This will result in the table and the sky image side-by-side.

.. figure:: /_static/portal_intro_DP02i.png
    :name: portal_ImageQuery_sidebyside_DP02
    :alt: Screenshot of a portal query.  The left image shows and image of the sky.  The right image shows the data table with one row selected, that row selects the image on the left.  
	Display of the image in row two of the table (with the view format set to "Tables / Coverage Images Charts").

**Image tools**:
There are many tools available for users, the following demonstrates use of just one.
First, zoom in on a bright star in one of the images.
Select the "tools" icon (wrench and hammer), and from the pop-up window choose to "Extract" using a line.
Draw a line on the image across the star to extract the pixel values and show an approximate shape of the point-spread function (PSF) for the star.
The plot reveals that this particular star is saturated.
Click on "Pin Chart/Table" to add a table of pixel data as a new tab in the left half of the view (the "Tables" side) as well as the PSF profile plot as a 
new tab next to Active Chart plot (the tab is marked as "Pinned Charts"). To make the line go away, click on the "layers" icon (the one for which the hover-over text reads:  
"Manipulate overlay display...") and in the pop-up window, next to "Extract Line 1 - HDU#1", click on "x" by the "Extract Line Tool" row.

.. figure:: /_static/portal_intro_DP02j.png
    :name: portal_ImageQuery_tools_DP02
    :alt: A screenshot of the image display used to extract a line cut in the portal. On the left, is an image of the sky with an inverted color lookup table.
    	There is one large star in the image.  A horizontal arrow has been manually drawn over it by the user.  A data table is to the right.  Sitting over the data table is a graph, constructed from the red arrow, showing data numbers versus offset in arcseconds.  
	The use the image display tool to extract a line cut.

**Image grid display**:
Close all pop-up windows.  Above the image use the grid icon (hover-over text "Tile all images in the search result table") to show up to eight of the images side-by-side.
Notice that it is possible to pan and zoom in each of these grid windows. 

**Coverage window**:
Above the image, notice that the default tab view is "Data Product: ivoa.obs.core", and instead click on "Coverage".
The bounding boxes of all images listed in the table are shown, with the image in the selected row highlighted.
The color-composite background shows the relevant DC2 simulated sky region.

.. figure:: /_static/portal_intro_DP02k.png
    :name: portal_ImageQueryCoverageDP02
    :alt: This image is a screenshot of a results interface display in the Portal aspect. At right the bounding boxes for images returned by the query are drawn onto an image of the night sky. At left there is a table which lists metadata such as visit identifier and units for the images returned by the query.  The image demonstrates how users can click on a row in the table at left and the corresponding bounding box will be highlighted at right.   
	The Portal "Results" view shows the bounding boxes of the retrieved DP0.2 images overplotted on a 2MASS image (in the future, the underlay will be LSST data) at the right, and the table
    of retrieved DP0.2 image metadata at left.  The orange box at right corresponds to the yellow row at left.

**Learn More.**
See also :ref:`DP0-2-Tutorials-Portal` for a tutorial using additional image types and more of the Portal's image-related functionality.
