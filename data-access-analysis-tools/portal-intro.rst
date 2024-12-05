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

.. Most recent update:  December 4 2024

=====================

**1.  Selecting the image (rather than catalog) repository**:  Once logged into the Portal aspect of the Rubin Science Platform, searches for images at a specific location or observing time can be conducted by (currently) clicking in the "DP0.2 Images" tab on top of the screen.
Clicking on that tab will change the user interface to display query constraint options that are specific to the image data.

Additional information about the image types available in the Rubin data set is available in the :ref:`DP0-2-Data-Products-DPDD`.

**2.  Observation Types (calibration level)**: The IVOA standard options provide multiple choice for "Calibration Level" (0, 1, 2, 3, or 4).
For Rubin data, "1" is for the raw (unprocessed) images, "2" is for the processed visit images (PVIs; the calibrated single-epoch images 
also called calexps), and "3" is for the derived image data such as difference images and co-added multiple PVIs ("deep coadds").

**3.  Selection criteria**:  The "Data Product Type" should be left as "Image", and the "Instrument Name", "Collection", and "Data Product Subtype" should all be left blank.

Under "Location", only “Observation boundary contains point” was implemented at the time this documentation was written.

.. Recall that the central (RA, Dec) coordinates for the DC2 simulated sky region are ``61.863 -35.790``.

Under "Timing", users can specify a range of the time of observation (this is only relevant for PVIs/calexps) and/or exposure duration.

Under "Spectral Coverage", users can select one or more filters, or the wavelength in, e.g., nanometers as a means of specifying the image band.

**4.  Output Column Selection and Constraints**:  
The default is for all columns to be selected (i.e., have blue checks in the leftmost column).
It is recommended to always return all metadata because the Portal requires some columns in order for the some of the "Results" view functionality to work.  

**5.  Example (PVIs/calexps)**:
The screenshot below shows an example query for all PVIs (calexps) that overlap a specified location (here:  61.863 -35.790)
which were obtained with a modified Julian date between 60000 and 60500.

.. figure:: /_static/Howto_Image_1.png
    :name: Howto_Image_1
    :alt: Screenshot of the user interface query for the portal aspect.  The user can select the type of service to use for the query and enter constraints to access the data they need.  
	
**The default interface for the "Image Search (ObsTAP)" queries, with example search parameters.**
    
Clicking on the "Search" button retrieves observations in all filters.  

**6.  Results View**:
The default results appear in the tri-view format, with the image at upper left, an Active Chart plot at upper right, and the table of metadata below.
The Active Chart plot default is RA versus Declination of all retrieved images, with the location of the highlighted table row shown in orange and the rest in blue, with the corresponding image showing at upper left.
Clicking on another row in the displayed table will result in displaying the image corresponding to that particular exposure.
It is possible to restrict the retrieved images to be only those in the 'r' filter by clicking the down-arrow below the table column heading "lsst_band" and selecting "r" from the drop-down menu.  
    
.. figure:: /_static/Howto_Image_2.png
    :name: Howto_Image_2
    :alt: A screenshot of the results view from submitting the query described above.  The upper left image is an image of the sky.  The upper right image shows the cartesian scatter plot resulting from the query.  The bottom section is the data table resulting from the query.  

**Results for the example search parameters, with the left panel displaying the image corresponding to the observation which is highlighted in orange in the table at the bottom.**

**7.  Manipulating the Active Chart plot**:
This can be done via clicking on the "settings" icon (single gear) in the upper right corner to change the column data being plotted, alter the plot style, add axes labels, etc.

