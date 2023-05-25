.. code-block::

    $ pipetask build -p pipelines/MakeWarpAssembleCoadd.yaml#step3 --show pipeline
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
    subsets:
      step3:
        subset:
        - makeWarp
        - assembleCoadd
        description: |
          Tasks that can be run together, but only after the 'step1' and 'step2'
          subsets.
    
          These should be run with explicit 'tract' constraints essentially all the
          time, because otherwise quanta will be created for jobs with only partial
          visit coverage.
    
          It is expected that many forcedPhotCcd quanta will "normally" fail when
          running this subset, but this isn't a problem right now because there are
          no tasks downstream of it.  If other tasks regularly fail or we add tasks
          downstream of forcedPhotCcd, these subsets or the tasks will need
          additional changes.
    
          This subset is considered a workaround for missing middleware and task
          functionality.  It may be removed in the future.
