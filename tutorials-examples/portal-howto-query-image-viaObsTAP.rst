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
.. _Tutorials-Examples-DP0-2-Portal-howto-query-image-viaObsTAP:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#######################################
10. How to search for images via ObsTAP
#######################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Yumi Choi

**Last verified to run:** 2025-03-04

**Targeted learning level:** beginner

**Introduction:**
This tutorial demonstrates how to perform a basic Portal query for image data with a few example constraints using `ObsTAP <https://www.ivoa.net/documents/ObsCore/>`_.

**1. Log in to the Portal Aspect of the Rubin Science Platform.**
In a browser, go to the URL `data.lsst.cloud <https://data.lsst.cloud>`_ and select the Portal Aspect.
Follow the process to log in.

**2. Select the "DP0.2 Images" tab in the Portal.** 
Click on the "DP0.2 Images" tab at the top to navigate to the DP0.2 image search page, as shown in Figure 1.

.. figure:: /_static/portal-howto-query-image-1.png
    :name: portal_howto_query_image_viaObsTAP-1
    :alt: A screenshot of the DP0.2 image search landing page, annotated with labels.

    Figure 1: A screenshot of the DP0.2 image search landing page, annotated with labels. 


**3. Enter constraints for image query (A in Figure 1).**

**3.1. Set observation type and source (B in Figure 1).** 
Select IVOA standard "Calibration Level" 2 to retrieve processed visit images (PVIs; also called "calexps") and "lsst.calexp" in the "Data Product Subtype" drop-down menu. 

**3.2. Set location (C in Figure 1).**
Choose "Observation boundary contains point" for "Query Type" and enter 61.863, -35.790.

**3.3. Set timing (D in Figure 1).**
Check "Timing", select "Overlapping specified range" for "Time of Observation",
choose "MJD values", and enter 60000 as the Star Time and 60500 as the End Time.  

.. figure:: /_static/portal-howto-query-image-2.png
    :name: portal_howto_query_image_viaObsTAP-2
    :width: 500
    :alt: A screenshot showing how to constrain timing in an image query.

    Figure 2: A screenshot demonstrating how to constrain timing in an image query by specifying the start and end times for the overlapping observation period in MJD. 


**3.4. Set spectral coverage (E in Figure 1).**
To constrain an image query by the LSSTCam's filter or wavelength, check the "Spectral Coverage" box and
check the "u" box to only retrieve u-band images. 

.. figure:: /_static/portal-howto-query-image-3.png
    :name: portal_howto_query_image_viaObsTAP-3
    :width: 500
    :alt: A screenshot showing how to constrain spectral coverage in an image query.

    Figure 3: A screenshot demonstrating how to constrain spectral coverage in an image query by specifying the LSSTCam's filter.


**3.5. Output column selection (F in Figure 1).**
The default is 27 out of 37 columns to be selected. It is recommended to return all selected metadata.
Click on the “Search” button. 

**4. Results.**
The query returns seven u-band PVIs that meet all the constraints specified in Section 2.

.. figure:: /_static/portal-howto-query-image-4.png
    :name: portal_howto_query_image_viaObsTAP-4
    :width: 700
    :alt: A screenshot showing the query results.

    Figure 4: A screenshot displaying the image query results, showing seven u-band PVIs.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
