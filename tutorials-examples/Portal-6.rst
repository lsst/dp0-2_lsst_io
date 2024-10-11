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

####################################################################
06. Exploring DS9-like Functionality in the Firefly-based RSP Portal
####################################################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Yumi Choi

**Last verified to run:** 2024-10-10

**Targeted learning level:** Beginner 

**Introduction:**
This tutorial will explore some of the key functionalities available in the Firefly-based
Rubin Science Platform (RSP) Portal that are also familiar to users of DS9, a widely-used
astronomical image viewer. Both DS9 and Firefly allow astronomers to display, analyze, and
interact with FITS image data, offering features like multiple frame support, region of
interest (ROI) tools, color mapping, and overlay capabilities. While Firefly and DS9 share
many powerful tools, they each bring unique strengths to image analysis. 

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

**2.1** Overlay a compass, coordinate grid, and ruler on the images. First, click
the "Tools" icon to open the drop-down menu. Under the "Layers" section, click the
"North-East arrow" icon to add the compass, click "Grid" icon to add a coordinate grid,
and click "Ruler" icon to measure the distance between two user-identified points.
To measure distance, click on the starting point, then drag to the endpoint.
This will display an arrow on the image along with the angular separation between
the two points and the position angle. 

.. figure:: /_static/portal_tut06_step02a.png
    :name: portal_tut06_step02a
    :alt: The image overlaid with a compass indicating the North and East directions,
    a grid for Equatorial J2000 coordinates, and a ruler measuring angular separation
    between two selected objects.

    Figure 3: The image overlaid with a compass, coordinate grid, and ruler.

**Warning:** Switching between single and tile frames does not retain the applied layers,
except for the compass indicating the North and East directions on the image.

**2.2** To select a coordinate system to overlay on the image, open the drop-down
menu under the "Grid" option from the "Manipualte overlay display" icon (magenta circle).
For the Equatorial coordinate systems, two formats are available for displaying
astronomical coordinates: sexagesimal and decimal. The readout coordinate format
is independent of the coordinate format for the overlaid grid. To choose a readout format,
click the colored box (blue square) next to the "expand window" icon at the bottom left
corner of the image panel. Having different coordinate systems for the overlaid grid
and readout is useful for determining an object's position across the two reference frames.

.. figure:: /_static/portal_tut06_step02b.png
    :name: portal_tut06_step02b
    :alt:A screenshot displaying the drop-down menu for selecting a grid coordinate system to overlay, along with the option to choose the readout coordinate to print out.

    Figure 4: Demonstration of selecting a coordinate system for the overlaid grid and configuring the readout format. 

**2.3** A different unit other than the default degrees is available for measuring
the distance between two selected points. Options include arcminutes, arcseconds, and pixels.
To change the unit, go to the "Distance Tool" option under the "Manipulate Overlay Display" icon,
and choose the unit to use. Check the "Offset Calculation" box to display the separations
along the x and y axes on the image.

.. figure:: /_static/portal_tut06_step02c.png
    :width: 400
    :name: portal_tut06_step02c
    :alt: A screenshot demonstrating how to use the distance tool to display the angular separation between two points.

    Figure 5: Demonstration of the distance tool in use, displaying the angular separation between two selected points.

**2.4** Create a region file
How to creat a region file from selecting objects in the image. 

.. figure:: /_static/portal_tut06_step02d.png
    :width: 500
    :name: portal_tut06_step02d
    :alt: xxx

    Figure 6: xxx

**2.5** Load a region file
How to load an existing region file and overplot on the image.

.. figure:: /_static/portal_tut06_step02e.png
    :width: 500
    :name: portal_tut06_step02e
    :alt: xxx

    Figure 7: xxx

**2.6** Adding a marker
How to add makers on the image.

.. figure:: /_static/portal_tut06_step02f.png
    :width: 500
    :name: portal_tut06_step02f
    :alt: xxx

    Figure 8: xxx

**2.7** Overlay footprints from various observatories and missions directly on images.
How to overlay footprints.

.. figure:: /_static/portal_tut06_step02g.png
    :name: portal_tut06_step02g
    :alt: xxx

    Figure 9: xxx

Step 3. Analysis Tools  
======================


