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
.. _Tutorials-Examples-DP0-2-Portal-howto-sia:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

########################################
13. How to use Simple Image Access (SIA)
########################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski

**Last verified to run:** 2025-05-05

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to use the Simple Image Access (SIA) service to retrieve DP0.2 images and perform simple manipulation steps.
Specifically it retrieves all "calexps" (Processed Visit Images) for a containing specific location on the sky during the desired range of observation epochs.

**1. Execute an image query.**
Go to `data.lsst.cloud <https://data.lsst.cloud>`_ , select the Portal Aspect, and click on the ``SIAv2 Searches".
To the right of "Select SIAv2 Service" select the "LSST SIAV2 DP0.2 DC2" from the menu (it should be the default).

**1.1. Select the location contained in the images to be retrieved.**
Check the "Spatial" box and in the "Coordinates or Object Name" enter the desired coordinates.
This example uses 62.0, -37.0 for RA and Dec.
For "Shape Type select "Cone Shape."
For "Radius" select 10 arcseconds"

**1.2.  Select the Observation Type and Source."**
For "Calibration Level" select "Calibrated science-ready data (2)".
For the "Data Product Type" select "image".
For "Instrument Name" select 'LSSTCam-imSim."
Leave the defaults for the "Facility" and "Collection."

**1.3.  Select the desired range of observation times.**
Check the "Timing" box and for the "Time of Observation" select "Overlapping specified range".
Select "MJD values" and enter ``60100`` for the "Start Time" and ``60180`` for the end time.

.. figure:: /_static/portal-howto-SIA-1.png
	:name: portal-howto-SIA-1
	:alt: Screenshot of the window containing all parameters and ready to execute the search.

Figure 1:  The screenshot of the window containing all parameters and ready to execute the search.

**1.4.  Retrieve the images.**  
Click on the "Search" button.
This will result in extracting 17 images meeting the selected criteria.
By default, the displayed image on the upper left is the first one in the table of images on the bottom of the screen.
The plot on the uper right 


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
