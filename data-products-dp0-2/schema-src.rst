.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-2-schema-src:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

.. This file will not be included in a toctree because it is a reference page.
.. The ``orphan`` metadata field is used to suppress the "WARNING: document isn't included in any toctree."

:orphan:

#############################
Schema for Butler catalog src
#############################

.. This section should provide a brief, top-level description of the page.

This page is a reference to schema for source detections in a single processed visit image (PVI; also called a calexp).
Other schemas are listed under :ref:`DP0-2-Data-Products-DPDD-Catalogs`.

**id** (units=None,type=int64): unique ID

**coord_ra** (units=rad,type=float64): position in ra/dec

**coord_dec** (units=rad,type=float64): position in ra/dec

**parent** (units=None,type=int64): unique ID of parent source

**calib_detected** (units=None,type=bool): Source was detected as an icSource

**calib_psf_candidate** (units=None,type=bool): Flag set if the source was a candidate for PSF determination, as determined by the star selector.

**calib_psf_used** (units=None,type=bool): Flag set if the source was actually used for PSF determination, as determined by the

**calib_psf_reserved** (units=None,type=bool): set if source was reserved from PSF determination

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

**base_NaiveCentroid_x** (units=pix,type=float64): centroid from Naive Centroid algorithm

**base_NaiveCentroid_y** (units=pix,type=float64): centroid from Naive Centroid algorithm

**base_NaiveCentroid_flag** (units=None,type=bool): General Failure Flag

**base_NaiveCentroid_flag_noCounts** (units=None,type=bool): Object to be centroided has no counts

**base_NaiveCentroid_flag_edge** (units=None,type=bool): Object too close to edge

**base_NaiveCentroid_flag_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_SdssCentroid_x** (units=pix,type=float64): centroid from Sdss Centroid algorithm

**slot_Centroid_x** (units=pix,type=float64): centroid from Sdss Centroid algorithm

**base_SdssCentroid_y** (units=pix,type=float64): centroid from Sdss Centroid algorithm

**slot_Centroid_y** (units=pix,type=float64): centroid from Sdss Centroid algorithm

**base_SdssCentroid_xErr** (units=pix,type=float32): 1-sigma uncertainty on x position

**slot_Centroid_xErr** (units=pix,type=float32): 1-sigma uncertainty on x position

**base_SdssCentroid_yErr** (units=pix,type=float32): 1-sigma uncertainty on y position

**slot_Centroid_yErr** (units=pix,type=float32): 1-sigma uncertainty on y position

**base_SdssCentroid_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_flag_badCentroid** (units=None,type=bool): General Failure Flag

**base_GaussianFlux_flag_badCentroid** (units=None,type=bool): General Failure Flag

**base_LocalBackground_flag_badCentroid** (units=None,type=bool): General Failure Flag

**base_NaiveCentroid_flag_badInitialCentroid** (units=None,type=bool): General Failure Flag

**base_PsfFlux_flag_badCentroid** (units=None,type=bool): General Failure Flag

**base_SdssShape_flag_badCentroid** (units=None,type=bool): General Failure Flag

**base_Variance_flag_badCentroid** (units=None,type=bool): General Failure Flag

**ext_photometryKron_KronFlux_flag_badInitialCentroid** (units=None,type=bool): General Failure Flag

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid** (units=None,type=bool): General Failure Flag

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid** (units=None,type=bool): General Failure Flag

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid** (units=None,type=bool): General Failure Flag

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid** (units=None,type=bool): General Failure Flag

**slot_Centroid_flag** (units=None,type=bool): General Failure Flag

**base_SdssCentroid_flag_edge** (units=None,type=bool): Object too close to edge

**base_CircularApertureFlux_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**base_GaussianFlux_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**base_LocalBackground_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**base_NaiveCentroid_flag_badInitialCentroid_edge** (units=None,type=bool): Object too close to edge

**base_PsfFlux_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**base_SdssShape_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**base_Variance_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**ext_photometryKron_KronFlux_flag_badInitialCentroid_edge** (units=None,type=bool): Object too close to edge

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid_edge** (units=None,type=bool): Object too close to edge

