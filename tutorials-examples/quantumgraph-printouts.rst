.. code-block::

    $ pipetask qgraph \
    > -b dp02 \
    > -i 2.2i/runs/DP0.2 \
    > -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    > -c makeWarp:doApplyFinalizedPsf=False \
    > -c makeWarp:connections.visitSummary="visitSummary" \
    > -d "tract = 4431 AND patch = 17 AND visit in (919515,924057,924085,924086,929477,930353) AND skymap = 'DC2'" \
    > --show graph
    lsst.ctrl.mpexec.cmdLineFwk INFO: QuantumGraph contains 7 quanta for 2 tasks, graph ID: '1684058228.843482-1364'
    TaskDef(lsst.pipe.tasks.makeWarp.MakeWarpTask, label=makeWarp)
      Quantum 0:
        inputs:
          DatasetType('visitSummary', {band, instrument, physical_filter, visit_system, visit}, ExposureCatalog): [DataId({instrument: 'LSSTCam-imSim', visit: 924085, ...})]
          DatasetType('calexp.wcs', {band, instrument, detector, physical_filter, visit_system, visit}, Wcs, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 178, visit: 924085, ...})]
          DatasetType('calexp.bbox', {band, instrument, detector, physical_filter, visit_system, visit}, Box2I, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 178, visit: 924085, ...})]
          DatasetType('skyMap', {skymap}, SkyMap): [DataId({skymap: 'DC2'})]
          DatasetType('calexp', {band, instrument, detector, physical_filter, visit_system, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 178, visit: 924085, ...})]
        outputs:
          DatasetType('makeWarp_metadata', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, PropertySet): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})]
          DatasetType('deepCoadd_psfMatchedWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})]
          DatasetType('deepCoadd_directWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})]
          DatasetType('makeWarp_log', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ButlerLogRecords): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})]
      Quantum 1:
        inputs:
          DatasetType('visitSummary', {band, instrument, physical_filter, visit_system, visit}, ExposureCatalog): [DataId({instrument: 'LSSTCam-imSim', visit: 919515, ...})]
          DatasetType('calexp.wcs', {band, instrument, detector, physical_filter, visit_system, visit}, Wcs, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 110, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 113, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 116, visit: 919515, ...})]
          DatasetType('calexp.bbox', {band, instrument, detector, physical_filter, visit_system, visit}, Box2I, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 110, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 113, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 116, visit: 919515, ...})]
          DatasetType('skyMap', {skymap}, SkyMap): [DataId({skymap: 'DC2'})]
          DatasetType('calexp', {band, instrument, detector, physical_filter, visit_system, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 110, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 113, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 116, visit: 919515, ...})]
        outputs:
          DatasetType('makeWarp_metadata', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, PropertySet): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})]
          DatasetType('deepCoadd_psfMatchedWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})]
          DatasetType('deepCoadd_directWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})]
          DatasetType('makeWarp_log', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ButlerLogRecords): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})]
      Quantum 2:
        inputs:
          DatasetType('visitSummary', {band, instrument, physical_filter, visit_system, visit}, ExposureCatalog): [DataId({instrument: 'LSSTCam-imSim', visit: 929477, ...})]
          DatasetType('calexp.wcs', {band, instrument, detector, physical_filter, visit_system, visit}, Wcs, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 52, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 90, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 91, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 92, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 93, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 94, visit: 929477, ...})]
          DatasetType('calexp.bbox', {band, instrument, detector, physical_filter, visit_system, visit}, Box2I, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 52, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 90, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 91, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 92, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 93, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 94, visit: 929477, ...})]
          DatasetType('skyMap', {skymap}, SkyMap): [DataId({skymap: 'DC2'})]
          DatasetType('calexp', {band, instrument, detector, physical_filter, visit_system, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 52, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 90, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 91, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 92, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 93, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 94, visit: 929477, ...})]
        outputs:
          DatasetType('makeWarp_metadata', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, PropertySet): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})]
          DatasetType('deepCoadd_psfMatchedWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})]
          DatasetType('deepCoadd_directWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})]
          DatasetType('makeWarp_log', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ButlerLogRecords): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})]
      Quantum 3:
        inputs:
          DatasetType('visitSummary', {band, instrument, physical_filter, visit_system, visit}, ExposureCatalog): [DataId({instrument: 'LSSTCam-imSim', visit: 924086, ...})]
          DatasetType('calexp.wcs', {band, instrument, detector, physical_filter, visit_system, visit}, Wcs, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 138, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 139, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 140, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 141, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 142, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 143, visit: 924086, ...})]
          DatasetType('calexp.bbox', {band, instrument, detector, physical_filter, visit_system, visit}, Box2I, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 138, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 139, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 140, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 141, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 142, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 143, visit: 924086, ...})]
          DatasetType('skyMap', {skymap}, SkyMap): [DataId({skymap: 'DC2'})]
          DatasetType('calexp', {band, instrument, detector, physical_filter, visit_system, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 138, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 139, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 140, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 141, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 142, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 143, visit: 924086, ...})]
        outputs:
          DatasetType('makeWarp_metadata', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, PropertySet): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})]
          DatasetType('deepCoadd_psfMatchedWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})]
          DatasetType('deepCoadd_directWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})]
          DatasetType('makeWarp_log', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ButlerLogRecords): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})]
      Quantum 4:
        inputs:
          DatasetType('visitSummary', {band, instrument, physical_filter, visit_system, visit}, ExposureCatalog): [DataId({instrument: 'LSSTCam-imSim', visit: 924057, ...})]
          DatasetType('calexp.wcs', {band, instrument, detector, physical_filter, visit_system, visit}, Wcs, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 30, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 31, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 33, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 34, visit: 924057, ...})]
          DatasetType('calexp.bbox', {band, instrument, detector, physical_filter, visit_system, visit}, Box2I, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 30, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 31, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 33, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 34, visit: 924057, ...})]
          DatasetType('skyMap', {skymap}, SkyMap): [DataId({skymap: 'DC2'})]
          DatasetType('calexp', {band, instrument, detector, physical_filter, visit_system, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 30, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 31, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 33, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 34, visit: 924057, ...})]
        outputs:
          DatasetType('makeWarp_metadata', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, PropertySet): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})]
          DatasetType('deepCoadd_psfMatchedWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})]
          DatasetType('deepCoadd_directWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})]
          DatasetType('makeWarp_log', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ButlerLogRecords): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})]
      Quantum 5:
        inputs:
          DatasetType('visitSummary', {band, instrument, physical_filter, visit_system, visit}, ExposureCatalog): [DataId({instrument: 'LSSTCam-imSim', visit: 930353, ...})]
          DatasetType('calexp.wcs', {band, instrument, detector, physical_filter, visit_system, visit}, Wcs, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 165, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 166, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 168, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 169, visit: 930353, ...})]
          DatasetType('calexp.bbox', {band, instrument, detector, physical_filter, visit_system, visit}, Box2I, parentStorageClass=ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 165, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 166, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 168, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 169, visit: 930353, ...})]
          DatasetType('skyMap', {skymap}, SkyMap): [DataId({skymap: 'DC2'})]
          DatasetType('calexp', {band, instrument, detector, physical_filter, visit_system, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', detector: 165, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 166, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 168, visit: 930353, ...}), DataId({instrument: 'LSSTCam-imSim', detector: 169, visit: 930353, ...})]
        outputs:
          DatasetType('makeWarp_metadata', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, PropertySet): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})]
          DatasetType('deepCoadd_psfMatchedWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})]
          DatasetType('deepCoadd_directWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})]
          DatasetType('makeWarp_log', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ButlerLogRecords): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})]
    TaskDef(lsst.pipe.tasks.assembleCoadd.CompareWarpAssembleCoaddTask, label=assembleCoadd)
      Quantum 0:
        inputs:
          DatasetType('deepCoadd_psfMatchedWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})]
          DatasetType('skyMap', {skymap}, SkyMap): [DataId({skymap: 'DC2'})]
          DatasetType('deepCoadd_directWarp', {band, instrument, skymap, physical_filter, tract, visit_system, patch, visit}, ExposureF): [DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...}), DataId({instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})]
        outputs:
          DatasetType('deepCoadd_nImage', {band, skymap, tract, patch}, ImageU): [DataId({band: 'i', skymap: 'DC2', tract: 4431, patch: 17})]
          DatasetType('assembleCoadd_log', {band, skymap, tract, patch}, ButlerLogRecords): [DataId({band: 'i', skymap: 'DC2', tract: 4431, patch: 17})]
          DatasetType('deepCoadd', {band, skymap, tract, patch}, ExposureF): [DataId({band: 'i', skymap: 'DC2', tract: 4431, patch: 17})]
          DatasetType('deepCoadd_inputMap', {band, skymap, tract, patch}, HealSparseMap): [DataId({band: 'i', skymap: 'DC2', tract: 4431, patch: 17})]
          DatasetType('assembleCoadd_metadata', {band, skymap, tract, patch}, PropertySet): [DataId({band: 'i', skymap: 'DC2', tract: 4431, patch: 17})]
