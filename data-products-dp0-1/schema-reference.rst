.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-1-schema-reference:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

.. This file will not be included in a toctree because it is a reference page.
.. The ``orphan`` metadata field is used to suppress the "WARNING: document isn't included in any toctree."

:orphan:

######################################
Schema for dp01_dc2_catalogs.reference
######################################

.. This section should provide a brief, top-level description of the page.

This page is a reference to schema for measurements for objects detected in the coadded images.
Other schemas are listed under :ref:`DP0-1-Data-Products-DPDD-Catalogs`.

Principal Columns
=================

**base_ClassificationExtendedness_value** (type=double): Set to 1 for extended sources, 0 for point sources.

**coord_dec** (unit=rad, type=double): position in ra/dec

**coord_ra** (unit=rad, type=double): position in ra/dec

**deblend_deblendedAsPsf** (type=boolean): Deblender thought this source looked like a PSF

**deblend_skipped** (type=boolean): Deblender skipped this source

**good** (type=boolean): True if the source has no flagged pixels.

**modelfit_CModel_flag** (type=boolean): flag set if the final cmodel fit (or any previous fit) failed

**objectId** (type=long): Unique id.


All Other Columns
=================

**base_Blendedness_abs** (type=double): Measure of how much the flux is affected by neighbors: (1 - child_instFlux/parent_instFlux).  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_child_xx** (unit=pixel^2, type=double): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_child_xy** (unit=pixel^2, type=double): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_child_yy** (unit=pixel^2, type=double): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_instFlux** (type=double): measure of how instFlux is affected by neighbors: (1 - instFlux.child/instFlux.parent)

**base_Blendedness_abs_instFlux_child** (unit=count, type=double): instFlux of the child, measured with a Gaussian weight matched to the child

**base_Blendedness_abs_instFlux_parent** (unit=count, type=double): instFlux of the parent, measured with a Gaussian weight matched to the child

**base_Blendedness_abs_parent_xx** (unit=pixel^2, type=double): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_parent_xy** (unit=pixel^2, type=double): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_parent_yy** (unit=pixel^2, type=double): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_flag** (type=boolean): General Failure Flag

**base_Blendedness_flag_noCentroid** (type=boolean): Object has no centroid

**base_Blendedness_flag_noShape** (type=boolean): Object has no shape

**base_Blendedness_old** (type=double): Blendedness from dot products: (child.dot(parent)/child.dot(child) - 1)

**base_Blendedness_raw_child_xx** (unit=pixel^2, type=double): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_child_xy** (unit=pixel^2, type=double): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_child_yy** (unit=pixel^2, type=double): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_instFlux** (type=double): measure of how instFlux is affected by neighbors: (1 - instFlux.child/instFlux.parent)

**base_Blendedness_raw_instFlux_child** (unit=count, type=double): instFlux of the child, measured with a Gaussian weight matched to the child

**base_Blendedness_raw_instFlux_parent** (unit=count, type=double): instFlux of the parent, measured with a Gaussian weight matched to the child

**base_Blendedness_raw_parent_xx** (unit=pixel^2, type=double): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_parent_xy** (unit=pixel^2, type=double): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_parent_yy** (unit=pixel^2, type=double): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_ClassificationExtendedness_flag** (type=boolean): Set to 1 for any fatal failure.

**base_PixelFlags_flag** (type=boolean): General failure flag, set if anything went wrong

**base_PixelFlags_flag_bad** (type=boolean): Bad pixel in the Source footprint

**base_PixelFlags_flag_bright_object** (type=boolean): Source footprint includes BRIGHT_OBJECT pixels

**base_PixelFlags_flag_bright_objectCenter** (type=boolean): Source center is close to BRIGHT_OBJECT pixels

**base_PixelFlags_flag_clipped** (type=boolean): Source footprint includes CLIPPED pixels

**base_PixelFlags_flag_clippedCenter** (type=boolean): Source center is close to CLIPPED pixels

**base_PixelFlags_flag_cr** (type=boolean): Cosmic ray in the Source footprint

**base_PixelFlags_flag_crCenter** (type=boolean): Cosmic ray in the Source center

