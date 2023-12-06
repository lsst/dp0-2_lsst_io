#################################################################
Full Output of Custom Coadd Source Detection pipetask run Command
#################################################################

.. code-block::

    $ pipetask --long-log --log-file $LOGFILE run \
    > -b dp02 \
    > -i u/$USER/custom_coadd_window1_cl00 \
    > -o u/$USER/custom_coadd_window1_cl00_det \
    > -c detection:detection.thresholdValue=10 \
    > -c detection:detection.thresholdType="stdev" \
    > -c deblend:multibandDeblend.maxIter=20 \
    > -c measure:doPropagateFlags=False \
    > -p $DRP_PIPE_DIR/pipelines/LSSTCam-imSim/DRP-test-med-1.yaml#detection,mergeDetections,deblend,measure \
    > -d "tract = 4431 AND patch = 17 AND band = 'i' AND skymap = 'DC2'"
    INFO 2023-10-19T05:59:02.685+00:00 lsst.ctrl.mpexec.cmdLineFwk ()(cmdLineFwk.py:581) - QuantumGraph contains 4 quanta for 4 tasks, graph ID: '1697695142.6832964-3058'
    INFO 2023-10-19T05:59:28.636+00:00 lsst.detection.scaleVariance (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(scaleVariance.py:130) - Renormalizing variance by 1.004598
    INFO 2023-10-19T05:59:28.673+00:00 lsst.detection.detection (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:925) - Applying temporary wide background subtraction
    INFO 2023-10-19T05:59:32.147+00:00 lsst.detection.detection (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 4778 positive peaks in 3570 footprints to 5 sigma
    INFO 2023-10-19T05:59:33.105+00:00 lsst.detection.detection.skyObjects (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(skyObjects.py:125) - Added 1000 of 1000 requested sky sources (100%)
    INFO 2023-10-19T05:59:33.136+00:00 lsst.detection.detection.skyMeasurement (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(forcedMeasurement.py:342) - Performing forced measurement on 1000 sources
    INFO 2023-10-19T05:59:42.004+00:00 lsst.detection.detection (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(dynamicDetection.py:220) - Modifying configured detection threshold by factor 0.767935 to 7.679347
    INFO 2023-10-19T05:59:44.489+00:00 lsst.detection.detection (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 2934 positive peaks in 2569 footprints to 7.67935 sigma
    INFO 2023-10-19T05:59:46.407+00:00 lsst.detection.detection (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 3393 positive peaks in 2678 footprints to 7.67935 sigma
    INFO 2023-10-19T05:59:47.122+00:00 lsst.detection.detection.skyObjects (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(skyObjects.py:125) - Added 1000 of 1000 requested sky sources (100%)
    INFO 2023-10-19T05:59:47.154+00:00 lsst.detection.detection.skyMeasurement (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(forcedMeasurement.py:342) - Performing forced measurement on 1000 sources
    INFO 2023-10-19T05:59:55.923+00:00 lsst.detection.detection (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(dynamicDetection.py:280) - Tweaking background by -0.004311 to match sky photometry
    INFO 2023-10-19T06:00:01.727+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (detection:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(singleQuantumExecutor.py:232) - Execution of task 'detection' on quantum {band: 'i', skymap: 'DC2', tract: 4431, patch: 17} took 36.198 seconds
    INFO 2023-10-19T06:00:01.745+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-10-19T06:00:02.358+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 1 quanta successfully, 0 failed and 3 remain out of total 4 quanta.
    INFO 2023-10-19T06:00:08.147+00:00 lsst.mergeDetections.skyObjects (mergeDetections:{skymap: 'DC2', tract: 4431, patch: 17})(skyObjects.py:125) - Added 100 of 100 requested sky sources (100%)
    INFO 2023-10-19T06:00:08.163+00:00 lsst.mergeDetections (mergeDetections:{skymap: 'DC2', tract: 4431, patch: 17})(mergeDetections.py:331) - Merged to 2669 sources
    INFO 2023-10-19T06:00:08.211+00:00 lsst.mergeDetections (mergeDetections:{skymap: 'DC2', tract: 4431, patch: 17})(mergeDetections.py:364) - Culled 0 of 3034 peaks
    INFO 2023-10-19T06:00:08.866+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (mergeDetections:{skymap: 'DC2', tract: 4431, patch: 17})(singleQuantumExecutor.py:232) - Execution of task 'mergeDetections' on quantum {skymap: 'DC2', tract: 4431, patch: 17} took 6.508 seconds
    INFO 2023-10-19T06:00:08.882+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-10-19T06:00:09.470+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 2 quanta successfully, 0 failed and 2 remain out of total 4 quanta.
    INFO 2023-10-19T06:00:11.215+00:00 lsst.deblend.multibandDeblend (deblend:{skymap: 'DC2', tract: 4431, patch: 17})(scarletDeblendTask.py:973) - Deblending 2669 sources in 1 exposure bands
    WARNING 2023-10-19T06:00:11.291+00:00 py.warnings (deblend:{skymap: 'DC2', tract: 4431, patch: 17})(warnings.py:109) - /opt/lsst/software/stack/stack/miniconda3-py38_4.9.2-4.1.0/Linux64/scarlet/gd32b658ba2+4083830bf8/lib/python/scarlet/lite/models.py:119: RuntimeWarning: invalid value encountered in true_divide
      if np.any(edge_flux/edge_mask > self.bg_thresh*self.bg_rms[:, None, None]):
    
    WARNING 2023-10-19T06:01:32.574+00:00 py.warnings (deblend:{skymap: 'DC2', tract: 4431, patch: 17})(warnings.py:109) - /opt/lsst/software/stack/stack/miniconda3-py38_4.9.2-4.1.0/Linux64/scarlet/gd32b658ba2+4083830bf8/lib/python/scarlet/lite/measure.py:35: RuntimeWarning: invalid value encountered in multiply
      denominator = (psfs * noise) * psfs
    
    WARNING 2023-10-19T06:01:32.856+00:00 py.warnings (deblend:{skymap: 'DC2', tract: 4431, patch: 17})(warnings.py:109) - /opt/lsst/software/stack/stack/miniconda3-py38_4.9.2-4.1.0/Linux64/scarlet/gd32b658ba2+4083830bf8/lib/python/scarlet/lite/parameters.py:302: RuntimeWarning: invalid value encountered in true_divide
      _z = self.prox(z - gamma/step * psi * (z-self.x), gamma)
    
    WARNING 2023-10-19T06:01:32.857+00:00 py.warnings (deblend:{skymap: 'DC2', tract: 4431, patch: 17})(warnings.py:109) - /opt/lsst/software/stack/stack/miniconda3-py38_4.9.2-4.1.0/Linux64/scarlet/gd32b658ba2+4083830bf8/lib/python/scarlet/lite/parameters.py:302: RuntimeWarning: invalid value encountered in subtract
      _z = self.prox(z - gamma/step * psi * (z-self.x), gamma)
    
    INFO 2023-10-19T06:01:55.535+00:00 lsst.deblend.multibandDeblend (deblend:{skymap: 'DC2', tract: 4431, patch: 17})(scarletDeblendTask.py:1135) - Deblender results: of 2669 parent sources, 2569 were deblended, creating 2934 children, for a total of 5603 sources
    INFO 2023-10-19T06:01:58.922+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (deblend:{skymap: 'DC2', tract: 4431, patch: 17})(singleQuantumExecutor.py:232) - Execution of task 'deblend' on quantum {skymap: 'DC2', tract: 4431, patch: 17} took 109.451 seconds
    INFO 2023-10-19T06:01:58.939+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-10-19T06:01:59.576+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 3 quanta successfully, 0 failed and 1 remain out of total 4 quanta.
    WARNING 2023-10-19T06:02:03.394+00:00 py.warnings (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(warnings.py:109) - /opt/lsst/software/stack/stack/miniconda3-py38_4.9.2-4.1.0/Linux64/scarlet/gd32b658ba2+4083830bf8/lib/python/scarlet/lite/measure.py:85: RuntimeWarning: divide by zero encountered in true_divide
      ratio = numerator / denominator
    
    WARNING 2023-10-19T06:02:03.395+00:00 py.warnings (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(warnings.py:109) - /opt/lsst/software/stack/stack/miniconda3-py38_4.9.2-4.1.0/Linux64/scarlet/gd32b658ba2+4083830bf8/lib/python/scarlet/lite/measure.py:85: RuntimeWarning: invalid value encountered in true_divide
      ratio = numerator / denominator
    
    INFO 2023-10-19T06:03:07.911+00:00 lsst.measure.measurement (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(sfm.py:298) - Measuring 5603 sources (2669 parents, 2934 children) 
    INFO 2023-10-19T06:10:04.751+00:00 lsst.measure.applyApCorr (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(applyApCorr.py:244) - Applying aperture corrections to 23 instFlux fields
    INFO 2023-10-19T06:10:33.883+00:00 lsst.measure.match.sourceSelection (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(sourceSelector.py:560) - Selected 5603/5603 sources
    INFO 2023-10-19T06:10:33.885+00:00 lsst.measure (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(loadReferenceObjects.py:913) - Loading reference objects from cal_ref_cat_2_2 in region bounded by [55.46032473, 55.85329048], [-32.37103199, -32.03852616] RA Dec
    INFO 2023-10-19T06:10:34.173+00:00 lsst.measure (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(loadReferenceObjects.py:953) - Loaded 2514 reference objects
    INFO 2023-10-19T06:10:34.180+00:00 lsst.measure.match.referenceSelection (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(sourceSelector.py:626) - Selected 2514/2514 references
    INFO 2023-10-19T06:10:34.185+00:00 lsst.measure.match (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(directMatch.py:111) - Matched 1523 from 5603/5603 input and 2514/2514 reference sources
    INFO 2023-10-19T06:10:36.769+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (measure:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(singleQuantumExecutor.py:232) - Execution of task 'measure' on quantum {band: 'i', skymap: 'DC2', tract: 4431, patch: 17} took 517.192 seconds
    INFO 2023-10-19T06:10:36.789+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-10-19T06:10:37.451+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 4 quanta successfully, 0 failed and 0 remain out of total 4 quanta.