**slot_Centroid_flag_edge** (units=None,type=bool): Object too close to edge

**base_SdssCentroid_flag_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_CircularApertureFlux_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_GaussianFlux_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_LocalBackground_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_NaiveCentroid_flag_badInitialCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_PsfFlux_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_SdssShape_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_Variance_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**ext_photometryKron_KronFlux_flag_badInitialCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**slot_Centroid_flag_noSecondDerivative** (units=None,type=bool): Vanishing second derivative

**base_SdssCentroid_flag_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_CircularApertureFlux_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_GaussianFlux_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_LocalBackground_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_NaiveCentroid_flag_badInitialCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_PsfFlux_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_SdssShape_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_Variance_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**ext_photometryKron_KronFlux_flag_badInitialCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**slot_Centroid_flag_almostNoSecondDerivative** (units=None,type=bool): Almost vanishing second derivative

**base_SdssCentroid_flag_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_CircularApertureFlux_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_GaussianFlux_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_LocalBackground_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_NaiveCentroid_flag_badInitialCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_PsfFlux_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_SdssShape_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_Variance_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**ext_photometryKron_KronFlux_flag_badInitialCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**slot_Centroid_flag_notAtMaximum** (units=None,type=bool): Object is not at a maximum

**base_SdssCentroid_flag_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_CircularApertureFlux_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_GaussianFlux_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_LocalBackground_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_NaiveCentroid_flag_badInitialCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_PsfFlux_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_SdssShape_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_Variance_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**ext_photometryKron_KronFlux_flag_badInitialCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**slot_Centroid_flag_resetToPeak** (units=None,type=bool): set if CentroidChecker reset the centroid

**base_SdssCentroid_flag_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_CircularApertureFlux_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_GaussianFlux_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_LocalBackground_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_NaiveCentroid_flag_badInitialCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_PsfFlux_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_SdssShape_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_Variance_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**ext_photometryKron_KronFlux_flag_badInitialCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**ext_shapeHSM_HsmPsfMoments_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**ext_shapeHSM_HsmShapeRegauss_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**ext_shapeHSM_HsmSourceMomentsRound_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**ext_shapeHSM_HsmSourceMoments_flag_badCentroid_badError** (units=None,type=bool): Error on x and/or y position is NaN

**slot_Centroid_flag_badError** (units=None,type=bool): Error on x and/or y position is NaN

**base_Blendedness_old** (units=None,type=float64): Blendedness from dot products: (child.dot(parent)/child.dot(child) - 1)

**base_Blendedness_raw** (units=None,type=float64): Measure of how much the flux is affected by neighbors: (1 - child_instFlux/parent_instFlux).  Operates on the "raw" pixel values.

**base_Blendedness_raw_child_instFlux** (units=ct,type=float64): Instrumental flux of the child, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_parent_instFlux** (units=ct,type=float64): Instrumental flux of the parent, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_abs** (units=None,type=float64): Measure of how much the flux is affected by neighbors: (1 - child_instFlux/parent_instFlux).  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_child_instFlux** (units=ct,type=float64): Instrumental flux of the child, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_parent_instFlux** (units=ct,type=float64): Instrumental flux of the parent, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_raw_child_xx** (units=pix2,type=float64): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_child_yy** (units=pix2,type=float64): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_child_xy** (units=pix2,type=float64): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_parent_xx** (units=pix2,type=float64): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_parent_yy** (units=pix2,type=float64): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_raw_parent_xy** (units=pix2,type=float64): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the "raw" pixel values.

**base_Blendedness_abs_child_xx** (units=pix2,type=float64): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_child_yy** (units=pix2,type=float64): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_child_xy** (units=pix2,type=float64): Shape of the child, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_parent_xx** (units=pix2,type=float64): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_parent_yy** (units=pix2,type=float64): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_abs_parent_xy** (units=pix2,type=float64): Shape of the parent, measured with a Gaussian weight matched to the child.  Operates on the absolute value of the pixels to try to obtain a "de-noised" value.  See section 4.9.11 of Bosch et al. 2018, PASJ, 70, S5 for details.

