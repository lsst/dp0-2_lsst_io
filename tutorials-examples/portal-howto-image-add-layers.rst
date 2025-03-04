.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-howto-query-image:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.


#########################################
11. How to add layers to retrieved Images
#########################################

.. This section should provide a brief, top-level description of the page.

For the Portal Aspect of the Rubin Science Platform at data.lsst.cloud.

**Data Release:** DP0.2

**Last verified to run:** 2025-03-04

**Learning objective:** How to add layers to retrieved images in the RSP's Portal query results page

**LSST data products:** lsst.calexp

**Credit:** Yumi Choi

**Get Support:** Everyone is encouraged to ask questions or raise issues in the `Support Category <https://community.lsst.org/c/support/6>`_ of the Rubin Community Forum. Rubin staff will respond to all questions posted there.


.. _DP0-2-Portal-howto-image-add-layers:

Introduction
============

This tutorial demonstrates how to add layers to the active images retreived from a basic Portal query for image data.

.. _DP0-2-Portal-howto-image-add-layers-1:

1. Execute an Image query 
=========================

Go to `data.lsst.cloud <https://data.lsst.cloud>`_ , select the Portal Aspect, and
click on the "DP0.2 Images" tab at the top. Enter your desired constraints for the image query,
and click "Search" to execute it.



.. _DP0-2-Portal-howto-image-add-layers-2:

2. Add layers to the active image(s)
====================================

Overlay additional information on the active image(s) as layers,
displayed in the top-left panel of the default results view.
  
**2.1 Explore available image layer options.**
First, click the "Tools" icon to open the drop-down menu. 
Under the "Layers" section, explore the available options. 

.. figure:: /_static/portal-howto-image-add-layers-1.png
    :name: portal-howto-image-add-layers-1
    :alt: A screenshot of the drop-down menu under the "Tool" icon.

    Figure 1: A screenshot of the drop-down menu under the "Tool" icon.

**2.2 Add desired layers to the active image.**

* To add **compass**, click the "North-East arrow" icon. 
* To add **coordinate grid**, click the "Grid" icon. 
* To add **ruler** to measure distance, select the "Ruler" icon, click a starting point, and drag to an endpoint.
* To add **regions of interest**, click the "DS9" icon, choose a DS9 region file to upload, and click "Draw".
* To add **mask**, click the "Mask" icon, upload a mask file or use an extension of the active plot file, then click "Ok".
* To add **marker**, click the last icon and select "Add Marker".
* To add **footprint**, click the last icon and select desired observatory and intrument.



.. _DP0-2-Portal-howto-image-add-layers-3:

3. Customize the image layers
=============================

After overlaying the desired layers, customize them as needed using the "Manipulate overlay display" functionality.
Click the "Layer" icon (circled in red in Figure 2) to view all added layers for the active image and access overlay display controls.

* To temporalily remove a layer, toggle the sliding button next to it.
* To completely remove a layer, click the "X" next to its "Color" box. 
* To change a layer's color, click its "Color" box and select a new color.
* To change the unit for the "Distance Tool", select the desired unit. 
* To display separations along the x and y axes, check the "Offset Calculation" box.
* To edit a marker or footprint label, enter the desired label and select its position from the drop-down menu.
* To move a marker, click and drag it. 
* To resize a marker, click and drag any corner.
* To move a footpint, click and drag any part of it.
* To roate a footprint, drag the rotate handle or enter a specific rotation angle.

.. figure:: /_static/portal-howto-image-add-layers-2.png
    :name: portal-howto-image-add-layers-2
    :alt: A screenshot of exmaple added layers listed under the "Layer" icon with overlay display controls.

    Figure 2: A screenshot of exmaple added layers listed under the "Layer" icon (circled in red) with overlay display controls.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
