.. This is the beginning of a new tutorial focussing on learning to Firefly features of the Rubin Portal

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

############################################################################
06. Exploring SAOImageDS9-like Functionality in the Firefly-based RSP Portal
############################################################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Yumi Choi

**Last verified to run:** 2024-10-11

**Targeted learning level:** Beginner 

**Introduction:**
This tutorial will explore some of the key functionalities available in the 
`Firefly <https://github.com/Caltech-IPAC/firefly?tab=readme-ov-file#firefly>`_-based
Rubin Science Platform (RSP) Portal that are also familiar to users of 
`SAOImageDS9 <https://sites.google.com/cfa.harvard.edu/saoimageds9>`_ (hearafter DS9), 
a widely-used astronomical image viewer. Both DS9 and Firefly allow astronomers to display,
analyze, and interact with FITS (Flexible Image Transport System) image data, offering
features like multiple frame support, region of interest (ROI) tools, color mapping,
and overlay capabilities. While Firefly and DS9 share many powerful tools, they each
bring unique strengths to image analysis. 

This tutorial will demonstrate Firefly's key functionalities in the RSP Portal, enabling
users to effectively utilize these tools for their astronomical research.  

.. _DP0-2-Portal-6-Step-1:

Step 1. Query for Images 
========================

The first step is to query images to explore with Firefly functionalities.

**1.1.** Log into the Portal Aspect, click "DP02 Images" tab at the top.  

**1.2.** Under Observation Type and Source", choose "Calibration Level" 3,
which is for derived images such as deepCoadds and difference images. Leave
the other options to their default settings except for the "Data Product Subtype"
select "lsst.deepCoadd_calexp". 

**1.3.** Under "Location", choose "Observation boundary contains point" from
the drop-down menu and enter the coordinates "56, -34.9" - this is a random
location within the `DC2 <https://dp0-2.lsst.io/data-products-dp0-2/index.html#the-desc-dc2-data-set>`_
footprint. Do not set any timing, spectral coverage, or object ID search constraints.

.. figure:: /_static/portal_tut06_step01a.png
    :width: 400
    :name: portal_tut06_step01a
    :alt: A screenshot of the Portal aspect after selecting the "DP0.2 Images" with the query set up.

    Figure 1: RSP Portal aspect with "DP0.2 Images" selected, prepared to query images.

**1.4.** Click "Search", and the Portal will execute the query and display
the default results view.

.. figure:: /_static/portal_tut06_step01b.png
    :name: portal_tut06_step01b
    :alt: A screenshot of the DP0.2 Image Query's default results view.

    Figure 2: The default results view for the DP0.2 Image Query.


.. _DP0-2-Portal-6-Step-2:

Step 2. Add Layers to the Active Image(s)  
=========================================

Additional information can be overlaid on the active image(s) as layers. 

**2.1. Overlay a compass, coordinate grid, and ruler on the images.** First, click
the "Tools" icon to open the drop-down menu. Under the "Layers" section, click the
"North-East arrow" icon to add the compass, click "Grid" icon to add a coordinate grid,
and click "Ruler" icon to measure the distance between two user-identified points.
To measure distance, click on the starting point, then drag to the endpoint.
This will display an arrow on the image along with the angular separation between
the two points and the position angle. 

.. figure:: /_static/portal_tut06_step02a.png
    :width: 600
    :name: portal_tut06_step02a
    :alt: The image overlaid with a compass indicating the North and East directions, a grid for Equatorial J2000 coordinates, and a ruler measuring angular separation between two selected objects.

    Figure 3: The image overlaid with a compass, coordinate grid, and ruler.

**Warning:** Switching between single and tile frames does not retain the applied layers,
except for the compass indicating the North and East directions on the image.

**2.2. Select the Coordinate Systems to Overlay and to Read Out.** To select a coordinate
system to overlay on the image, open the drop-down menu under the "Grid" option from the
"Manipualte overlay display" icon (magenta circle). For the Equatorial coordinate systems,
two formats are available for displaying astronomical coordinates: sexagesimal and decimal.
The readout coordinate format is independent of the coordinate format for the overlaid grid.
To choose a readout format, click the colored box (blue square) next to the "expand window"
icon at the bottom left corner of the image panel. Having different coordinate systems for
the overlaid grid and readout is useful for determining an object's position across the two
reference frames. 

.. figure:: /_static/portal_tut06_step02b.png
    :width: 700
    :name: portal_tut06_step02b
    :alt: A screenshot displaying the drop-down menu for selecting a grid coordinate system to overlay, along with the option to choose the readout coordinate to print out.

    Figure 4: Demonstration of selecting a coordinate system for the overlaid grid and configuring the readout format.