**base_Blendedness_flag** (units=None,type=bool): General Failure Flag

**base_Blendedness_flag_noCentroid** (units=None,type=bool): Object has no centroid

**base_Blendedness_flag_noShape** (units=None,type=bool): Object has no shape

**base_FPPosition_x** (units=mm,type=float64): Position on the focal plane

**base_FPPosition_y** (units=mm,type=float64): Position on the focal plane

**base_FPPosition_flag** (units=None,type=bool): Set to True for any fatal failure

**base_FPPosition_missingDetector_flag** (units=None,type=bool): Set to True if detector object is missing

**base_Jacobian_value** (units=None,type=float64): Jacobian correction

**base_Jacobian_flag** (units=None,type=bool): Set to 1 for any fatal failure

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

**base_SdssShape_psf_yy** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**base_SdssShape_psf_xy** (units=pix2,type=float64): adaptive moments of the PSF model at the object position

**base_SdssShape_instFlux_xx_Cov** (units=ct pix2,type=float32): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xx

**base_SdssShape_instFlux_yy_Cov** (units=ct pix2,type=float32): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_yy

**base_SdssShape_instFlux_xy_Cov** (units=ct pix2,type=float32): uncertainty covariance between base_SdssShape_instFlux and base_SdssShape_xy

**base_SdssShape_flag** (units=None,type=bool): General Failure Flag

**base_SdssShape_flag_unweightedBad** (units=None,type=bool): Both weighted and unweighted moments were invalid

**base_SdssShape_flag_unweighted** (units=None,type=bool): Weighted moments converged to an invalid value; using unweighted moments

**base_SdssShape_flag_shift** (units=None,type=bool): centroid shifted by more than the maximum allowed amount

**base_SdssShape_flag_maxIter** (units=None,type=bool): Too many iterations in adaptive moments

**base_SdssShape_flag_psf** (units=None,type=bool): Failure in measuring PSF model shape

**ext_shapeHSM_HsmPsfMoments_x** (units=pix,type=float64): HSM Centroid

**slot_PsfShape_x** (units=pix,type=float64): HSM Centroid

**ext_shapeHSM_HsmPsfMoments_y** (units=pix,type=float64): HSM Centroid

**slot_PsfShape_y** (units=pix,type=float64): HSM Centroid

**ext_shapeHSM_HsmPsfMoments_xx** (units=pix2,type=float64): HSM moments

**slot_PsfShape_xx** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmPsfMoments_yy** (units=pix2,type=float64): HSM moments

**slot_PsfShape_yy** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmPsfMoments_xy** (units=pix2,type=float64): HSM moments

**slot_PsfShape_xy** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmPsfMoments_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**slot_PsfShape_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmPsfMoments_flag_no_pixels** (units=None,type=bool): no pixels to measure

**slot_PsfShape_flag_no_pixels** (units=None,type=bool): no pixels to measure

**ext_shapeHSM_HsmPsfMoments_flag_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**slot_PsfShape_flag_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**ext_shapeHSM_HsmPsfMoments_flag_parent_source** (units=None,type=bool): parent source, ignored

**slot_PsfShape_flag_parent_source** (units=None,type=bool): parent source, ignored

**ext_shapeHSM_HsmShapeRegauss_e1** (units=None,type=float64): PSF-corrected shear using Hirata & Seljak (2003) ''regaussianization

**ext_shapeHSM_HsmShapeRegauss_e2** (units=None,type=float64): PSF-corrected shear using Hirata & Seljak (2003) ''regaussianization

**ext_shapeHSM_HsmShapeRegauss_sigma** (units=None,type=float64): PSF-corrected shear using Hirata & Seljak (2003) ''regaussianization

**ext_shapeHSM_HsmShapeRegauss_resolution** (units=None,type=float64): resolution factor (0=unresolved, 1=resolved)

**ext_shapeHSM_HsmShapeRegauss_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmShapeRegauss_flag_no_pixels** (units=None,type=bool): no pixels to measure

