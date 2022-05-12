.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-2-schema-forced-photometry:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

.. This file will not be included in a toctree because it is a reference page.
.. The ``orphan`` metadata field is used to suppress the "WARNING: document isn't included in any toctree."

:orphan:

##############################################
Schema for dp01_dc2_catalogs.forced_photometry
##############################################

.. This section should provide a brief, top-level description of the page.

This page is a reference to schema for forced photometry measurements for objects detected in the coadded images, at the locations defined by the position table.
Other schemas are listed under :ref:`DP0-2-Data-Products-DPDD-Catalogs`.

Principal Columns
=================

**coord_dec** (unit=rad, type=double): position in ra/dec

**coord_ra** (unit=rad, type=double): position in ra/dec

**objectId** (type=long): Unique id.

**[f]_base_ClassificationExtendedness_flag** (type=boolean): Set to 1 for any fatal failure.

**[f]_base_ClassificationExtendedness_value** (type=double): Set to 1 for extended sources, 0 for point sources.

**[f]_good** (type=boolean): True if the source has no flagged pixels.

**[f]_modelfit_CModel_instFlux** (unit=count, type=double): flux from the final cmodel fit

**[f]_modelfit_CModel_instFluxErr** (unit=count, type=double): flux uncertainty from the final cmodel fit


All Other Columns
=================

**[f]_base_InputCount_flag** (type=boolean): Set for any fatal failure

**[f]_base_InputCount_flag_badCentroid** (type=boolean): General Failure Flag

**[f]_base_InputCount_flag_noInputs** (type=boolean): No coadd inputs available

**[f]_base_InputCount_value** (type=int): Number of images contributing at center, not including anyclipping

**[f]_base_LocalBackground_flag** (type=boolean): General Failure Flag

**[f]_base_LocalBackground_flag_badCentroid** (type=boolean): General Failure Flag

**[f]_base_LocalBackground_flag_noGoodPixels** (type=boolean): no good pixels in the annulus

**[f]_base_LocalBackground_flag_noPsf** (type=boolean): no PSF provided

**[f]_base_LocalBackground_instFlux** (unit=count, type=double): background in annulus around source

**[f]_base_LocalBackground_instFluxErr** (unit=count, type=double): 1-sigma instFlux uncertainty

**[f]_base_PixelFlags_flag** (type=boolean): General failure flag, set if anything went wrong

**[f]_base_PixelFlags_flag_bad** (type=boolean): Bad pixel in the Source footprint

**[f]_base_PixelFlags_flag_bright_object** (type=boolean): Source footprint includes BRIGHT_OBJECT pixels

**[f]_base_PixelFlags_flag_bright_objectCenter** (type=boolean): Source center is close to BRIGHT_OBJECT pixels

**[f]_base_PixelFlags_flag_clipped** (type=boolean): Source footprint includes CLIPPED pixels

**[f]_base_PixelFlags_flag_clippedCenter** (type=boolean): Source center is close to CLIPPED pixels

**[f]_base_PixelFlags_flag_cr** (type=boolean): Cosmic ray in the Source footprint

**[f]_base_PixelFlags_flag_crCenter** (type=boolean): Cosmic ray in the Source center

**[f]_base_PixelFlags_flag_edge** (type=boolean): Source is outside usable exposure region (masked EDGE or NO_DATA)

**[f]_base_PixelFlags_flag_inexact_psf** (type=boolean): Source footprint includes INEXACT_PSF pixels

**[f]_base_PixelFlags_flag_inexact_psfCenter** (type=boolean): Source center is close to INEXACT_PSF pixels

**[f]_base_PixelFlags_flag_interpolated** (type=boolean): Interpolated pixel in the Source footprint

**[f]_base_PixelFlags_flag_interpolatedCenter** (type=boolean): Interpolated pixel in the Source center

**[f]_base_PixelFlags_flag_offimage** (type=boolean): Source center is off image

**[f]_base_PixelFlags_flag_rejected** (type=boolean): Source footprint includes REJECTED pixels

**[f]_base_PixelFlags_flag_rejectedCenter** (type=boolean): Source center is close to REJECTED pixels

**[f]_base_PixelFlags_flag_saturated** (type=boolean): Saturated pixel in the Source footprint

**[f]_base_PixelFlags_flag_saturatedCenter** (type=boolean): Saturated pixel in the Source center

**[f]_base_PixelFlags_flag_sensor_edge** (type=boolean): Source footprint includes SENSOR_EDGE pixels

**[f]_base_PixelFlags_flag_sensor_edgeCenter** (type=boolean): Source center is close to SENSOR_EDGE pixels

**[f]_base_PixelFlags_flag_suspect** (type=boolean): Source''s footprint includes suspect pixels

