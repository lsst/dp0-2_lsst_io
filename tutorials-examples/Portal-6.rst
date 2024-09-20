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

**Last verified to run:** 2024-09-20

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

This first step is ...

**1.1.** Log into the Portal Aspect, click on “DP02 Images” tab at the top.  

**1.2.** Under “Observation Type and Source”, choose “Calibration Level” 3,
which is for derived images such as deepCoadds and difference images. Leave
the other options to their default settings except for the “Data Product Subtype”
enter “lsst.deepCoadd_calexp”. 

.. figure:: /_static/portal_tut05_step01a.png
    :name: portal_tut05_step01a
    :alt: A screenshot of the ADQL Query view of the Portal user interface.

    Figure 1: RSP Portal aspect with "DP0.2 catalogs" selected.

**1.3.** Under “Location”, choose “Observation boundary contains point” from
the drop-down menu and enter the coordinates “67.4579, -44.0802” - the known
location of the SNIa from Portal tutorial 02.

**1.4.** Do not set any timing or spectral coverage constraints, and do not change the default table column selections.

**1.5.** Click "Search".  
