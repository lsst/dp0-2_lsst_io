.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-2-schema-position:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

.. This file will not be included in a toctree because it is a reference page.
.. The ``orphan`` metadata field is used to suppress the "WARNING: document isn't included in any toctree."

:orphan:

#####################################
Schema for dp01_dc2_catalogs.position
#####################################

.. This section should provide a brief, top-level description of the page.

This page is a reference to schema for select astrometry-related parameters for objects detected in the coadded images.
Other schemas are listed under :ref:`DP0-2-Data-Products-DPDD-Catalogs`.

Principal columns are in **bold face type**.

.. list-table:: Schema for dp01_dc2_catalogs.position
   :header-rows: 1

   * - Column Name
     - Unit
     - Data Type
     - Description
   * - **coord_ra**
     - rad
     - double
     - RA-coordinate
   * - **coord_dec**
     - rad
     - double
     - Decl-coordinate
   * - **extinction_bv**
     - mag
     - double
     - Milky Way dust extinction, E(B-V)
   * - **objectId**
     - 
     - long
     - Unique id.
   * - **parent**
     - 
     - long
     - unique ID of parent source
   * - **deblend_nChild**
     - 
     - int
     - Number of children this object has (defaults to 0)
   * - **detect_isPrimary**
     - 
     - boolean
     - true if source has no children and is in the inner region of a coadd patch and is in the inner region of a coadd tract and is not "detected" in a pseudo-filter (see config.pseudoFilterList)
   * - detect_isPatchInner
     - 
     - boolean
     - true if source is in the inner region of a coadd patch
   * - detect_isTractInner
     - 
     - boolean
     - true if source is in the inner region of a coadd tract
   * - merge_footprint_sky
     - 
     - boolean
     - Detection footprint overlapped with a detection from filter sky
   * - merge_peak_sky
     - 
     - boolean
     - Peak detected in filter sky
   * - merge_footprint_[f]
     - 
     - boolean
     - Detection footprint overlapped with a detection from filter f
   * - merge_measurement_[f]
     - 
     - boolean
     - Flag field set if the measurements here are from the f filter
   * - merge_peak_[f]
     - 
     - boolean
     - Peak detected in filter f