**[f]_base_PixelFlags_flag_suspectCenter** (type=boolean): Source''s center is close to suspect pixels

**[f]_base_PsfFlux_apCorr** (type=double): aperture correction applied to base_PsfFlux

**[f]_base_PsfFlux_apCorrErr** (type=double): standard deviation of aperture correction applied to base_PsfFlux

**[f]_base_PsfFlux_area** (unit=pixel, type=double): effective area of PSF

**[f]_base_PsfFlux_flag** (type=boolean): General Failure Flag

**[f]_base_PsfFlux_flag_apCorr** (type=boolean): set if unable to aperture correct base_PsfFlux

**[f]_base_PsfFlux_flag_badCentroid** (type=boolean): General Failure Flag

**[f]_base_PsfFlux_flag_edge** (type=boolean): object was too close to the edge of the image to use the full PSF model

**[f]_base_PsfFlux_flag_noGoodPixels** (type=boolean): not enough non-rejected pixels in data to attempt the fit

**[f]_base_PsfFlux_instFlux** (unit=count, type=double): instFlux derived from linear least-squares fit of PSF model

**[f]_base_PsfFlux_instFluxErr** (unit=count, type=double): 1-sigma instFlux uncertainty

**[f]_base_SdssCentroid_flag** (type=boolean): General Failure Flag

**[f]_base_SdssCentroid_flag_almostNoSecondDerivative** (type=boolean): Almost vanishing second derivative

**[f]_base_SdssCentroid_flag_badInitialCentroid** (type=boolean): whether the reference centroid is marked as bad

**[f]_base_SdssCentroid_flag_edge** (type=boolean): Object too close to edge

**[f]_base_SdssCentroid_flag_noSecondDerivative** (type=boolean): Vanishing second derivative

**[f]_base_SdssCentroid_flag_notAtMaximum** (type=boolean): Object is not at a maximum

**[f]_base_SdssCentroid_flag_resetToPeak** (type=boolean): set if CentroidChecker reset the centroid

**[f]_base_SdssCentroid_x** (unit=pixel, type=double): centroid from Sdss Centroid algorithm

**[f]_base_SdssCentroid_xErr** (unit=pixel, type=double): 1-sigma uncertainty on x position

**[f]_base_SdssCentroid_y** (unit=pixel, type=double): centroid from Sdss Centroid algorithm

**[f]_base_SdssCentroid_yErr** (unit=pixel, type=double): 1-sigma uncertainty on y position

**[f]_base_SdssShape_flag** (type=boolean): General Failure Flag

**[f]_base_SdssShape_flag_badCentroid** (type=boolean): General Failure Flag

**[f]_base_SdssShape_flag_maxIter** (type=boolean): Too many iterations in adaptive moments

**[f]_base_SdssShape_flag_psf** (type=boolean): Failure in measuring PSF model shape

**[f]_base_SdssShape_flag_shift** (type=boolean): centroid shifted by more than the maximum allowed amount

**[f]_base_SdssShape_flag_unweighted** (type=boolean): Weighted moments converged to an invalid value; using unweighted moments

**[f]_base_SdssShape_flag_unweightedBad** (type=boolean): Both weighted and unweighted moments were invalid

**[f]_base_SdssShape_instFlux** (unit=count, type=double): elliptical Gaussian adaptive moments

**[f]_base_SdssShape_instFlux_xx_Cov** (unit=count*pixel^2, type=double): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xx

**[f]_base_SdssShape_instFlux_xy_Cov** (unit=count*pixel^2, type=double): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xy

**[f]_base_SdssShape_instFlux_yy_Cov** (unit=count*pixel^2, type=double): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_yy

**[f]_base_SdssShape_instFluxErr** (unit=count, type=double): 1-sigma instFlux uncertainty

**[f]_base_SdssShape_psf_xx** (unit=pixel^2, type=double): adaptive moments of the PSF model at the object position

**[f]_base_SdssShape_psf_xy** (unit=pixel^2, type=double): adaptive moments of the PSF model at the object position

**[f]_base_SdssShape_psf_yy** (unit=pixel^2, type=double): adaptive moments of the PSF model at the object position

**[f]_base_SdssShape_x** (unit=pixel, type=double): elliptical Gaussian adaptive moments

**[f]_base_SdssShape_xx** (unit=pixel^2, type=double): elliptical Gaussian adaptive moments

**[f]_base_SdssShape_xxErr** (unit=pixel^2, type=double): Standard deviation of xx moment

**[f]_base_SdssShape_xy** (unit=pixel^2, type=double): elliptical Gaussian adaptive moments

**[f]_base_SdssShape_xyErr** (unit=pixel^2, type=double): Standard deviation of xy moment