**base_PixelFlags_flag_edge** (type=boolean): Source is outside usable exposure region (masked EDGE or NO_DATA)

**base_PixelFlags_flag_inexact_psf** (type=boolean): Source footprint includes INEXACT_PSF pixels

**base_PixelFlags_flag_inexact_psfCenter** (type=boolean): Source center is close to INEXACT_PSF pixels

**base_PixelFlags_flag_interpolated** (type=boolean): Interpolated pixel in the Source footprint

**base_PixelFlags_flag_interpolatedCenter** (type=boolean): Interpolated pixel in the Source center

**base_PixelFlags_flag_offimage** (type=boolean): Source center is off image

**base_PixelFlags_flag_saturated** (type=boolean): Saturated pixel in the Source footprint

**base_PixelFlags_flag_saturatedCenter** (type=boolean): Saturated pixel in the Source center

**base_PixelFlags_flag_sensor_edge** (type=boolean): Source footprint includes SENSOR_EDGE pixels

**base_PixelFlags_flag_sensor_edgeCenter** (type=boolean): Source center is close to SENSOR_EDGE pixels

**base_PixelFlags_flag_suspect** (type=boolean): Source''s footprint includes suspect pixels

**base_PixelFlags_flag_suspectCenter** (type=boolean): Source''s center is close to suspect pixels

**base_PsfFlux_apCorr** (type=double): aperture correction applied to base_PsfFlux

**base_PsfFlux_apCorrErr** (type=double): standard deviation of aperture correction applied to base_PsfFlux

**base_PsfFlux_area** (unit=pixel, type=double): effective area of PSF

**base_PsfFlux_flag** (type=boolean): General Failure Flag

**base_PsfFlux_flag_apCorr** (type=boolean): set if unable to aperture correct base_PsfFlux

**base_PsfFlux_flag_badCentroid** (type=boolean): General Failure Flag

**base_PsfFlux_flag_edge** (type=boolean): object was too close to the edge of the image to use the full PSF model

**base_PsfFlux_flag_noGoodPixels** (type=boolean): not enough non-rejected pixels in data to attempt the fit

**base_PsfFlux_instFlux** (unit=count, type=double): instFlux derived from linear least-squares fit of PSF model

**base_PsfFlux_instFluxErr** (unit=count, type=double): 1-sigma instFlux uncertainty

**base_SdssCentroid_flag** (type=boolean): General Failure Flag

**base_SdssCentroid_flag_almostNoSecondDerivative** (type=boolean): Almost vanishing second derivative

**base_SdssCentroid_flag_edge** (type=boolean): Object too close to edge

**base_SdssCentroid_flag_noSecondDerivative** (type=boolean): Vanishing second derivative

**base_SdssCentroid_flag_notAtMaximum** (type=boolean): Object is not at a maximum

**base_SdssCentroid_flag_resetToPeak** (type=boolean): set if CentroidChecker reset the centroid

**base_SdssCentroid_x** (unit=pixel, type=double): centroid from Sdss Centroid algorithm

**base_SdssCentroid_xErr** (unit=pixel, type=double): 1-sigma uncertainty on x position

**base_SdssCentroid_y** (unit=pixel, type=double): centroid from Sdss Centroid algorithm

**base_SdssCentroid_yErr** (unit=pixel, type=double): 1-sigma uncertainty on y position

**base_SdssShape_flag** (type=boolean): General Failure Flag

**base_SdssShape_flag_badCentroid** (type=boolean): General Failure Flag

**base_SdssShape_flag_maxIter** (type=boolean): Too many iterations in adaptive moments

**base_SdssShape_flag_psf** (type=boolean): Failure in measuring PSF model shape

**base_SdssShape_flag_shift** (type=boolean): centroid shifted by more than the maximum allowed amount

**base_SdssShape_flag_unweighted** (type=boolean): Weighted moments converged to an invalid value; using unweighted moments

**base_SdssShape_flag_unweightedBad** (type=boolean): Both weighted and unweighted moments were invalid

**base_SdssShape_instFlux** (unit=count, type=double): elliptical Gaussian adaptive moments

**base_SdssShape_instFlux_xx_Cov** (unit=count*pixel^2, type=double): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xx

