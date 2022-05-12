.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-2-schema-deepCoadd-forced-src:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

.. This file will not be included in a toctree because it is a reference page.
.. The ``orphan`` metadata field is used to suppress the "WARNING: document isn't included in any toctree."

:orphan:

##############################################
Schema for Butler catalog deepCoadd_forced_src
##############################################

.. This section should provide a brief, top-level description of the page.

This page is a reference to schema for forced photometry for sources in deep coadded images.
Other schemas are listed under :ref:`DP0-2-Data-Products-DPDD-Catalogs`.

**id** (units=None,type=int64): unique ID

**coord_ra** (units=rad,type=float64): position in ra/dec

**coord_dec** (units=rad,type=float64): position in ra/dec

**parent** (units=None,type=int64): unique ID of parent source

**deblend_nChild** (units=None,type=int32): Number of children this object has (defaults to 0)

**base_SdssCentroid_x** (units=pix,type=float64): centroid from Sdss Centroid algorithm

**base_SdssCentroid_y** (units=pix,type=float64): centroid from Sdss Centroid algorithm

**base_SdssCentroid_xErr** (units=pix,type=float32): 1-sigma uncertainty on x position

**base_SdssCentroid_yErr** (units=pix,type=float32): 1-sigma uncertainty on y position

**base_SdssCentroid_flag** (units=None,type=bool): General Failure Flag

**base_SdssCentroid_flag_edge** (units=None,type=bool): Object too close to edge

**base_SdssCentroid_flag_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_SdssCentroid_flag_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_SdssCentroid_flag_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_SdssCentroid_flag_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_SdssCentroid_flag_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_TransformedCentroid_x** (units=pix,type=float64): transformed reference centroid column

**slot_Centroid_x** (units=pix,type=float64): transformed reference centroid column

**base_TransformedCentroid_y** (units=pix,type=float64): transformed reference centroid row

**slot_Centroid_y** (units=pix,type=float64): transformed reference centroid row

**base_TransformedCentroid_flag** (units=None,type=bool): whether the reference centroid is marked as bad

**base_CircularApertureFlux_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_GaussianFlux_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_InputCount_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_LocalBackground_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_PsfFlux_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_SdssCentroid_flag_badInitialCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_SdssShape_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_Variance_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**ext_convolved_ConvolvedFlux_0_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**ext_convolved_ConvolvedFlux_1_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**ext_convolved_ConvolvedFlux_2_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**ext_convolved_ConvolvedFlux_3_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**ext_convolved_ConvolvedFlux_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**ext_photometryKron_KronFlux_flag_badInitialCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**modelfit_DoubleShapeletPsfApprox_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**slot_Centroid_flag** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_base_CircularApertureFlux_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_base_PsfFlux_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_ext_convolved_ConvolvedFlux_0_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_ext_convolved_ConvolvedFlux_1_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_ext_convolved_ConvolvedFlux_2_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_ext_convolved_ConvolvedFlux_3_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_ext_convolved_ConvolvedFlux_flag_badCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**undeblended_ext_photometryKron_KronFlux_flag_badInitialCentroid** (units=None,type=bool): whether the reference centroid is marked as bad

**base_InputCount_flag** (units=None,type=bool): Set for any fatal failure

**base_InputCount_value** (units=None,type=int32): Number of images contributing at center, not including anyclipping

**base_InputCount_flag_noInputs** (units=None,type=bool): No coadd inputs available

**base_SdssShape_xx** (units=pix2,type=float64): elliptical Gaussian adaptive moments

**base_SdssShape_yy** (units=pix2,type=float64): elliptical Gaussian adaptive moments

**base_SdssShape_xy** (units=pix2,type=float64): elliptical Gaussian adaptive moments

**base_SdssShape_xxErr** (units=pix2,type=float32): Standard deviation of xx moment

**base_SdssShape_yyErr** (units=pix2,type=float32): Standard deviation of yy moment

**base_SdssShape_xyErr** (units=pix2,type=float32): Standard deviation of xy moment

**base_SdssShape_x** (units=pix,type=float64): elliptical Gaussian adaptive moments

**base_SdssShape_y** (units=pix,type=float64): elliptical Gaussian adaptive moments

**base_SdssShape_instFlux** (units=ct,type=float64): elliptical Gaussian adaptive moments

**base_SdssShape_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_SdssShape_psf_xx** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**slot_PsfShape_xx** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**base_SdssShape_psf_yy** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**slot_PsfShape_yy** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**base_SdssShape_psf_xy** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**slot_PsfShape_xy** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**base_SdssShape_instFlux_xx_Cov** (units=ct pix2,type=float32): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xx

**base_SdssShape_instFlux_yy_Cov** (units=ct pix2,type=float32): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_yy