**ext_shapeHSM_HsmShapeRegauss_flag_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**ext_shapeHSM_HsmShapeRegauss_flag_parent_source** (units=None,type=bool): parent source, ignored

**ext_shapeHSM_HsmShapeRegauss_flag_galsim** (units=None,type=bool): GalSim failure

**ext_shapeHSM_HsmSourceMoments_x** (units=pix,type=float64): HSM Centroid

**slot_Shape_x** (units=pix,type=float64): HSM Centroid

**ext_shapeHSM_HsmSourceMoments_y** (units=pix,type=float64): HSM Centroid

**slot_Shape_y** (units=pix,type=float64): HSM Centroid

**ext_shapeHSM_HsmSourceMoments_xx** (units=pix2,type=float64): HSM moments

**slot_Shape_xx** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmSourceMoments_yy** (units=pix2,type=float64): HSM moments

**slot_Shape_yy** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmSourceMoments_xy** (units=pix2,type=float64): HSM moments

**slot_Shape_xy** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmSourceMoments_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**base_GaussianFlux_flag_badShape** (units=None,type=bool): general failure flag, set if anything went wrong

**slot_Shape_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmSourceMoments_flag_no_pixels** (units=None,type=bool): no pixels to measure

**base_GaussianFlux_flag_badShape_no_pixels** (units=None,type=bool): no pixels to measure

**slot_Shape_flag_no_pixels** (units=None,type=bool): no pixels to measure

**ext_shapeHSM_HsmSourceMoments_flag_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**base_GaussianFlux_flag_badShape_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**slot_Shape_flag_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**ext_shapeHSM_HsmSourceMoments_flag_parent_source** (units=None,type=bool): parent source, ignored

**base_GaussianFlux_flag_badShape_parent_source** (units=None,type=bool): parent source, ignored

**slot_Shape_flag_parent_source** (units=None,type=bool): parent source, ignored

**ext_shapeHSM_HsmSourceMomentsRound_x** (units=pix,type=float64): HSM Centroid

**slot_ShapeRound_x** (units=pix,type=float64): HSM Centroid

**ext_shapeHSM_HsmSourceMomentsRound_y** (units=pix,type=float64): HSM Centroid

**slot_ShapeRound_y** (units=pix,type=float64): HSM Centroid

**ext_shapeHSM_HsmSourceMomentsRound_xx** (units=pix2,type=float64): HSM moments

**slot_ShapeRound_xx** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmSourceMomentsRound_yy** (units=pix2,type=float64): HSM moments

**slot_ShapeRound_yy** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmSourceMomentsRound_xy** (units=pix2,type=float64): HSM moments

**slot_ShapeRound_xy** (units=pix2,type=float64): HSM moments

**ext_shapeHSM_HsmSourceMomentsRound_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**slot_ShapeRound_flag** (units=None,type=bool): general failure flag, set if anything went wrong

**ext_shapeHSM_HsmSourceMomentsRound_flag_no_pixels** (units=None,type=bool): no pixels to measure

**slot_ShapeRound_flag_no_pixels** (units=None,type=bool): no pixels to measure

**ext_shapeHSM_HsmSourceMomentsRound_flag_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**slot_ShapeRound_flag_not_contained** (units=None,type=bool): center not contained in footprint bounding box

**ext_shapeHSM_HsmSourceMomentsRound_flag_parent_source** (units=None,type=bool): parent source, ignored

**slot_ShapeRound_flag_parent_source** (units=None,type=bool): parent source, ignored

**ext_shapeHSM_HsmSourceMomentsRound_Flux** (units=None,type=float32): HSM flux

**slot_ShapeRound_Flux** (units=None,type=float32): HSM flux

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

**slot_ApFlux_instFlux** (units=ct,type=float64): instFlux within 12.000000-pixel aperture

**slot_CalibFlux_instFlux** (units=ct,type=float64): instFlux within 12.000000-pixel aperture

**base_CircularApertureFlux_12_0_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**slot_ApFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**slot_CalibFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_CircularApertureFlux_12_0_flag** (units=None,type=bool): General Failure Flag