**base_SdssShape_instFlux_xy_Cov** (unit=count*pixel^2, type=double): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xy

**base_SdssShape_instFlux_yy_Cov** (unit=count*pixel^2, type=double): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_yy

**base_SdssShape_instFluxErr** (unit=count, type=double): 1-sigma instFlux uncertainty

**base_SdssShape_psf_xx** (unit=pixel^2, type=double): adaptive moments of the PSF model at the object position

**base_SdssShape_psf_xy** (unit=pixel^2, type=double): adaptive moments of the PSF model at the object position

**base_SdssShape_psf_yy** (unit=pixel^2, type=double): adaptive moments of the PSF model at the object position

**base_SdssShape_x** (unit=pixel, type=double): elliptical Gaussian adaptive moments

**base_SdssShape_xx** (unit=pixel^2, type=double): elliptical Gaussian adaptive moments

**base_SdssShape_xxErr** (unit=pixel^2, type=double): Standard deviation of xx moment

**base_SdssShape_xy** (unit=pixel^2, type=double): elliptical Gaussian adaptive moments

**base_SdssShape_xyErr** (unit=pixel^2, type=double): Standard deviation of xy moment

**base_SdssShape_y** (unit=pixel, type=double): elliptical Gaussian adaptive moments

**base_SdssShape_yy** (unit=pixel^2, type=double): elliptical Gaussian adaptive moments

**base_SdssShape_yyErr** (unit=pixel^2, type=double): Standard deviation of yy moment

**deblend_hasStrayFlux** (type=boolean): This source was assigned some stray flux

**deblend_masked** (type=boolean): Parent footprint was predominantly masked

**deblend_parentTooBig** (type=boolean): Parent footprint covered too many pixels

**deblend_patchedTemplate** (type=boolean): This source was near an image edge and the deblender used "patched" edge-handling.

**deblend_psf_instFlux** (unit=count, type=double): If deblended-as-psf, the instrumental PSF flux

**deblend_psfCenter_x** (unit=pixel, type=double): If deblended-as-psf, the PSF centroid

**deblend_psfCenter_y** (unit=pixel, type=double): If deblended-as-psf, the PSF centroid

**deblend_psfflux** (unit=count, type=double): If deblended-as-psf, the instrumental PSF flux

**deblend_rampedTemplate** (type=boolean): This source was near an image edge and the deblender used "ramp" edge-handling.

**deblend_tooManyPeaks** (type=boolean): Source had too many peaks; only the brightest were included

**ext_shapeHSM_HsmPsfMoments_flag** (type=boolean): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid** (type=boolean): General Failure Flag

**ext_shapeHSM_HsmPsfMoments_flag_no_pixels** (type=boolean): no pixels to measure

**ext_shapeHSM_HsmPsfMoments_flag_not_contained** (type=boolean): center not contained in footprint bounding box

**ext_shapeHSM_HsmPsfMoments_flag_parent_source** (type=boolean): parent source, ignored

**ext_shapeHSM_HsmPsfMoments_x** (unit=pixel, type=double): HSM Centroid

**ext_shapeHSM_HsmPsfMoments_xx** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmPsfMoments_xy** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmPsfMoments_y** (unit=pixel, type=double): HSM Centroid

**ext_shapeHSM_HsmPsfMoments_yy** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmShapeRegauss_e1** (type=double): PSF-corrected shear using Hirata & Seljak (2003) ''regaussianization

**ext_shapeHSM_HsmShapeRegauss_e2** (type=double): PSF-corrected shear using Hirata & Seljak (2003) ''regaussianization

**ext_shapeHSM_HsmShapeRegauss_flag** (type=boolean): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid** (type=boolean): General Failure Flag

**ext_shapeHSM_HsmShapeRegauss_flag_galsim** (type=boolean): GalSim failure

**ext_shapeHSM_HsmShapeRegauss_flag_no_pixels** (type=boolean): no pixels to measure

**ext_shapeHSM_HsmShapeRegauss_flag_not_contained** (type=boolean): center not contained in footprint bounding box

**ext_shapeHSM_HsmShapeRegauss_flag_parent_source** (type=boolean): parent source, ignored