**base_SdssShape_instFlux_xy_Cov** (units=ct pix2,type=float32): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xy

**base_SdssShape_flag** (units=None,type=bool): General Failure Flag

**base_SdssShape_flag_unweightedBad** (units=None,type=bool): Both weighted and unweighted moments were invalid

**base_SdssShape_flag_unweighted** (units=None,type=bool): Weighted moments converged to an invalid value; using unweighted moments

**base_SdssShape_flag_shift** (units=None,type=bool): centroid shifted by more than the maximum allowed amount

**base_SdssShape_flag_maxIter** (units=None,type=bool): Too many iterations in adaptive moments

**base_SdssShape_flag_psf** (units=None,type=bool): Failure in measuring PSF model shape

**base_TransformedShape_xx** (units=pix2,type=float64): transformed reference shape x^2 moment

**slot_Shape_xx** (units=pix2,type=float64): transformed reference shape x^2 moment

**base_TransformedShape_yy** (units=pix2,type=float64): transformed reference shape y^2 moment

**slot_Shape_yy** (units=pix2,type=float64): transformed reference shape y^2 moment

**base_TransformedShape_xy** (units=pix2,type=float64): transformed reference shape xy moment

**slot_Shape_xy** (units=pix2,type=float64): transformed reference shape xy moment

**base_TransformedShape_flag** (units=None,type=bool): whether the reference shape is marked as bad

**base_GaussianFlux_flag_badShape** (units=None,type=bool): whether the reference shape is marked as bad

**slot_Shape_flag** (units=None,type=bool): whether the reference shape is marked as bad

