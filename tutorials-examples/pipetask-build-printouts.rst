.. code-block::

    $ pipetask build -p $DRP_PIPE_DIR/pipelines/LSSTCam-imSim/DRP-test-med-1.yaml#makeWarp,assembleCoadd --show pipeline
    description: DRP specialized for the ImSim-DC2 test-med-1 dataset
    instrument: lsst.obs.lsst.LsstCamImSim
    parameters:
      band: i
      model: cModelFlux
    tasks:
      makeWarp:
        class: lsst.pipe.tasks.makeWarp.MakeWarpTask
        config:
        - makePsfMatched: true
      assembleCoadd:
        class: lsst.pipe.tasks.assembleCoadd.CompareWarpAssembleCoaddTask
        config:
        - doInputMap: true