**ext_shapeHSM_HsmShapeRegauss_resolution** (type=double): resolution factor (0=unresolved, 1=resolved)

**ext_shapeHSM_HsmShapeRegauss_sigma** (type=double): PSF-corrected shear using Hirata & Seljak (2003) ''regaussianization

**ext_shapeHSM_HsmSourceMoments_flag** (type=boolean): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid** (type=boolean): General Failure Flag

**ext_shapeHSM_HsmSourceMoments_flag_no_pixels** (type=boolean): no pixels to measure

**ext_shapeHSM_HsmSourceMoments_flag_not_contained** (type=boolean): center not contained in footprint bounding box

**ext_shapeHSM_HsmSourceMoments_flag_parent_source** (type=boolean): parent source, ignored

**ext_shapeHSM_HsmSourceMoments_x** (unit=pixel, type=double): HSM Centroid

**ext_shapeHSM_HsmSourceMoments_xx** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmSourceMoments_xy** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmSourceMoments_y** (unit=pixel, type=double): HSM Centroid

**ext_shapeHSM_HsmSourceMoments_yy** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmSourceMomentsRound_flag** (type=boolean): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid** (type=boolean): General Failure Flag

**ext_shapeHSM_HsmSourceMomentsRound_flag_no_pixels** (type=boolean): no pixels to measure

**ext_shapeHSM_HsmSourceMomentsRound_flag_not_contained** (type=boolean): center not contained in footprint bounding box

**ext_shapeHSM_HsmSourceMomentsRound_flag_parent_source** (type=boolean): parent source, ignored

**ext_shapeHSM_HsmSourceMomentsRound_Flux** (type=double): HSM flux

**ext_shapeHSM_HsmSourceMomentsRound_x** (unit=pixel, type=double): HSM Centroid

**ext_shapeHSM_HsmSourceMomentsRound_xx** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmSourceMomentsRound_xy** (unit=pixel^2, type=double): HSM moments

**ext_shapeHSM_HsmSourceMomentsRound_y** (unit=pixel, type=double): HSM Centroid

**ext_shapeHSM_HsmSourceMomentsRound_yy** (unit=pixel^2, type=double): HSM moments

**modelfit_CModel_apCorr** (type=double): aperture correction applied to modelfit_CModel

**modelfit_CModel_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel

**modelfit_CModel_dev_apCorr** (type=double): aperture correction applied to modelfit_CModel_dev

**modelfit_CModel_dev_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel_dev

**modelfit_CModel_dev_ellipse_xx** (unit=pixel^2, type=double): half-light ellipse of the de Vaucouleur fit

**modelfit_CModel_dev_ellipse_xy** (unit=pixel^2, type=double): half-light ellipse of the de Vaucouleur fit

**modelfit_CModel_dev_ellipse_yy** (unit=pixel^2, type=double): half-light ellipse of the de Vaucouleur fit

**modelfit_CModel_dev_fixed_0** (type=double): fixed parameters for the de Vaucouleur fit

**modelfit_CModel_dev_fixed_1** (type=double): fixed parameters for the de Vaucouleur fit

**modelfit_CModel_dev_flag** (type=boolean): flag set when the flux for the de Vaucouleur flux failed

**modelfit_CModel_dev_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel_dev

**modelfit_CModel_dev_flag_maxIter** (type=boolean): the optimizer hit the maximum number of iterations and did not converge

**modelfit_CModel_dev_flag_numericError** (type=boolean): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**modelfit_CModel_dev_flag_trSmall** (type=boolean): the optimizer converged because the trust radius became too small; this is a less-secure result than when the gradient is below the threshold, but usually not a problem

**modelfit_CModel_dev_flux_inner** (unit=count, type=double): flux from the de Vaucouleur fit region, with no extrapolation

**modelfit_CModel_dev_instFlux** (unit=count, type=double): flux from the de Vaucouleur fit

**modelfit_CModel_dev_instFluxErr** (unit=count, type=double): flux uncertainty from the de Vaucouleur fit

**modelfit_CModel_dev_nIter** (type=int): Number of total iterations in stage

**modelfit_CModel_dev_nonlinear_0** (type=double): nonlinear parameters for the de Vaucouleur fit