**modelfit_DoubleShapeletPsfApprox_0_xx** (units=pix2,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_yy** (units=pix2,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_xy** (units=pix2,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_x** (units=pix,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_y** (units=pix,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_0** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_1** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_2** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_3** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_4** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_0_5** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_xx** (units=pix2,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_yy** (units=pix2,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_xy** (units=pix2,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_x** (units=pix,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_y** (units=pix,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_0** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_1** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_1_2** (units=None,type=float64): Double-Shapelet approximation to the PSF model at the position of this source

**modelfit_DoubleShapeletPsfApprox_flag** (units=None,type=bool): General Failure Flag

**modelfit_DoubleShapeletPsfApprox_flag_invalidPointForPsf** (units=None,type=bool): PSF model could not be evaluated at the source position

**modelfit_DoubleShapeletPsfApprox_flag_invalidMoments** (units=None,type=bool): Moments of the PSF model were not a valid ellipse

**modelfit_DoubleShapeletPsfApprox_flag_maxIterations** (units=None,type=bool): optimizer exceeded the maximum number (inner or outer) iterations

**base_CircularApertureFlux_3_0_instFlux** (units=ct,type=float64): instFlux within 3.000000-pixel aperture

**base_CircularApertureFlux_3_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_3_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_3_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_3_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**base_CircularApertureFlux_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**base_CircularApertureFlux_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_4_5_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**base_CircularApertureFlux_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**base_CircularApertureFlux_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_6_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**base_CircularApertureFlux_9_0_instFlux** (units=ct,type=float64): instFlux within 9.000000-pixel aperture

**base_CircularApertureFlux_9_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_9_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_9_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_9_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**base_CircularApertureFlux_12_0_instFlux** (units=ct,type=float64): instFlux within 12.000000-pixel aperture

**base_CircularApertureFlux_12_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_12_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_12_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_12_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**base_CircularApertureFlux_17_0_instFlux** (units=ct,type=float64): instFlux within 17.000000-pixel aperture

**base_CircularApertureFlux_17_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_17_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_17_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_25_0_instFlux** (units=ct,type=float64): instFlux within 25.000000-pixel aperture

**base_CircularApertureFlux_25_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_25_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_25_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_35_0_instFlux** (units=ct,type=float64): instFlux within 35.000000-pixel aperture

**base_CircularApertureFlux_35_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_35_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_35_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_50_0_instFlux** (units=ct,type=float64): instFlux within 50.000000-pixel aperture

**base_CircularApertureFlux_50_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_50_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_50_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_70_0_instFlux** (units=ct,type=float64): instFlux within 70.000000-pixel aperture

**base_CircularApertureFlux_70_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_70_0_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_70_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_GaussianFlux_instFlux** (units=ct,type=float64): instFlux from Gaussian Flux algorithm

**base_GaussianFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_GaussianFlux_flag** (units=None,type=bool): General Failure Flag

**base_LocalBackground_instFlux** (units=ct,type=float64): background in annulus around source

**base_LocalBackground_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_LocalBackground_flag** (units=None,type=bool): General Failure Flag

**base_LocalBackground_flag_noGoodPixels** (units=None,type=bool): no good pixels in the annulus

**base_LocalBackground_flag_noPsf** (units=None,type=bool): no PSF provided

**base_PixelFlags_flag** (units=None,type=bool): General failure flag, set if anything went wrong

**base_PixelFlags_flag_offimage** (units=None,type=bool): Source center is off image

**base_PixelFlags_flag_edge** (units=None,type=bool): Source is outside usable exposure region (masked EDGE or NO_DATA)

**base_PixelFlags_flag_interpolated** (units=None,type=bool): Interpolated pixel in the Source footprint

**base_PixelFlags_flag_saturated** (units=None,type=bool): Saturated pixel in the Source footprint

**base_PixelFlags_flag_cr** (units=None,type=bool): Cosmic ray in the Source footprint

**base_PixelFlags_flag_bad** (units=None,type=bool): Bad pixel in the Source footprint

**base_PixelFlags_flag_suspect** (units=None,type=bool): Source''s footprint includes suspect pixels

**base_PixelFlags_flag_interpolatedCenter** (units=None,type=bool): Interpolated pixel in the Source center

**base_PixelFlags_flag_saturatedCenter** (units=None,type=bool): Saturated pixel in the Source center

**base_PixelFlags_flag_crCenter** (units=None,type=bool): Cosmic ray in the Source center

**base_PixelFlags_flag_suspectCenter** (units=None,type=bool): Source''s center is close to suspect pixels

**base_PixelFlags_flag_clippedCenter** (units=None,type=bool): Source center is close to CLIPPED pixels

**base_PixelFlags_flag_sensor_edgeCenter** (units=None,type=bool): Source center is close to SENSOR_EDGE pixels

**base_PixelFlags_flag_rejectedCenter** (units=None,type=bool): Source center is close to REJECTED pixels

**base_PixelFlags_flag_inexact_psfCenter** (units=None,type=bool): Source center is close to INEXACT_PSF pixels

**base_PixelFlags_flag_bright_objectCenter** (units=None,type=bool): Source center is close to BRIGHT_OBJECT pixels

**base_PixelFlags_flag_clipped** (units=None,type=bool): Source footprint includes CLIPPED pixels

**base_PixelFlags_flag_sensor_edge** (units=None,type=bool): Source footprint includes SENSOR_EDGE pixels

**base_PixelFlags_flag_rejected** (units=None,type=bool): Source footprint includes REJECTED pixels

**base_PixelFlags_flag_inexact_psf** (units=None,type=bool): Source footprint includes INEXACT_PSF pixels

**base_PixelFlags_flag_bright_object** (units=None,type=bool): Source footprint includes BRIGHT_OBJECT pixels

**base_PsfFlux_instFlux** (units=ct,type=float64): instFlux derived from linear least-squares fit of PSF model

**slot_PsfFlux_instFlux** (units=ct,type=float64): instFlux derived from linear least-squares fit of PSF model

**base_PsfFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**slot_PsfFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_PsfFlux_area** (units=pix,type=float32): effective area of PSF

**slot_PsfFlux_area** (units=pix,type=float32): effective area of PSF

**base_PsfFlux_flag** (units=None,type=bool): General Failure Flag

**slot_PsfFlux_flag** (units=None,type=bool): General Failure Flag

**base_PsfFlux_flag_noGoodPixels** (units=None,type=bool): not enough non-rejected pixels in data to attempt the fit

**slot_PsfFlux_flag_noGoodPixels** (units=None,type=bool): not enough non-rejected pixels in data to attempt the fit

**base_PsfFlux_flag_edge** (units=None,type=bool): object was too close to the edge of the image to use the full PSF model

**slot_PsfFlux_flag_edge** (units=None,type=bool): object was too close to the edge of the image to use the full PSF model

**base_Variance_flag** (units=None,type=bool): Set for any fatal failure

**base_Variance_value** (units=None,type=float64): Variance at object position

**base_Variance_flag_emptyFootprint** (units=None,type=bool): Set to True when the footprint has no usable pixels

**ext_photometryKron_KronFlux_instFlux** (units=ct,type=float64): flux from Kron Flux algorithm

**ext_photometryKron_KronFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_photometryKron_KronFlux_radius** (units=None,type=float32): Kron radius (sqrt(a*b))

**ext_photometryKron_KronFlux_radius_for_radius** (units=None,type=float32): radius used to estimate <radius> (sqrt(a*b))

**ext_photometryKron_KronFlux_psf_radius** (units=None,type=float32): Radius of PSF

**ext_photometryKron_KronFlux_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**ext_photometryKron_KronFlux_flag_edge** (units=None,type=bool): bad measurement due to image edge

**ext_photometryKron_KronFlux_flag_bad_shape_no_psf** (units=None,type=bool): bad shape and no PSF

**ext_photometryKron_KronFlux_flag_no_minimum_radius** (units=None,type=bool): minimum radius could not enforced: no minimum value or PSF

**ext_photometryKron_KronFlux_flag_no_fallback_radius** (units=None,type=bool): no minimum radius and no PSF provided

**ext_photometryKron_KronFlux_flag_bad_radius** (units=None,type=bool): bad Kron radius

**ext_photometryKron_KronFlux_flag_used_minimum_radius** (units=None,type=bool): used the minimum radius for the Kron aperture

**ext_photometryKron_KronFlux_flag_used_psf_radius** (units=None,type=bool): used the PSF Kron radius for the Kron aperture

**ext_photometryKron_KronFlux_flag_small_radius** (units=None,type=bool): measured Kron radius was smaller than that of the PSF

**ext_photometryKron_KronFlux_flag_bad_shape** (units=None,type=bool): shape for measuring Kron radius is bad; used PSF shape

**ext_convolved_ConvolvedFlux_seeing** (units=pix,type=float32): original seeing (Gaussian sigma) at position

**ext_convolved_ConvolvedFlux_0_deconv** (units=None,type=bool): deconvolution required for seeing 3.500000; no measurement made

**ext_convolved_ConvolvedFlux_0_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**ext_convolved_ConvolvedFlux_0_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_0_3_3_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_0_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_0_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_0_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**ext_convolved_ConvolvedFlux_0_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_0_4_5_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_0_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_0_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_0_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**ext_convolved_ConvolvedFlux_0_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_0_6_0_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_0_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_0_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_0_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 3.500000

**ext_convolved_ConvolvedFlux_0_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_0_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 3.500000

**ext_convolved_ConvolvedFlux_1_deconv** (units=None,type=bool): deconvolution required for seeing 5.000000; no measurement made

**ext_convolved_ConvolvedFlux_1_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**ext_convolved_ConvolvedFlux_1_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_1_3_3_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_1_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_1_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_1_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**ext_convolved_ConvolvedFlux_1_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_1_4_5_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_1_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_1_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_1_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**ext_convolved_ConvolvedFlux_1_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_1_6_0_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_1_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_1_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_1_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 5.000000

**ext_convolved_ConvolvedFlux_1_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_1_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 5.000000

**ext_convolved_ConvolvedFlux_2_deconv** (units=None,type=bool): deconvolution required for seeing 6.500000; no measurement made

**ext_convolved_ConvolvedFlux_2_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**ext_convolved_ConvolvedFlux_2_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_2_3_3_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_2_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_2_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_2_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**ext_convolved_ConvolvedFlux_2_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_2_4_5_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_2_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_2_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_2_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**ext_convolved_ConvolvedFlux_2_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_2_6_0_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_2_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_2_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_2_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 6.500000

**ext_convolved_ConvolvedFlux_2_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_2_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 6.500000

**ext_convolved_ConvolvedFlux_3_deconv** (units=None,type=bool): deconvolution required for seeing 8.000000; no measurement made

**ext_convolved_ConvolvedFlux_3_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**ext_convolved_ConvolvedFlux_3_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_3_3_3_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_3_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_3_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_3_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**ext_convolved_ConvolvedFlux_3_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_3_4_5_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_3_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_3_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_3_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**ext_convolved_ConvolvedFlux_3_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_3_6_0_flag** (units=None,type=bool): General Failure Flag

**ext_convolved_ConvolvedFlux_3_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**ext_convolved_ConvolvedFlux_3_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**ext_convolved_ConvolvedFlux_3_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 8.000000

**ext_convolved_ConvolvedFlux_3_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**ext_convolved_ConvolvedFlux_3_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 8.000000

**ext_convolved_ConvolvedFlux_flag** (units=None,type=bool): error in running ConvolvedFluxPlugin

**modelfit_CModel_initial_instFlux** (units=ct,type=float64): flux from the initial fit

**slot_ModelFlux_initial_instFlux** (units=ct,type=float64): flux from the initial fit

**modelfit_CModel_initial_instFluxErr** (units=ct,type=float64): flux uncertainty from the initial fit

**slot_ModelFlux_initial_instFluxErr** (units=ct,type=float64): flux uncertainty from the initial fit

**modelfit_CModel_initial_flag** (units=None,type=bool): flag set when the flux for the initial flux failed

**slot_ModelFlux_initial_flag** (units=None,type=bool): flag set when the flux for the initial flux failed

**modelfit_CModel_initial_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**slot_ModelFlux_initial_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**modelfit_CModel_initial_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**slot_ModelFlux_initial_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**modelfit_CModel_initial_flag_numericError** (units=None,type=bool): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**slot_ModelFlux_initial_flag_numericError** (units=None,type=bool): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**modelfit_CModel_exp_instFlux** (units=ct,type=float64): flux from the exponential fit

**slot_ModelFlux_exp_instFlux** (units=ct,type=float64): flux from the exponential fit

**modelfit_CModel_exp_instFluxErr** (units=ct,type=float64): flux uncertainty from the exponential fit

**slot_ModelFlux_exp_instFluxErr** (units=ct,type=float64): flux uncertainty from the exponential fit

**modelfit_CModel_exp_flag** (units=None,type=bool): flag set when the flux for the exponential flux failed

**slot_ModelFlux_exp_flag** (units=None,type=bool): flag set when the flux for the exponential flux failed

**modelfit_CModel_exp_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**slot_ModelFlux_exp_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**modelfit_CModel_exp_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**slot_ModelFlux_exp_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**modelfit_CModel_exp_flag_numericError** (units=None,type=bool): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**slot_ModelFlux_exp_flag_numericError** (units=None,type=bool): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**modelfit_CModel_dev_instFlux** (units=ct,type=float64): flux from the de Vaucouleur fit

**slot_ModelFlux_dev_instFlux** (units=ct,type=float64): flux from the de Vaucouleur fit

**modelfit_CModel_dev_instFluxErr** (units=ct,type=float64): flux uncertainty from the de Vaucouleur fit

**slot_ModelFlux_dev_instFluxErr** (units=ct,type=float64): flux uncertainty from the de Vaucouleur fit

**modelfit_CModel_dev_flag** (units=None,type=bool): flag set when the flux for the de Vaucouleur flux failed

**slot_ModelFlux_dev_flag** (units=None,type=bool): flag set when the flux for the de Vaucouleur flux failed

**modelfit_CModel_dev_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**slot_ModelFlux_dev_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**modelfit_CModel_dev_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**slot_ModelFlux_dev_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**modelfit_CModel_dev_flag_numericError** (units=None,type=bool): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**slot_ModelFlux_dev_flag_numericError** (units=None,type=bool): numerical underflow or overflow in model evaluation; usually this means the prior was insufficient to regularize the fit, or all pixel values were zero.

**modelfit_CModel_instFlux** (units=ct,type=float64): flux from the final cmodel fit

**slot_ModelFlux_instFlux** (units=ct,type=float64): flux from the final cmodel fit

**modelfit_CModel_instFluxErr** (units=ct,type=float64): flux uncertainty from the final cmodel fit

**slot_ModelFlux_instFluxErr** (units=ct,type=float64): flux uncertainty from the final cmodel fit

**modelfit_CModel_flag** (units=None,type=bool): flag set if the final cmodel fit (or any previous fit) failed

**slot_ModelFlux_flag** (units=None,type=bool): flag set if the final cmodel fit (or any previous fit) failed

**modelfit_CModel_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**slot_ModelFlux_instFlux_inner** (units=ct,type=float64): flux within the fit region, with no extrapolation

**modelfit_CModel_fracDev** (units=None,type=float64): fraction of flux in de Vaucouleur component

**slot_ModelFlux_fracDev** (units=None,type=float64): fraction of flux in de Vaucouleur component

**modelfit_CModel_objective** (units=None,type=float64): -ln(likelihood) (chi^2) in cmodel fit

**slot_ModelFlux_objective** (units=None,type=float64): -ln(likelihood) (chi^2) in cmodel fit

**modelfit_CModel_flag_region_maxArea** (units=None,type=bool): number of pixels in fit region exceeded the region.maxArea value

**slot_ModelFlux_flag_region_maxArea** (units=None,type=bool): number of pixels in fit region exceeded the region.maxArea value

**modelfit_CModel_flag_region_maxBadPixelFraction** (units=None,type=bool): the fraction of bad/clipped pixels in the fit region exceeded region.maxBadPixelFraction

**slot_ModelFlux_flag_region_maxBadPixelFraction** (units=None,type=bool): the fraction of bad/clipped pixels in the fit region exceeded region.maxBadPixelFraction

**modelfit_CModel_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**slot_ModelFlux_flag_badReference** (units=None,type=bool): The original fit in the reference catalog failed.

**modelfit_CModel_flag_noShapeletPsf** (units=None,type=bool): the multishapelet fit to the PSF model did not succeed

**slot_ModelFlux_flag_noShapeletPsf** (units=None,type=bool): the multishapelet fit to the PSF model did not succeed

**modelfit_CModel_flag_badCentroid** (units=None,type=bool): input centroid was not within the fit region (probably because it''s not within the Footprint)

**slot_ModelFlux_flag_badCentroid** (units=None,type=bool): input centroid was not within the fit region (probably because it''s not within the Footprint)

**undeblended_base_CircularApertureFlux_3_0_instFlux** (units=ct,type=float64): instFlux within 3.000000-pixel aperture

**undeblended_base_CircularApertureFlux_3_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_3_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_3_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_3_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_base_CircularApertureFlux_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**undeblended_base_CircularApertureFlux_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_4_5_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_base_CircularApertureFlux_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**undeblended_base_CircularApertureFlux_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_6_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_base_CircularApertureFlux_9_0_instFlux** (units=ct,type=float64): instFlux within 9.000000-pixel aperture

**undeblended_base_CircularApertureFlux_9_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_9_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_9_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_9_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_base_CircularApertureFlux_12_0_instFlux** (units=ct,type=float64): instFlux within 12.000000-pixel aperture

**undeblended_base_CircularApertureFlux_12_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_12_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_12_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_12_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_base_CircularApertureFlux_17_0_instFlux** (units=ct,type=float64): instFlux within 17.000000-pixel aperture

**undeblended_base_CircularApertureFlux_17_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_17_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_17_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_25_0_instFlux** (units=ct,type=float64): instFlux within 25.000000-pixel aperture

**undeblended_base_CircularApertureFlux_25_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_25_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_25_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_35_0_instFlux** (units=ct,type=float64): instFlux within 35.000000-pixel aperture

**undeblended_base_CircularApertureFlux_35_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_35_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_35_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_50_0_instFlux** (units=ct,type=float64): instFlux within 50.000000-pixel aperture

**undeblended_base_CircularApertureFlux_50_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_50_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_50_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_CircularApertureFlux_70_0_instFlux** (units=ct,type=float64): instFlux within 70.000000-pixel aperture

**undeblended_base_CircularApertureFlux_70_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_CircularApertureFlux_70_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_CircularApertureFlux_70_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_base_PsfFlux_instFlux** (units=ct,type=float64): instFlux derived from linear least-squares fit of PSF model

**undeblended_base_PsfFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_base_PsfFlux_area** (units=pix,type=float32): effective area of PSF

**undeblended_base_PsfFlux_flag** (units=None,type=bool): General Failure Flag

**undeblended_base_PsfFlux_flag_noGoodPixels** (units=None,type=bool): not enough non-rejected pixels in data to attempt the fit

**undeblended_base_PsfFlux_flag_edge** (units=None,type=bool): object was too close to the edge of the image to use the full PSF model

**undeblended_ext_photometryKron_KronFlux_instFlux** (units=ct,type=float64): flux from Kron Flux algorithm

**undeblended_ext_photometryKron_KronFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_photometryKron_KronFlux_radius** (units=None,type=float32): Kron radius (sqrt(a*b))

**undeblended_ext_photometryKron_KronFlux_radius_for_radius** (units=None,type=float32): radius used to estimate <radius> (sqrt(a*b))

**undeblended_ext_photometryKron_KronFlux_psf_radius** (units=None,type=float32): Radius of PSF

**undeblended_ext_photometryKron_KronFlux_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**undeblended_ext_photometryKron_KronFlux_flag_edge** (units=None,type=bool): bad measurement due to image edge

**undeblended_ext_photometryKron_KronFlux_flag_bad_shape_no_psf** (units=None,type=bool): bad shape and no PSF

**undeblended_ext_photometryKron_KronFlux_flag_no_minimum_radius** (units=None,type=bool): minimum radius could not enforced: no minimum value or PSF

**undeblended_ext_photometryKron_KronFlux_flag_no_fallback_radius** (units=None,type=bool): no minimum radius and no PSF provided

**undeblended_ext_photometryKron_KronFlux_flag_bad_radius** (units=None,type=bool): bad Kron radius

**undeblended_ext_photometryKron_KronFlux_flag_used_minimum_radius** (units=None,type=bool): used the minimum radius for the Kron aperture

**undeblended_ext_photometryKron_KronFlux_flag_used_psf_radius** (units=None,type=bool): used the PSF Kron radius for the Kron aperture

**undeblended_ext_photometryKron_KronFlux_flag_small_radius** (units=None,type=bool): measured Kron radius was smaller than that of the PSF

**undeblended_ext_photometryKron_KronFlux_flag_bad_shape** (units=None,type=bool): shape for measuring Kron radius is bad; used PSF shape

**undeblended_ext_convolved_ConvolvedFlux_seeing** (units=pix,type=float32): original seeing (Gaussian sigma) at position

**undeblended_ext_convolved_ConvolvedFlux_0_deconv** (units=None,type=bool): deconvolution required for seeing 3.500000; no measurement made

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_0_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 3.500000

**undeblended_ext_convolved_ConvolvedFlux_0_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_0_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 3.500000

**undeblended_ext_convolved_ConvolvedFlux_1_deconv** (units=None,type=bool): deconvolution required for seeing 5.000000; no measurement made

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_1_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 5.000000

**undeblended_ext_convolved_ConvolvedFlux_1_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_1_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 5.000000

**undeblended_ext_convolved_ConvolvedFlux_2_deconv** (units=None,type=bool): deconvolution required for seeing 6.500000; no measurement made

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_2_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 6.500000

**undeblended_ext_convolved_ConvolvedFlux_2_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_2_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 6.500000

**undeblended_ext_convolved_ConvolvedFlux_3_deconv** (units=None,type=bool): deconvolution required for seeing 8.000000; no measurement made

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_instFlux** (units=ct,type=float64): instFlux within 3.300000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_instFlux** (units=ct,type=float64): instFlux within 4.500000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_instFlux** (units=ct,type=float64): instFlux within 6.000000-pixel aperture

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_flag** (units=None,type=bool): General Failure Flag

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**undeblended_ext_convolved_ConvolvedFlux_3_kron_instFlux** (units=ct,type=float64): convolved Kron flux: seeing 8.000000

**undeblended_ext_convolved_ConvolvedFlux_3_kron_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**undeblended_ext_convolved_ConvolvedFlux_3_kron_flag** (units=None,type=bool): convolved Kron flux failed: seeing 8.000000

**undeblended_ext_convolved_ConvolvedFlux_flag** (units=None,type=bool): error in running ConvolvedFluxPlugin

**base_GaussianFlux_apCorr** (units=None,type=float64): aperture correction applied to base_GaussianFlux

**base_GaussianFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_GaussianFlux

**base_GaussianFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_GaussianFlux

**base_PsfFlux_apCorr** (units=None,type=float64): aperture correction applied to base_PsfFlux

**slot_PsfFlux_apCorr** (units=None,type=float64): aperture correction applied to base_PsfFlux

**base_PsfFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_PsfFlux

**slot_PsfFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_PsfFlux

**base_PsfFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_PsfFlux

**slot_PsfFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_PsfFlux

**ext_convolved_ConvolvedFlux_0_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_3_3

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_3_3

**ext_convolved_ConvolvedFlux_0_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_3_3

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_3_3

**ext_convolved_ConvolvedFlux_0_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_0_3_3

**ext_convolved_ConvolvedFlux_0_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_4_5

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_4_5

**ext_convolved_ConvolvedFlux_0_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_4_5

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_4_5

**ext_convolved_ConvolvedFlux_0_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_0_4_5

**ext_convolved_ConvolvedFlux_0_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_6_0

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_6_0

**ext_convolved_ConvolvedFlux_0_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_6_0

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_6_0

**ext_convolved_ConvolvedFlux_0_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_0_6_0

**ext_convolved_ConvolvedFlux_0_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_kron

**undeblended_ext_convolved_ConvolvedFlux_0_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_0_kron

**ext_convolved_ConvolvedFlux_0_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_kron

**undeblended_ext_convolved_ConvolvedFlux_0_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_0_kron

**ext_convolved_ConvolvedFlux_0_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_0_kron

**ext_convolved_ConvolvedFlux_1_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_3_3

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_3_3

**ext_convolved_ConvolvedFlux_1_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_3_3

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_3_3

**ext_convolved_ConvolvedFlux_1_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_1_3_3

**ext_convolved_ConvolvedFlux_1_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_4_5

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_4_5

**ext_convolved_ConvolvedFlux_1_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_4_5

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_4_5

**ext_convolved_ConvolvedFlux_1_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_1_4_5

**ext_convolved_ConvolvedFlux_1_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_6_0

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_6_0

**ext_convolved_ConvolvedFlux_1_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_6_0

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_6_0

**ext_convolved_ConvolvedFlux_1_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_1_6_0

**ext_convolved_ConvolvedFlux_1_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_kron

**undeblended_ext_convolved_ConvolvedFlux_1_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_1_kron

**ext_convolved_ConvolvedFlux_1_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_kron

**undeblended_ext_convolved_ConvolvedFlux_1_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_1_kron

**ext_convolved_ConvolvedFlux_1_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_1_kron

**ext_convolved_ConvolvedFlux_2_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_3_3

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_3_3

**ext_convolved_ConvolvedFlux_2_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_3_3

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_3_3

**ext_convolved_ConvolvedFlux_2_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_2_3_3

**ext_convolved_ConvolvedFlux_2_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_4_5

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_4_5

**ext_convolved_ConvolvedFlux_2_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_4_5

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_4_5

**ext_convolved_ConvolvedFlux_2_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_2_4_5

**ext_convolved_ConvolvedFlux_2_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_6_0

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_6_0

**ext_convolved_ConvolvedFlux_2_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_6_0

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_6_0

**ext_convolved_ConvolvedFlux_2_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_2_6_0

**ext_convolved_ConvolvedFlux_2_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_kron

**undeblended_ext_convolved_ConvolvedFlux_2_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_2_kron

**ext_convolved_ConvolvedFlux_2_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_kron

**undeblended_ext_convolved_ConvolvedFlux_2_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_2_kron

**ext_convolved_ConvolvedFlux_2_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_2_kron

**ext_convolved_ConvolvedFlux_3_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_3_3

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_3_3

**ext_convolved_ConvolvedFlux_3_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_3_3

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_3_3

**ext_convolved_ConvolvedFlux_3_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_3_3_3

**ext_convolved_ConvolvedFlux_3_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_4_5

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_4_5

**ext_convolved_ConvolvedFlux_3_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_4_5

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_4_5

**ext_convolved_ConvolvedFlux_3_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_3_4_5

**ext_convolved_ConvolvedFlux_3_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_6_0

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_6_0

**ext_convolved_ConvolvedFlux_3_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_6_0

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_6_0

**ext_convolved_ConvolvedFlux_3_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_3_6_0

**ext_convolved_ConvolvedFlux_3_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_kron

**undeblended_ext_convolved_ConvolvedFlux_3_kron_apCorr** (units=None,type=float64): aperture correction applied to ext_convolved_ConvolvedFlux_3_kron

**ext_convolved_ConvolvedFlux_3_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_kron

**undeblended_ext_convolved_ConvolvedFlux_3_kron_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_convolved_ConvolvedFlux_3_kron

**ext_convolved_ConvolvedFlux_3_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_convolved_ConvolvedFlux_3_kron

**ext_photometryKron_KronFlux_apCorr** (units=None,type=float64): aperture correction applied to ext_photometryKron_KronFlux

**ext_photometryKron_KronFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_photometryKron_KronFlux

**ext_photometryKron_KronFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_photometryKron_KronFlux

**modelfit_CModel_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel

**slot_ModelFlux_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel

**modelfit_CModel_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel

**slot_ModelFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel

**modelfit_CModel_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel

**slot_ModelFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel

**modelfit_CModel_dev_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel_dev

**slot_ModelFlux_dev_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel_dev

**modelfit_CModel_dev_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel_dev

**slot_ModelFlux_dev_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel_dev

**modelfit_CModel_dev_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel_dev

**slot_ModelFlux_dev_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel_dev

**modelfit_CModel_exp_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel_exp

**slot_ModelFlux_exp_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel_exp

**modelfit_CModel_exp_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel_exp

**slot_ModelFlux_exp_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel_exp

**modelfit_CModel_exp_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel_exp

**slot_ModelFlux_exp_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel_exp

**modelfit_CModel_initial_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel_initial

**slot_ModelFlux_initial_apCorr** (units=None,type=float64): aperture correction applied to modelfit_CModel_initial

**modelfit_CModel_initial_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel_initial

**slot_ModelFlux_initial_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to modelfit_CModel_initial

**modelfit_CModel_initial_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel_initial

**slot_ModelFlux_initial_flag_apCorr** (units=None,type=bool): set if unable to aperture correct modelfit_CModel_initial

**undeblended_ext_convolved_ConvolvedFlux_0_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_0_3_3

**undeblended_ext_convolved_ConvolvedFlux_0_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_0_4_5

**undeblended_ext_convolved_ConvolvedFlux_0_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_0_6_0

**undeblended_ext_convolved_ConvolvedFlux_1_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_1_3_3

**undeblended_ext_convolved_ConvolvedFlux_1_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_1_4_5

**undeblended_ext_convolved_ConvolvedFlux_1_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_1_6_0

**undeblended_ext_convolved_ConvolvedFlux_2_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_2_3_3

**undeblended_ext_convolved_ConvolvedFlux_2_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_2_4_5

**undeblended_ext_convolved_ConvolvedFlux_2_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_2_6_0

**undeblended_ext_convolved_ConvolvedFlux_3_3_3_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_3_3_3

**undeblended_ext_convolved_ConvolvedFlux_3_4_5_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_3_4_5

**undeblended_ext_convolved_ConvolvedFlux_3_6_0_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_3_6_0

**undeblended_ext_convolved_ConvolvedFlux_0_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_0_kron

**undeblended_ext_convolved_ConvolvedFlux_1_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_1_kron

**undeblended_ext_convolved_ConvolvedFlux_2_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_2_kron

**undeblended_ext_convolved_ConvolvedFlux_3_kron_flag_apCorr** (units=None,type=bool): set if unable to aperture correct undeblended_ext_convolved_ConvolvedFlux_3_kron

**base_ClassificationExtendedness_value** (units=None,type=float64): Set to 1 for extended sources, 0 for point sources.

**base_ClassificationExtendedness_flag** (units=None,type=bool): Set to 1 for any fatal failure.
