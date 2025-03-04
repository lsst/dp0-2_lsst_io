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


#################################
10. How to execute an Image query
#################################

.. This section should provide a brief, top-level description of the page.

For the Portal Aspect of the Rubin Science Platform at data.lsst.cloud.

**Data Release:** DP0.2

**Last verified to run:** 2025-03-04

**Learning objective:** How to query images in the RSP's Portal via ObsTAP

**LSST data products:** lsst.calexp

**Credit:** Yumi Choi. Please consider acknowledging them if this tutorial is used for the preparation of journal articles, software releases, or other tutorials.

**Get Support:** Everyone is encouraged to ask questions or raise issues in the `Support Category <https://community.lsst.org/c/support/6>`_ of the Rubin Community Forum. Rubin staff will respond to all questions posted there.


.. _DP0-2-Portal-howto-query-image-Intro:

Introduction
============

This tutorial demonstrates how to perform a basic Portal query for image data with a few example constraints using `ObsTAP <https://www.ivoa.net/documents/ObsCore/>`_.


.. _DP0-2-Portal-howto-query-image-1:

1. Navigate to the Portal’s "DP0.2 Images" tab
==============================================

**1.1. Log in to the Portal Aspect of the Rubin Science Platform.**
In a browser, go to the URL `data.lsst.cloud <https://data.lsst.cloud>`_ and select the Portal Aspect.
Follow the process to log in.

**1.2. Select the "DP0.2 Images" tab in the Portal.** 
Click on the "DP0.2 Images" tab at the top to navigate to the DP0.2 image saerch page, as shown in Figure 1.

.. figure:: /_static/portal-howto-query-image-1.png
    :name: portal-howto-query-image-1
    :alt: A screenshot of the DP0.2 image search landing page, annotated with labels.

    Figure 1: A screenshot of the DP0.2 image search landing page, annotated with labels. 



.. _DP0-2-Portal-howto-query-image-2:

2. Enter constraints for image query (A in Figure 1)
====================================================

**2.1. Set observation type and source (B in Figure 1).** 
Under "Observation Type and Source", the IVOA standard "Calibration Level" option (0, 1, 2, 3, or 4) is provided.
Check the "2" box to retrieve processed visit images (PVIs), also known as calibrated single-epoch images (calexps).
The "Data Product Type" should be left as Image”, and the “Instrument Name”, “Collection”, and “Data Product Subtype” can all be left blank.
In the "Data Product Subtype" drop-down menu, select "lsst.calexp". 

**2.2. Set location (C in Figure 1).**
Under "Location", choose "Observation boundary contains point" for "Query Type". 
Enter the central (RA, Dec) coordinates for the DC2 simulated sky region: 61.863, -35.790.

**2.3. Set timing (D in Figure 1).**
Under "Timing", specify the observation time range (relevant only for PVIs/calexps) and/or exposure duration.
Check the "Timing" box, select "Overlapping specified range" for "Time of Observation",
choose "MJD values" as the time format, and enter 60000 as the Star Time and 60500 as the End Time.  

.. figure:: /_static/portal-howto-query-image-2.png
    :name: portal-howto-query-image-2
    :width: 500
    :alt: A screenshot showing how to constrain timing in an image query.

    Figure 2: A screenshot demonstrating how to constrain timing in an image query by specifying the start and end times for the overlapping observation period in MJD. 

**2.4. Set spectral coverage (E in Figure 1).**
To constrain an image query by the LSSTCam's filter or wavelength, check the "Spectral Coverage" box and
check the "u" box to only retrieve u-band images. 

.. figure:: /_static/portal-howto-query-image-3.png
    :name: portal-howto-query-image-3
    :width: 500
    :alt: A screenshot showing how to constrain spectral coverage in an image query.

    Figure 3: A screenshot demonstrating how to constrain spectral coverage in an image query by specifying the LSSTCam's filter.

**2.5 Output Column Selection and Constraints (F in Figure 1).
The default is 27 out of 37 columns to be selected. It is recommended to return all selected metadata.
Click on the “Search” button. 



.. _DP0-2-Portal-howto-query-image-3:

3. Results
==========

The query returns seven u-band PVIs that meet all the constraints specified in Section 2.

.. figure:: /_static/portal-howto-query-image-4.png
    :name: portal-howto-query-image-4
    :alt: A screenshot showing the query results.

    Figure 4: A screenshot displaying the image query results, showing seven u-band PVIs.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