**modelfit_CModel_dev_nonlinear_1** (type=double): nonlinear parameters for the de Vaucouleur fit

**modelfit_CModel_dev_nonlinear_2** (type=double): nonlinear parameters for the de Vaucouleur fit

**modelfit_CModel_dev_objective** (type=double): -ln(likelihood*prior) at best-fit point for the de Vaucouleur fit

**modelfit_CModel_dev_time** (unit=second, type=double): Time spent in stage

**modelfit_CModel_ellipse_xx** (unit=pixel^2, type=double): fracDev-weighted average of exp.ellipse and dev.ellipse

**modelfit_CModel_ellipse_xy** (unit=pixel^2, type=double): fracDev-weighted average of exp.ellipse and dev.ellipse

**modelfit_CModel_ellipse_yy** (unit=pixel^2, type=double): fracDev-weighted average of exp.ellipse and dev.ellipse

**modelfit_CModel_exp_apCorr** (type=double): aperture correction applied to modelfit_CModel_exp

**modelfit_CModel_exp_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel_exp

**modelfit_CModel_exp_ellipse_xx** (unit=pixel^2, type=double): half-light ellipse of the exponential fit

**modelfit_CModel_exp_ellipse_xy** (unit=pixel^2, type=double): half-light ellipse of the exponential fit

**modelfit_CModel_exp_ellipse_yy** (unit=pixel^2, type=double): half-light ellipse of the exponential fit

**modelfit_CModel_exp_fixed_0** (type=double): fixed parameters for the exponential fit

**modelfit_CModel_exp_fixed_1** (type=double): fixed parameters for the exponential fit

**modelfit_CModel_exp_flag** (type=boolean): flag set when the flux for the exponential flux failed

**modelfit_CModel_exp_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel_exp

**modelfit_CModel_exp_flag_maxIter** (type=boolean): the optimizer hit the maximum number of iterations and did not converge

**modelfit_CModel_exp_flag_numericError** (type=boolean): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**modelfit_CModel_exp_flag_trSmall** (type=boolean): the optimizer converged because the trust radius became too small; this is a less-secure result than when the gradient is below the threshold, but usually not a problem

**modelfit_CModel_exp_flux_inner** (unit=count, type=double): flux from the exponential fit region, with no extrapolation

**modelfit_CModel_exp_instFlux** (unit=count, type=double): flux from the exponential fit

**modelfit_CModel_exp_instFluxErr** (unit=count, type=double): flux uncertainty from the exponential fit

**modelfit_CModel_exp_nIter** (type=int): Number of total iterations in stage

**modelfit_CModel_exp_nonlinear_0** (type=double): nonlinear parameters for the exponential fit

**modelfit_CModel_exp_nonlinear_1** (type=double): nonlinear parameters for the exponential fit

**modelfit_CModel_exp_nonlinear_2** (type=double): nonlinear parameters for the exponential fit

**modelfit_CModel_exp_objective** (type=double): -ln(likelihood*prior) at best-fit point for the exponential fit

**modelfit_CModel_exp_time** (unit=second, type=double): Time spent in stage

**modelfit_CModel_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel

**modelfit_CModel_flag_badCentroid** (type=boolean): input centroid was not within the fit region (probably because it''s not within the Footprint)

**modelfit_CModel_flag_noShape** (type=boolean): the shape slot needed to initialize the parameters failed or was not defined

**modelfit_CModel_flag_noShapeletPsf** (type=boolean): the multishapelet fit to the PSF model did not succeed

**modelfit_CModel_flag_region_maxArea** (type=boolean): number of pixels in fit region exceeded the region.maxArea value

**modelfit_CModel_flag_region_maxBadPixelFraction** (type=boolean): the fraction of bad/clipped pixels in the fit region exceeded region.maxBadPixelFraction

**modelfit_CModel_flags_region_usedFootprintArea** (type=boolean): the pixel region for the initial fit was defined by the area of the Footprint

**modelfit_CModel_flags_region_usedInitialEllipseMax** (type=boolean): the pixel region for the final fit was set to the upper bound defined by the initial fit

**modelfit_CModel_flags_region_usedInitialEllipseMin** (type=boolean): the pixel region for the final fit was set to the lower bound defined by the initial fit