**slot_ApFlux_flag** (units=None,type=bool): General Failure Flag

**slot_CalibFlux_flag** (units=None,type=bool): General Failure Flag

**base_CircularApertureFlux_12_0_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**slot_ApFlux_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**slot_CalibFlux_flag_apertureTruncated** (units=None,type=bool): aperture did not fit within measurement image

**base_CircularApertureFlux_12_0_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**slot_ApFlux_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

**slot_CalibFlux_flag_sincCoeffsTruncated** (units=None,type=bool): full sinc coefficient image did not fit within measurement image

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

**slot_GaussianFlux_instFlux** (units=ct,type=float64): instFlux from Gaussian Flux algorithm

**slot_ModelFlux_instFlux** (units=ct,type=float64): instFlux from Gaussian Flux algorithm

**base_GaussianFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**slot_GaussianFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**slot_ModelFlux_instFluxErr** (units=ct,type=float64): 1-sigma instFlux uncertainty

**base_GaussianFlux_flag** (units=None,type=bool): General Failure Flag

**slot_GaussianFlux_flag** (units=None,type=bool): General Failure Flag

**slot_ModelFlux_flag** (units=None,type=bool): General Failure Flag

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

**base_GaussianFlux_apCorr** (units=None,type=float64): aperture correction applied to base_GaussianFlux

**slot_GaussianFlux_apCorr** (units=None,type=float64): aperture correction applied to base_GaussianFlux

**slot_ModelFlux_apCorr** (units=None,type=float64): aperture correction applied to base_GaussianFlux

**base_GaussianFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_GaussianFlux

**slot_GaussianFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_GaussianFlux

**slot_ModelFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_GaussianFlux

**base_GaussianFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_GaussianFlux

**slot_GaussianFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_GaussianFlux

**slot_ModelFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_GaussianFlux

**base_PsfFlux_apCorr** (units=None,type=float64): aperture correction applied to base_PsfFlux

**slot_PsfFlux_apCorr** (units=None,type=float64): aperture correction applied to base_PsfFlux

**base_PsfFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_PsfFlux

**slot_PsfFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to base_PsfFlux

**base_PsfFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_PsfFlux

**slot_PsfFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct base_PsfFlux

**ext_photometryKron_KronFlux_apCorr** (units=None,type=float64): aperture correction applied to ext_photometryKron_KronFlux

**ext_photometryKron_KronFlux_apCorrErr** (units=None,type=float64): standard deviation of aperture correction applied to ext_photometryKron_KronFlux

**ext_photometryKron_KronFlux_flag_apCorr** (units=None,type=bool): set if unable to aperture correct ext_photometryKron_KronFlux

**base_ClassificationExtendedness_value** (units=None,type=float64): Set to 1 for extended sources, 0 for point sources.

**base_ClassificationExtendedness_flag** (units=None,type=bool): Set to 1 for any fatal failure.

**base_FootprintArea_value** (units=pix,type=int32): Number of pixels in the source''s detection footprint.

**calib_astrometry_used** (units=None,type=bool): set if source was used in astrometric calibration

**calib_photometry_used** (units=None,type=bool): set if source was used in photometric calibration

**calib_photometry_reserved** (units=None,type=bool): set if source was reserved from photometric calibration

**base_localPhotoCalib** (units=None,type=float64): Local approximation of the PhotoCalib calibration factor at the location of the src.

**base_localPhotoCalibErr** (units=None,type=float64): Error on the local approximation of the PhotoCalib calibration factor at the location of the src.

**base_CDMatrix_1_1** (units=None,type=float64): (1, 1) element of the CDMatrix for the linear approximation of the WCS at the src location.

**base_CDMatrix_1_2** (units=None,type=float64): (1, 2) element of the CDMatrix for the linear approximation of the WCS at the src location.

**base_CDMatrix_2_1** (units=None,type=float64): (2, 1) element of the CDMatrix for the linear approximation of the WCS at the src location.

**base_CDMatrix_2_2** (units=None,type=float64): (2, 2) element of the CDMatrix for the linear approximation of the WCS at the src location.