**Note:** Remove a layer completely by clicking the "x" next to the "color" box, or
temporarily disable it by toggling the sliding button for that layer. 

**2.3. Manipulate the Distance Tool.** 
A different unit other than the default degrees is available for measuring the distance
between two selected points. Options include arcminutes, arcseconds, and pixels. To change
the unit, go to the "Distance Tool" option under the "Manipulate Overlay Display" icon, and
choose the unit to use. Check the "Offset Calculation" box to display the separations along
the x and y axes on the image.

.. figure:: /_static/portal_tut06_step02c.png
    :width: 400
    :name: portal_tut06_step02c
    :alt: A screenshot demonstrating how to use the distance tool to display the angular separation between two points.

    Figure 5: Demonstration of the distance tool in use, displaying the angular separation between two selected points.

**2.4.** A DS9 region file can be uploaded to the Portal, and overlaid on the image.
Download an example region file to your computer using the `link to the file <https://github.com/lsst/dp0-2_lsst_io/blob/main/_static/table_Points-4-HDU1.reg>`_.
If new to GitHub, click this link to navigate to the GitHub repository containing the 
example region file, then click the "Download" tab (an icon of an arrow pointing into a box).
To load the region file into the Portal and overlay the entries on the image, click the "Tools"
icon to open the drop-down menu. Under the "Layers" section, select the "Load a DS9 Region File"
icon to open a file upload window. Click "Choose File", select the region file from your computer,
click "Upload", and then click "Draw". It should overlay six circles on the image.  

.. figure:: /_static/portal_tut06_step02d.png
    :width: 500
    :name: portal_tut06_step02d
    :alt: A screenshot showing how to upload an existing region file and overlay its entries on the image.

    Figure 6: Six entries from the uploaded region file are overlaid on the image.

**2.5.** Markers can be added to the images. Click the "Tools" icon to open the drop-down menu.
Under the "Layers" section, click the last icon and select "Add Marker." A marker labeled
"Marker #1" will appear at the center of the image. Click and drag the marker to the desired
location, and adjust its size by dragging any corner of the surrounding box. To edit the marker,
click the "Manipualte overlay display" icon and go to the "Marker #1" section. Change the label
by typing "galaxy of interest" into the "Label" field, and use the "Corner" drop-down to adjust
the label’s position. To change the marker's color, click the "color" box to open the "Color Picker"
window and select your preferred color. To add another marker, click the "Add Marker" box, which
will place a new marker at the center of the image.

.. figure:: /_static/portal_tut06_step02e.png
    :width: 700
    :name: portal_tut06_step02e
    :alt: A screenshot showing how to add a marker and edit the marker.

    Figure 7: The image with an added marker with the modified label and color. 

**2.6.** Lastly, it is possible to overlay footprints from various observatories and intruments
directly onto the image. Click the last icon under the "Layers" section. Select "IRAC36" from
the "Add Spitzer footprint" option, "WFC3/UVIS" from the "Add HST footprint" option, and "NIRCam"
from the "Add JWST prelim. footprint" option. All three footprints will appear on the image.
Adjust their positions, angles, labels, label locations, and colors as desired in the 
"Manipulate Overlay Display" section as described in Step 2.5.

.. figure:: /_static/portal_tut06_step02f.png
    :name: portal_tut06_step02f
    :alt: A screenshot demonstrating how to overlay footprints from various observatories and instruments onto the image.

    Figure 8: The footprints of the Spitzer/IRAC36, HST's WFC3/UVIS, and JWST/NIRCam are overlaid on the image. 

**2.7.** At any point, if you want to capture all the layers as an image, click the "Tools"
icon, then select the "Save" icon and choose "PNG" as the file type. Note that the "FITS"
format only saves the default image. To remove all edits and revert to the default settings,
click the "Restore" icon. Click the "Information" icon to view the FITS header. 

Step 3. Analysis Tools  
======================

The Portal feature enables a variety of basic image analysis tools.

**3.1.** Extract line 

.. figure:: /_static/portal_tut06_step03a.png
    :name: portal_tut06_step03a
    :alt: xxx

    Figure 9: xxx

**3.2.** Extract points

.. figure:: /_static/portal_tut06_step03b.png
    :name: portal_tut06_step03b
    :alt: xxx

    Figure 10: xxx 

**3.3.** Save extracted points as a DS9 region file

**3.4.** TAP search for the extracted points

`Link to the Portal FAQ page <https://dp0-2.lsst.io/v/PREOPS-5150/data-access-analysis-tools/portal-future-faq.html>`_


