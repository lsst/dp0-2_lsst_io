.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-1-schema-deepCoadd-deblendedFlux:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

.. This file will not be included in a toctree because it is a reference page.
.. The ``orphan`` metadata field is used to suppress the "WARNING: document isn't included in any toctree."

:orphan:

#################################################
Schema for Butler catalog deepCoadd_deblendedFlux
#################################################

.. This section should provide a brief, top-level description of the page.

This page is a reference to schema for deblended parent and child parameters for sources in deep coadded images, based on :doc:`schema-deepCoadd-ref`.
Other schemas are listed under :ref:`DP0-1-Data-Products-DPDD-Catalogs`.

**id** (units=None,type=int64): unique ID

**coord_ra** (units=rad,type=float64): position in ra/dec

**coord_dec** (units=rad,type=float64): position in ra/dec

**parent** (units=None,type=int64): unique ID of parent source

**merge_footprint_i** (units=None,type=bool): Detection footprint overlapped with a detection from filter i

**merge_footprint_r** (units=None,type=bool): Detection footprint overlapped with a detection from filter r

**merge_footprint_z** (units=None,type=bool): Detection footprint overlapped with a detection from filter z

**merge_footprint_y** (units=None,type=bool): Detection footprint overlapped with a detection from filter y

**merge_footprint_g** (units=None,type=bool): Detection footprint overlapped with a detection from filter g

**merge_footprint_u** (units=None,type=bool): Detection footprint overlapped with a detection from filter u

**merge_footprint_sky** (units=None,type=bool): Detection footprint overlapped with a detection from filter sky

**merge_peak_i** (units=None,type=bool): Peak detected in filter i

**merge_peak_r** (units=None,type=bool): Peak detected in filter r

**merge_peak_z** (units=None,type=bool): Peak detected in filter z

**merge_peak_y** (units=None,type=bool): Peak detected in filter y

**merge_peak_g** (units=None,type=bool): Peak detected in filter g

**merge_peak_u** (units=None,type=bool): Peak detected in filter u

**merge_peak_sky** (units=None,type=bool): Peak detected in filter sky

**deblend_nChild** (units=None,type=int32): Number of children this object has (defaults to 0)

**deblend_deblendedAsPsf** (units=None,type=bool): Deblender thought this source looked like a PSF

**deblend_psfCenter_x** (units=pix,type=float64): If deblended-as-psf, the PSF centroid

**deblend_psfCenter_y** (units=pix,type=float64): If deblended-as-psf, the PSF centroid

**deblend_psf_instFlux** (units=ct,type=float64): If deblended-as-psf, the instrumental PSF flux

**deblend_tooManyPeaks** (units=None,type=bool): Source had too many peaks; only the brightest were included

**deblend_parentTooBig** (units=None,type=bool): Parent footprint covered too many pixels

**deblend_masked** (units=None,type=bool): Parent footprint was predominantly masked

**deblend_skipped** (units=None,type=bool): Deblender skipped this source

**deblend_rampedTemplate** (units=None,type=bool): This source was near an image edge and the deblender used "ramp" edge-handling.

**deblend_patchedTemplate** (units=None,type=bool): This source was near an image edge and the deblender used "patched" edge-handling.

**deblend_hasStrayFlux** (units=None,type=bool): This source was assigned some stray flux