**[f]_base_SdssShape_y** (unit=pixel, type=double): elliptical Gaussian adaptive moments

**[f]_base_SdssShape_yy** (unit=pixel^2, type=double): elliptical Gaussian adaptive moments

**[f]_base_SdssShape_yyErr** (unit=pixel^2, type=double): Standard deviation of yy moment

**[f]_base_Variance_flag** (type=boolean): Set for any fatal failure

**[f]_base_Variance_flag_badCentroid** (type=boolean): General Failure Flag

**[f]_base_Variance_flag_emptyFootprint** (type=boolean): Set to True when the footprint has no usable pixels

**[f]_base_Variance_value** (type=double): Variance at object position

**[f]_modelfit_CModel_apCorr** (type=double): aperture correction applied to modelfit_CModel

**[f]_modelfit_CModel_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel

**[f]_modelfit_CModel_dev_apCorr** (type=double): aperture correction applied to modelfit_CModel_dev

**[f]_modelfit_CModel_dev_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel_dev

**[f]_modelfit_CModel_dev_flag** (type=boolean): flag set when the flux for the de Vaucouleur flux failed

**[f]_modelfit_CModel_dev_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel_dev

**[f]_modelfit_CModel_dev_flag_badReference** (type=boolean): The original fit in the reference catalog failed.

**[f]_modelfit_CModel_dev_flag_numericError** (type=boolean): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**[f]_modelfit_CModel_dev_flux_inner** (unit=count, type=double): flux from the de Vaucouleur fit region, with no extrapolation

**[f]_modelfit_CModel_dev_instFlux** (unit=count, type=double): flux from the de Vaucouleur fit

**[f]_modelfit_CModel_dev_instFluxErr** (unit=count, type=double): flux uncertainty from the de Vaucouleur fit

**[f]_modelfit_CModel_exp_apCorr** (type=double): aperture correction applied to modelfit_CModel_exp

**[f]_modelfit_CModel_exp_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel_exp

**[f]_modelfit_CModel_exp_flag** (type=boolean): flag set when the flux for the exponential flux failed

**[f]_modelfit_CModel_exp_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel_exp

**[f]_modelfit_CModel_exp_flag_badReference** (type=boolean): The original fit in the reference catalog failed.

**[f]_modelfit_CModel_exp_flag_numericError** (type=boolean): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**[f]_modelfit_CModel_exp_flux_inner** (unit=count, type=double): flux from the exponential fit region, with no extrapolation

**[f]_modelfit_CModel_exp_instFlux** (unit=count, type=double): flux from the exponential fit

**[f]_modelfit_CModel_exp_instFluxErr** (unit=count, type=double): flux uncertainty from the exponential fit

**[f]_modelfit_CModel_flag** (type=boolean): flag set if the final cmodel fit (or any previous fit) failed

**[f]_modelfit_CModel_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel

**[f]_modelfit_CModel_flag_badCentroid** (type=boolean): input centroid was not within the fit region (probably because it''s not within the Footprint)

**[f]_modelfit_CModel_flag_badReference** (type=boolean): The original fit in the reference catalog failed.

**[f]_modelfit_CModel_flag_noShapeletPsf** (type=boolean): the multishapelet fit to the PSF model did not succeed

**[f]_modelfit_CModel_flag_region_maxArea** (type=boolean): number of pixels in fit region exceeded the region.maxArea value

**[f]_modelfit_CModel_flag_region_maxBadPixelFraction** (type=boolean): the fraction of bad/clipped pixels in the fit region exceeded region.maxBadPixelFraction

**[f]_modelfit_CModel_fracDev** (type=double): fraction of flux in de Vaucouleur component

**[f]_modelfit_CModel_initial_apCorr** (type=double): aperture correction applied to modelfit_CModel_initial

**[f]_modelfit_CModel_initial_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel_initial

**[f]_modelfit_CModel_initial_flag** (type=boolean): flag set when the flux for the initial flux failed

**[f]_modelfit_CModel_initial_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel_initial

**[f]_modelfit_CModel_initial_flag_badReference** (type=boolean): The original fit in the reference catalog failed.

**[f]_modelfit_CModel_initial_flag_numericError** (type=boolean): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**[f]_modelfit_CModel_initial_flux_inner** (unit=count, type=double): flux from the initial fit region, with no extrapolation

**[f]_modelfit_CModel_initial_instFlux** (unit=count, type=double): flux from the initial fit

**[f]_modelfit_CModel_initial_instFluxErr** (unit=count, type=double): flux uncertainty from the initial fit

**[f]_modelfit_CModel_instFlux_inner** (unit=count, type=double): flux within the fit region, with no extrapolation

**[f]_modelfit_CModel_objective** (type=double): -ln(likelihood) (chi^2) in cmodel fit