**modelfit_CModel_flags_region_usedPsfArea** (type=boolean): the pixel region for the initial fit was set to a fixed factor of the PSF area

**modelfit_CModel_flags_smallShape** (type=boolean): initial parameter guess resulted in negative radius; used minimum of 0.100000 pixels instead.

**modelfit_CModel_fracDev** (type=double): fraction of flux in de Vaucouleur component

**modelfit_CModel_initial_apCorr** (type=double): aperture correction applied to modelfit_CModel_initial

**modelfit_CModel_initial_apCorrErr** (type=double): standard deviation of aperture correction applied to modelfit_CModel_initial

**modelfit_CModel_initial_ellipse_xx** (unit=pixel^2, type=double): half-light ellipse of the initial fit

**modelfit_CModel_initial_ellipse_xy** (unit=pixel^2, type=double): half-light ellipse of the initial fit

**modelfit_CModel_initial_ellipse_yy** (unit=pixel^2, type=double): half-light ellipse of the initial fit

**modelfit_CModel_initial_fixed_0** (type=double): fixed parameters for the initial fit

**modelfit_CModel_initial_fixed_1** (type=double): fixed parameters for the initial fit

**modelfit_CModel_initial_flag** (type=boolean): flag set when the flux for the initial flux failed

**modelfit_CModel_initial_flag_apCorr** (type=boolean): set if unable to aperture correct modelfit_CModel_initial

**modelfit_CModel_initial_flag_maxIter** (type=boolean): the optimizer hit the maximum number of iterations and did not converge

**modelfit_CModel_initial_flag_numericError** (type=boolean): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**modelfit_CModel_initial_flag_trSmall** (type=boolean): the optimizer converged because the trust radius became too small; this is a less-secure result than when the gradient is below the threshold, but usually not a problem

**modelfit_CModel_initial_flux_inner** (unit=count, type=double): flux from the initial fit region, with no extrapolation

**modelfit_CModel_initial_instFlux** (unit=count, type=double): flux from the initial fit

**modelfit_CModel_initial_instFluxErr** (unit=count, type=double): flux uncertainty from the initial fit

**modelfit_CModel_initial_nIter** (type=int): Number of total iterations in stage

**modelfit_CModel_initial_nonlinear_0** (type=double): nonlinear parameters for the initial fit

**modelfit_CModel_initial_nonlinear_1** (type=double): nonlinear parameters for the initial fit

**modelfit_CModel_initial_nonlinear_2** (type=double): nonlinear parameters for the initial fit

**modelfit_CModel_initial_objective** (type=double): -ln(likelihood*prior) at best-fit point for the initial fit

**modelfit_CModel_initial_time** (unit=second, type=double): Time spent in stage

**modelfit_CModel_instFlux** (unit=count, type=double): flux from the final cmodel fit

**modelfit_CModel_instFlux_inner** (unit=count, type=double): flux within the fit region, with no extrapolation

**modelfit_CModel_instFluxErr** (unit=count, type=double): flux uncertainty from the final cmodel fit

**modelfit_CModel_objective** (type=double): -ln(likelihood) (chi^2) in cmodel fit

**modelfit_CModel_region_final_ellipse_xx** (unit=pixel^2, type=double): ellipse used to set the pixel region for the final fit (before applying bad pixel mask)

**modelfit_CModel_region_final_ellipse_xy** (unit=pixel^2, type=double): ellipse used to set the pixel region for the final fit (before applying bad pixel mask)

**modelfit_CModel_region_final_ellipse_yy** (unit=pixel^2, type=double): ellipse used to set the pixel region for the final fit (before applying bad pixel mask)

**modelfit_CModel_region_initial_ellipse_xx** (unit=pixel^2, type=double): ellipse used to set the pixel region for the initial fit (before applying bad pixel mask)

**modelfit_CModel_region_initial_ellipse_xy** (unit=pixel^2, type=double): ellipse used to set the pixel region for the initial fit (before applying bad pixel mask)

**modelfit_CModel_region_initial_ellipse_yy** (unit=pixel^2, type=double): ellipse used to set the pixel region for the initial fit (before applying bad pixel mask)
