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


###################################
12. How to use image analysis tools
###################################

.. This section should provide a brief, top-level description of the page.

For the Portal Aspect of the Rubin Science Platform at data.lsst.cloud.

**Data Release:** DP0.2

**Last verified to run:** 2025-03-04

**Learning objective:** How to use image analysis tools in the RSP's Portal image query results page

**LSST data products:** Image (any data product subtype)

**Credit:** This tutorial is based on the tutorial developed by Yumi Choi and incorporates part of Step 3 from the Science Portal Tutorial, "06. Exploring SAOImageDS9-like Functionality in the Firefly-based RSP Portal."

**Get Support:** Everyone is encouraged to ask questions or raise issues in the `Support Category <https://community.lsst.org/c/support/6>`_ of the Rubin Community Forum. Rubin staff will respond to all questions posted there.


.. _DP0-2-Portal-howto-image-analysis:

Introduction
============

This tutorial demonstrates how to use basic image analysis tools on active images retreived from a Portal image query.

.. _DP0-2-Portal-howto-image-analysis-1:

1. Execute an Image query 
=========================

Go to `data.lsst.cloud <https://data.lsst.cloud>`_ , select the Portal Aspect, and
click on the "DP0.2 Images" tab at the top. Enter your desired constraints for the image query,
and click "Search" to execute it.



.. _DP0-2-Portal-howto-image-analysis-2:
                                        
2. Extract pixel values along a line 
====================================
                                        
To extract pixel values along a line (i.e., 1D Brightness Profile of a Source),
click the "Tools" icon, then select the "Line" icon under the "Extract" section.
An instruction window will appear, allowing you to choose an aperture to combine the values.
Click on the start point of the image and drag to the end point to draw a line along your source.
Once the line is drawn, a pop-up window will display the 1D brightness profile.
You can also adjust the aperture in this window as needed. To save the result temporarily,
click the "Pin Chart/Table" button at the bottom left. This will add the table and chart
next to the default results table and the active chart. Alternatively, you can download
them directly. Repeat the process to add another line.

.. figure:: /_static/portal_tut06_step03a.png
    :width: 500
    :name: portal_howto_image_analysis-1
    :alt: A screenshot displaying a line drawn across a source, accompanied by a pop-up window showing the source's 1D brightness profile along that line. 

    Figure 1: A line drawn across a source, with a pop-up window displaying the 1D brightness profile of the source.



.. _DP0-2-Portal-howto-image-analysis-3:
                                        
3. Extract pixel information for selected points 
================================================
  
To extract pixel values in the specified aperture for selected points, click the "Points" icon under the "Extract" section. 
An instruction window will appear, allowing you to choose an aperture to combine the values. Unlike the line extraction process,
multiple points can be selected to extract their pixel values at once. To save the result temporarily,
click the "Pin Chart/Table" button. Or, to save the results locally, click the "Download as Table" and/or
"Download Chart" button. Note that the results can be saved as a DS9 region file. 

.. figure:: /_static/portal_tut06_step03b.png
    :name: portal_howto_image_analysis-2
    :alt: A screenshot displaying six selected points on the image (left panel), in the active chart (right panel), and in the pinned table (bottom panel), with a pop-up window offering options for file format and naming for saving.

    Figure 2: Six selected points on the image (left panel), in the active chart (right panel), and in the pinned table (bottom panel), with a pop-up window offering options for file format and naming for saving.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
