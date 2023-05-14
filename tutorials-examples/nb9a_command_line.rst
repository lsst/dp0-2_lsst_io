######################################################
02. Custom Coadds from the Command Line (advanced)
######################################################

.. This section should provide a brief, top-level description of the page.

**Contact author:** Aaron Meisner

**Last verified to run:** 05/14/2023

**Targeted learning level:** Advanced

**Container size:** large

**Credit:** This command line tutorial is based on the `corresponding notebook tutorial <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_ by Melissa Graham. The command line approach is heavily influenced by Shenming Fu's recipe for reducing `DECam <https://noirlab.edu/science/programs/ctio/instruments/Dark-Energy-Camera>`_ data with the Gen3 LSST Science Pipelines, which is in turn based on `Lee Kelvin's Merian processing instructions <https://hackmd.io/@lsk/merian>`_.

**Introduction:** 
This tutorial shows how to use command line ``pipetask`` invocations to produce custom coadds from simulated single-exposure Rubin/LSST images. It is meant to parallel the corresponding Jupyter Notebook tutorial entitled `Construct a Custom Coadded Image <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_.

The peak memory of this custom coadd processing is between 8 and 9 GB, hence a large container is necessary.

This tutorial uses the Data Preview 0.2 (DP0.2) data set.
This data set uses a subset of the DESC's Data Challenge 2 (DC2) simulated images, which have been reprocessed by Rubin Observatory using Version 23 of the LSST Science Pipelines.
More information about the simulated data can be found in the DESC's `DC2 paper <https://ui.adsabs.harvard.edu/abs/2021ApJS..253...31L/abstract>`_ and in the `DP0.2 data release documentation <https://dp0-2.lsst.io>`_.


**WARNING:
This custom coadd tutorial will only run with LSST Science Pipelines version Weekly 2022_40.**

To find out which version of the LSST Science Pipelines you are using, look in the footer bar.

If you are using ``w_2022_40``, you may proceed with executing the custom coadd notebooks.

If you are **not** using ``w_2022_40`` you **must** log out and start a new server:
 1. At top left in the menu bar choose File then Save All and Exit.
 2. Re-enter the Notebook Aspect.
 3. At `the "Server Options" stage <https://dp0-2.lsst.io/data-access-analysis-tools/nb-intro.html#how-to-log-in-navigate-and-log-out-of-jupyterlab>`_, under "Select uncached image (slower start)" choose ``w_2022_40``.
 4. Note that it might take a few minutes to start your server with an old image.

**Why do I need to use an old image for this tutorial?**
In this tutorial and in the future with real LSST data, users will be able to recreate coadds starting with intermediate data products (the `warps <https://pipelines.lsst.io/getting-started/coaddition.html?highlight=warp#warping-images-onto-the-skymap>`_).
On Feb 16 2023, as documented in the `Major Updates Log <https://dp0-2.lsst.io/tutorials-examples/major-updates-log.html#major-updates-log>`_ for DP0.2 tutorials, the recommended image of the RSP at `data.lsst.cloud <https://data.lsst.cloud/>`_ was bumped from Weekly 2022_40 to Weekly 2023_07.
However, the latest versions of the pipelines are not compatible with the intermediate data products of DP0.2, which were produced in early 2022.
To update this tutorial to be able to use Weekly 2023_07, it would have to demonstrate how to recreate coadds *starting with the raw data products*.
This is pedagogically undesirable because it does not accurately represent *future workflows*, which is the goal of DP0.2.
Thus, it is recommended that delegates learn how to recreate coadds with Weekly 2022_40.

Step 1. Access the terminal and set up
=====================================

1.0. Recall the scientific context motivating custom coadds

Per `notebook 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_, a (hypothetical) supernova went off at (RA, Dec) = (55.745834, -32.269167) degrees on MJD = 60960. You wish to make a custom coadd of input DESC DC2 simulated exposures corresponding to a specific MJD range, nicknamed "Window1": 60925 < MJD < 60955, roughly the month leading up to the explosion. The science goal is to search for any potential supernova precursor in the pre-explosion imaging, without contamination by the post-explosion transient.

1.1. Log in to the Notebook Aspect. The terminal is a subcomponent of the Notebook Aspect.

1.2. In the launcher window under "Other", select the terminal.

1.3. Set up the Rubin/LSST software stack environment.

.. code-block::

    $ setup lsst_distrib
    
In this tutorial, the ``$`` sign is used to indicate a command issued at the RSP terminal -- do not include the ``$`` in the command you issue.

1.4. Perform a command line verification that you are using the correct ``w_2022_40`` version of the LSST Science Pipelines.

.. code-block::

     $ eups list lsst_distrib
     g0b29ad24fb+9b30730ed8       current w_2022_40 setup

Step 2. Create your custom coaddition pipeline
=============================================

As you saw in `tutorial notebook 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_, you do not need to rerun the entire DP0.2 data processing in order to obtain custom coadds. You only need to run a subset of the tasks that make up ``step3`` of the DP0.2 processing, where ``step3`` refers to coadd-level processing. Specifically, you want to rerun only the ``makeWarp`` and ``assembleCoadd`` tasks.

The strategy for running these custom coadds via the command line is to start with the "Data Release Production" (DRP) pipeline used for DP0.2 processing and make relatively minor edits to isolate the specific ``makeWarp`` and ``assembleCoadd`` tasks of interest.

2.1. Inspect the DP0.2 YAML pipeline definition

Ensure that you're in the working directory on RSP that you've chosen to be the place from which you will run the custom coadd processing. Let's start by making a local copy of the DRP YAML pipeline definition file for DP0.2. It is conventional to put pipeline definition YAML files in a ``pipelines`` subdirectory, so let's make one in your current working directory:

.. code-block::

    $ mkdir pipelines

Now make yourself a local copy of the full DP0.2 pipeline definition YAML:

.. code-block::

    $ pipetask build -p $DRP_PIPE_DIR/pipelines/LSSTCam-imSim/DRP-test-med-1.yaml \
    --show pipeline > pipelines/MakeWarpAssembleCoadd.yaml

The above is the first of several ``pipetask`` commands used throughout this tutorial. `pipetask <https://pipelines.lsst.io/modules/lsst.ctrl.mpexec/pipetask.html>`_ commands are provided as part of the LSST Science Pipelines software stack and are used to build, visualize, and run processing pipelines from the terminal. When used as above with the ``--show pipeline`` option, ``pipetask build`` simply assembles and prints out the YAML pipeline definition specified via the ``-p`` argument.

Now let's take a look at your newly created ``pipelines/MakeWarpAssembleCoadd.yaml`` pipeline definition file. There are multiple ways to view an `ASCII <https://en.wikipedia.org/wiki/ASCII>`_ (plain text) file such as ``pipelines/MakeWarpAssembleCoadd.yaml`` from a Linux terminal. Let's use a program called `head <https://en.wikipedia.org/wiki/Head_(Unix)>`_.


.. code-block::

    $ head -3151 pipelines/MakeWarpAssembleCoadd.yaml  |tail -19
      step3:
        subset:
            - writeObjectTable
            - forcedPhotCoadd
            - templateGen
            - measure
            - healSparsePropertyMaps
            - mergeMeasurements
            - consolidateObjectTable
            - mergeDetections
            - makeWarp
            - deblend
            - detection
            - assembleCoadd
            - selectGoodSeeingVisits
            - transformObjectTable
            description: |
              Tasks that can be run together, but only after the 'step1' and 'step2'
              subsets.

The specific arguments to ``head`` and ``tail`` here are used to only show the relevant lines of the full YAML file. Reading through other sections of ``pipelines/MakeWarpAssembleCoadd.yaml`` is left as an optional exercise for the learner.

2.2. Edit the YAML pipeline definition for making custom coadds
    
Now let's edit your ``pipelines/MakeWarpAssembleCoadd.yaml`` pipeline definition file. There are multiple ways to edit a text file in a Linux environment, such as `nano <https://www.nano-editor.org/>`_, `emacs <https://www.gnu.org/software/emacs/>`_, and `vim <https://www.vim.org/>`_, all of which are available to you at the RSP terminal.

Using whichever text editor option you prefer, edit the ``step3`` section of ``pipelines/MakeWarpAssembleCoadd.yaml`` so that only the ``makeWarp`` and ``assembleCoadd`` tasks remain. To do this, you should delete exactly 12 lines of YAML from within the ``step3`` section, specifically the lines containing: ``- detection``, ``- mergeDetections``, ``- deblend``, ``- measure``, ``- mergeMeasurements``, ``- forcedPhotCoadd``, ``- transformObjectTable``, ``- writeObjectTable``, ``- consolidateObjectTable``, ``- healSparsePropertyMaps``, ``- selectGoodSeeingVisits``, and ``- templateGen``. Now the `step3` YAML section shown above in Section 2.1 should look like this:

.. code-block::

      step3:
        subset:
          - makeWarp
          - assembleCoadd
          description: |
            Tasks that can be run together, but only after the 'step1' and 'step2'
            subsets.

Make sure to save your changes when you exit the text editor! Also make sure that you did not change any of the indentation in the ``pipelines/MakeWarpAssembleCoadd.yaml`` file, for the lines that remain. Note that the ordering of the ``- makeWarp`` and ``- assembleCoadd`` lines relative to each other `does not matter <https://pipelines.lsst.io/modules/lsst.pipe.base/creating-a-pipeline.html#a-basic-pipeline>`_.

Step 3. Show your pipeline and its configurations
=================================================

3.1 Choose an output collection name/location

.. probably want to change where this appears relative to other items, figure out later

Some of the ``pipetask`` commands later in this tutorial require you to specify an output collection where your new coadds will eventually be written to. As described in the notebook version of `tutorial 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_, you want to name your output collection as something like ``u/<Your User Name>/<Collection Identifier>``. As a concrete example, throughout the rest of this tutorial ``u/$USER/custom_coadd_window1_cl00`` is used as the collection name (``$USER`` is a Linux environment variable that stores your RSP user name).

3.2 Build your custom-defined pipeline

Let's not jump straight into running the pipeline, but rather start by checking whether the pipeline will first ``build``. To ``build`` a pipeline, you use a command starting with ``pipetask build`` and specify the ``-p`` argument telling ``pipetask`` which specific YAML pipeline definition file you want it to build. If there are syntax or other errors in the YAML file's pipeline definition, then ``pipetask build`` will fail with an error about the problem. If ``pipetask build`` succeeds, it will run without generating errors and print a YAML version of the pipeline to `standard output <https://en.wikipedia.org/wiki/Standard_streams#Standard_output_(stdout)>`_. Here is the exact syntax:

.. code-block::

    $ pipetask build \
    -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    --show pipeline
    
This is all one single terminal (shell) command, but spread out over three input lines using ``\`` for line continuation. It would be entirely equivalent to run:

.. code-block::

    $ pipetask build -p pipelines/MakeWarpAssembleCoadd.yaml#step3 --show pipeline
    
The ``-p`` parameter of ``pipetask`` is short for ``--pipeline`` and it is critical that this parameter be specified as the new ``pipelines/MakeWarpAssembleCoadd.yaml`` file made in section 2.2. It is also critical that the ``-p`` argument contain the string ``#step3`` appended at the end of the config file name. This is because you want to only run the coaddition step to make custom coadds. Here's what running the command, and its output should look like:

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

``pipetask --help`` provides documentation about ``pipetask``, if you are (optionally) interested in learning more about ``pipetask`` and its command line options.

3.3 Customize and inspect the coaddition configurations

As mentioned in `tutorial notebook 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_, there are a couple of specific coaddition configuration parameters that need to be set in order to accomplish the desired custom coaddition. In detail, the ``makeWarp`` `Task` needs two of its configuration parameters modified: ``doApplyFinalizedPsf`` and ``connections.visitSummary``. First, let's try an experiment of simply finding out what the default value of ``doApplyFinalizedPsf`` is, so that you can appreciate the results of having modified this parameteter later on. To view the configuration parameters, you need to use a ``pipetask run`` command, not a ``pipetask build`` command. The command used is shown here, and will be explained below:

.. code-block::

    $ pipetask run \
    -b dp02 \
    -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    --show config=makeWarp::doApplyFinalizedPsf
    
Notice that the ``-p`` parameter passed to ``pipetask`` has remained the same. But in order for ``pipetask run`` to operate, it also needs to know what Butler repository it's dealing with. That's why the ``-b dp02`` argument has been added. ``dp02`` is an alias that points to the `S3 <https://en.wikipedia.org/wiki/Amazon_S3>`_ location of the DP0.2 Butler repository.

The final line merits further explanation. ``--show config`` tells the LSST pipelines not to actually run the pipeline, but rather to only show the configuration parameters, so that you can understand all the detailed choices being made by your processing, if desired. The last line would be valid as simply ``--show config``. However, this would print out every single configuration parameter and its description -- more than 1300 lines of printouts in total! Appending ``=<Task>::<Parameter>`` to ``--show config`` specifies exactly which parameter you want to be shown. In this case, it's known from `tutorial notebook 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_ that you want to adjust the ``doApplyFinalizedPsf`` parameter of the ``makeWarp`` Task, hence why ``makeWarp::doApplyFinalizedPsf`` is appended to ``--show config``.

Now let's look at what happens when you run the above ``pipetask command``:

.. code-block::

    $ pipetask run \
    > -b dp02 \
    > -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    > --show config=makeWarp::doApplyFinalizedPsf
    Matching "doApplyFinalizedPsf" without regard to case (append :NOIGNORECASE to prevent this)
    ### Configuration for task `makeWarp'
    # Whether to apply finalized psf models and aperture correction map.
    config.doApplyFinalizedPsf=True
    No quantum graph generated or pipeline executed. The --show option was given and all options were processed.
    
Ignore the lines about "No quantum graph" and "NOIGNORECASE" -- for the present purposes, these can be considered non-fatal warnings. The line that starts with ``###`` specificies that ``pipetask run`` is showing us a parameter of the ``makeWarp`` Task (as opposed to some other task, like ``assembleCoadd``). The line that starts with ``#`` provides the plain English description of the parameter that you requested to be shown. The line following the plain English description of ``doApplyFinalizedPsf`` shows this parameter's default value, which is a boolean equal to ``True``. From `tutorial notebook 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_, you know that it's necessary to change ``doApplyFinalizedPsf`` to ``False`` i.e., the opposite of its default value. The following modified ``pipetask run`` command adds one extra ``-c`` input parameter for the custom ``doApplyFinalizedPsf`` setting:

.. code-block::

    $ pipetask run \
    -b dp02 \
    -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    -c makeWarp:doApplyFinalizedPsf=False \
    --show config=makeWarp::doApplyFinalizedPsf
    
The penultimate line (``-c makeWarp:doApplyFinalizedPsf=False \``) is newly added. The ``-c`` parameter of ``pipetask run`` (note the lower case ``c``) can be used to specify a desired value of a given parameter, with argument syntax of ``<Task>:<Parameter>=<Value>``. In this case, the Task is ``makeWarp``, the parameter is ``doApplyFinalizedPsf``, and the desired value is ``False``. Now find out if you succeeded in changing the configuration, by looking at the printouts generated from running the above command:

.. code-block::

    $ pipetask run \
    > -b dp02 \
    > -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    > -c makeWarp:doApplyFinalizedPsf=False \
    > --show config=makeWarp::doApplyFinalizedPsf
    Matching "doApplyFinalizedPsf" without regard to case (append :NOIGNORECASE to prevent this)
    ### Configuration for task `makeWarp'
    # Whether to apply finalized psf models and aperture correction map.
    config.doApplyFinalizedPsf=False

    No quantum graph generated or pipeline executed. The --show option was given and all options were processed.
    
Notice that the printed configuration parameter value is indeed ``False`` i.e., not the default value...great! The second configuration parameter that you need to change can be passed to ``pipetask run`` in exactly the same way, by simply adding a second ``-c`` argument whose line in the full shell command looks like:

.. code-block::

    -c makeWarp:connections.visitSummary="visitSummary" \
    
Step 4. Explore and visualize the ``QuantumGraph``
==================================================

Before actually deploying the custom coaddition, let's take some time to understand the ``QuantumGraph`` of the processing to be run. The ``QuantumGraph`` is `a tool <https://pipelines.lsst.io/py-api/lsst.pipe.base.QuantumGraph.html#lsst.pipe.base.QuantumGraph>`_ used by the LSST Science Pipelines to break a large processing into relatively "bite-sized" quanta and arrange these quanta into a sequence such that all inputs needed by a given quantum are available for the execution of that quantum. In the present case, you will not be doing an especially large processing, but for production deployments it makes sense to inspect and validate the ``QuantumGraph`` before proceeding straight to full-scale processing launch.

So far, you've seen ``pipetask build`` and ``pipetask run``. For the ``QuantumGraph``, you'll use another ``pipetask`` variant, ``pipetask qgraph``. ``pipetask qgraph`` determines the full list of quanta that your processing will entail, so at this stage it's important to bring in the query constraints that specify what subset of DP0.2 will be analyzed. This information is already available from `notebook tutorial 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_. In detail, you want to make a coadd only for ``patch=4431``, ``tract=17`` of the ``DC2`` ``skyMap``, and only using a particular set of 6 input exposures drawn from a desired temporal interval (``visit`` = 919515, 924057, 924085, 924086, 929477, 930353). `Tutorial notebook 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_ also provides a translation of these constraints into `Butler query syntax <https://pipelines.lsst.io/modules/lsst.daf.butler/queries.html>`_ as:

.. code-block::

    tract = 4431 AND patch = 17 AND visit in (919515,924057,924085,924086,929477,930353) AND skymap = 'DC2'

4.1 What are the quanta?

`Tutorial notebook 9a <https://github.com/rubin-dp0/tutorial-notebooks/blob/main/09_Custom_Coadds/09a_Custom_Coadd.ipynb>`_ shows that the desired custom coaddition entails executing 7 quanta (6 for ``makeWarp`` -- one per input exposure -- plus one for ``assembleCoadd``). Hopefully the command line version of this processing has the same number (and list) of quanta! 

You can find out full details about all quanta with a ``pipetask qgraph`` command. Here's the ``pipetask qgraph`` command:

.. code-block::

    $ pipetask qgraph \
    -b dp02 \
    -i 2.2i/runs/DP0.2 \
    -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    -c makeWarp:doApplyFinalizedPsf=False \
    -c makeWarp:connections.visitSummary="visitSummary" \
    -d "tract = 4431 AND patch = 17 AND visit in (919515,924057,924085,924086,929477,930353) AND skymap = 'DC2'" \
    --show graph
    
Be aware that this takes approximately 15 minutes to run. Note a few things about this command:

* the command starts out with ``pipetask qgraph`` rather than ``pipetask run`` or ``pipetask build``.

* the input data set ``collection`` within DP0.2 is specified via the argument ``-i 2.2i/runs/DP0.2``. It's necessary to know about the input ``collection`` in order for ``pipetask`` and Butler to figure out how many (and which) quanta are expected.

* The same custom pipeline as always is specified, ``-p pipelines/MakeWarpAssembleCoadd.yaml#step3 \``.

* ``-c`` is used twice, to override the default configuration parameter settings for both ``doApplyFinalizedPsf`` and ``connections.visitSummary``.

* The query string has speen specified via the ``-d`` argument of ``pipetask``. Including this query constraint is **really important** -- without it, Butler and ``pipetask`` might try to figure out the (huge) list of quanta for custom coaddition of the entire DP0.2 data set.

Below is the full output of running the above ``pipetask qgraph`` command:

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
 
As expected, there are 7 quanta (lines starting with ``Quantum N``), where ``N`` runs from 0-5 (inclusive) for ``makeWarp`` and then there's another ``N`` = 0 quantum for ``assembleCoadd``. Note that the exact order in which the quanta get printed out is not always guaranteed to be the same.

4.2 Visualizing the ``QuantumGraph``

In addition to generating and printing out the ``QuantumGraph`` you can also visualize the ``QuantumGraph`` as a "flowchart" style diagram. Perhaps counterintuitively, visualization of the ``QuantumGraph`` is performed with ``pipetask build`` rather than ``pipetask qgraph``. This is because the ``QuantumGraph`` visualization depends only on the structure of the pipeline definition, and not on details of exactly which patches/tracts/exposures will be processed. For this same reason, you don't need to specify all of the command line parameters (like the Butler query string) when generating the ``QuantumGraph`` visualization. The ``pipetask build`` command to generate the ``QuantumGraph`` visualization of your custom coadd processing is:


.. code-block::

    $ pipetask build \
    -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    --pipeline-dot pipeline.dot; \
    dot pipeline.dot -Tpdf > makeWarpAssembleCoadd.pdf
    
This command executes very fast (roughly 5 seconds), again because it is not performing any search through the DP0.2 data set for e.g., input exposures. The ``pipeline.dot`` output is essentially an intermediate temporary file which you may wish to delete. The PDF you make (shown below) can be opened by double clicking on its file name in the JupyterHub file browser.

.. image:: makeWarpAssembleCoadd.png
  :width: 1500
  :alt: QuantumGraph diagram for custom coaddition

Light gray rectangles with rounded corners represent data, whereas darker gray rectangles with sharp corners represent pipeline Tasks. The arrows connecting the data and Tasks illustrate the data processing flow. The data processing starts at the top, with the ``calexp`` calibrated single-exposure images (also known as Processed Visit Images; PVIs). The ``makeWarp`` Task is applied to generate reprojected "warp" images from the various input ``calexp`` images, and finally the ``assembleCoadd`` Task combines the warps into ``deepCoadd`` coadded products (light gray boxes along the bottom row). 

Step 5. Deploy your custom coadd processing
===========================================

As you might guess, the custom coadd processing is run via the ``pipetask run`` command. Because this processing takes longer than prior steps, it's worth adding a little bit of "infrastructure" around your ``pipetask run`` command to perform logging and timing. First, let's start by making a directory into which you'll send the log file of the coaddition processing:

.. code-block::

    $ export LOGDIR=logs
    $ mkdir $LOGDIR
    
Now you have a directory called ``logs`` into which you can save the pipeline outputs printed when creating your custom coadds. Also, print out the processing's start time at the very beginning and the time of completion at the very end, in both cases using the ``Linux`` ``date`` command. This will keep a record of how long your custom coadd processing took end-to-end.  Send the ``date`` printouts both to the terminal and to the log file using the Linux ``tee`` command. Putting this all together, the final commands to generate your custom coadds are:

.. code-block::

    LOGFILE=$LOGDIR/makeWarpAssembleCoadd-logfile.log; \
    date | tee $LOGFILE; \
    pipetask --long-log --log-file $LOGFILE run --register-dataset-types \
    -b dp02 \
    -i 2.2i/runs/DP0.2 \
    -o u/$USER/custom_coadd_window1_cl00 \
    -p pipelines/MakeWarpAssembleCoadd.yaml#step3 \
    -c makeWarp:doApplyFinalizedPsf=False \
    -c makeWarp:connections.visitSummary="visitSummary" \
    -d "tract = 4431 AND patch = 17 AND visit in (919515,924057,924085,924086,929477,930353) AND skymap = 'DC2'"; \
    date | tee -a $LOGFILE
    
It may be desirable to save this shell script to a file and then launch the shell script, rather than attempting to copy all of this into the terminal prompt at once. Call the shell script ``dp02_custom_coadd_1patch.sh``. This ``dp02_custom_coadd_1patch.sh`` script takes 30-35 minutes to run from start to finish. Here's what the full set of printouts looks like for a successful custom coadd processing:

.. code-block::

    $ . dp02_custom_coadd_1patch.sh
    Sun May 14 10:14:40 UTC 2023
    INFO 2023-05-14T10:31:11.940+00:00 lsst.ctrl.mpexec.cmdLineFwk ()(cmdLineFwk.py:581) - QuantumGraph contains 7 quanta for 2 tasks, graph ID: '1684060271.9353757-1754'
    INFO 2023-05-14T10:31:34.866+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 110, visit: 919515, ...}
    INFO 2023-05-14T10:31:34.866+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 113, visit: 919515, ...}
    INFO 2023-05-14T10:31:34.867+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 116, visit: 919515, ...}
    INFO 2023-05-14T10:31:38.926+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeWarp.py:448) - Processing calexp 1 of 3 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 110, visit: 919515, ...}
    INFO 2023-05-14T10:31:40.618+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:31:40.793+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:31:41.297+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:31:46.420+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:31:50.776+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:31:50.798+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeWarp.py:448) - Processing calexp 2 of 3 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 113, visit: 919515, ...}
    INFO 2023-05-14T10:32:01.297+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:32:01.987+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:32:03.961+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:32:23.401+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:32:43.236+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:32:43.377+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeWarp.py:448) - Processing calexp 3 of 3 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 116, visit: 919515, ...}
    INFO 2023-05-14T10:32:44.184+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:32:44.336+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:32:44.728+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:32:49.049+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:32:52.751+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:32:52.781+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeWarp.py:494) - directWarp has 8982709 good pixels (50.9%)
    INFO 2023-05-14T10:32:52.784+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(makeWarp.py:494) - psfMatchedWarp has 8856818 good pixels (50.2%)
    INFO 2023-05-14T10:32:58.598+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...})(singleQuantumExecutor.py:232) - Execution of task 'makeWarp' on quantum {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...} took 88.610 seconds
    INFO 2023-05-14T10:32:58.633+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-05-14T10:32:59.280+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 1 quanta successfully, 0 failed and 6 remain out of total 7 quanta.
    INFO 2023-05-14T10:33:08.346+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 139, visit: 924086, ...}
    INFO 2023-05-14T10:33:08.347+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 140, visit: 924086, ...}
    INFO 2023-05-14T10:33:08.347+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 141, visit: 924086, ...}
    INFO 2023-05-14T10:33:08.348+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 142, visit: 924086, ...}
    INFO 2023-05-14T10:33:08.348+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 143, visit: 924086, ...}
    INFO 2023-05-14T10:33:14.858+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeWarp.py:448) - Processing calexp 1 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 139, visit: 924086, ...}
    INFO 2023-05-14T10:33:21.639+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:33:22.112+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:33:23.410+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:33:37.035+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:33:50.193+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:33:50.258+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeWarp.py:448) - Processing calexp 2 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 140, visit: 924086, ...}
    INFO 2023-05-14T10:33:50.468+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:33:50.575+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:33:50.840+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:33:53.755+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:33:55.873+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:33:55.891+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeWarp.py:448) - Processing calexp 3 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 141, visit: 924086, ...}
    INFO 2023-05-14T10:33:56.686+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:33:56.842+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:33:57.251+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:34:01.708+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:34:05.597+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:34:05.621+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeWarp.py:448) - Processing calexp 4 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 142, visit: 924086, ...}
    INFO 2023-05-14T10:34:17.135+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:34:17.932+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:34:19.997+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:34:42.907+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:35:06.243+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:35:06.388+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeWarp.py:448) - Processing calexp 5 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 143, visit: 924086, ...}
    INFO 2023-05-14T10:35:08.251+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:35:08.503+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:35:09.128+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:35:16.094+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:35:22.725+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:35:22.772+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeWarp.py:494) - directWarp has 16136708 good pixels (91.5%)
    INFO 2023-05-14T10:35:22.775+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(makeWarp.py:494) - psfMatchedWarp has 15929402 good pixels (90.3%)
    INFO 2023-05-14T10:35:30.623+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...})(singleQuantumExecutor.py:232) - Execution of task 'makeWarp' on quantum {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...} took 151.343 seconds
    INFO 2023-05-14T10:35:30.641+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-05-14T10:35:31.273+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 2 quanta successfully, 0 failed and 5 remain out of total 7 quanta.
    INFO 2023-05-14T10:35:39.936+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 52, visit: 929477, ...}
    INFO 2023-05-14T10:35:39.937+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 90, visit: 929477, ...}
    INFO 2023-05-14T10:35:39.937+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 91, visit: 929477, ...}
    INFO 2023-05-14T10:35:39.937+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 92, visit: 929477, ...}
    INFO 2023-05-14T10:35:39.938+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 94, visit: 929477, ...}
    INFO 2023-05-14T10:35:48.426+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeWarp.py:448) - Processing calexp 1 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 52, visit: 929477, ...}
    INFO 2023-05-14T10:35:49.782+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:35:49.953+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (55, 55)
    INFO 2023-05-14T10:35:50.416+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:35:54.595+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:35:58.481+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:35:58.504+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeWarp.py:448) - Processing calexp 2 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 90, visit: 929477, ...}
    INFO 2023-05-14T10:36:01.927+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:36:02.218+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (55, 55)
    INFO 2023-05-14T10:36:03.067+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:36:10.056+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:36:17.549+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:36:17.600+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeWarp.py:448) - Processing calexp 3 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 91, visit: 929477, ...}
    INFO 2023-05-14T10:36:38.312+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:36:39.310+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (55, 55)
    INFO 2023-05-14T10:36:42.027+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:37:06.601+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:37:35.374+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:37:35.586+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeWarp.py:448) - Processing calexp 4 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 92, visit: 929477, ...}
    INFO 2023-05-14T10:37:36.203+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:37:36.359+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (55, 55)
    INFO 2023-05-14T10:37:36.770+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:37:40.537+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:37:43.931+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:37:43.979+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeWarp.py:448) - Processing calexp 5 of 5 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 94, visit: 929477, ...}
    INFO 2023-05-14T10:37:47.158+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:37:47.434+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (55, 55)
    INFO 2023-05-14T10:37:48.196+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:37:54.911+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:38:02.158+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:38:02.216+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeWarp.py:494) - directWarp has 16280498 good pixels (92.3%)
    INFO 2023-05-14T10:38:02.220+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(makeWarp.py:494) - psfMatchedWarp has 16091293 good pixels (91.2%)
    INFO 2023-05-14T10:38:10.318+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...})(singleQuantumExecutor.py:232) - Execution of task 'makeWarp' on quantum {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...} took 159.045 seconds
    INFO 2023-05-14T10:38:10.334+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-05-14T10:38:10.998+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 3 quanta successfully, 0 failed and 4 remain out of total 7 quanta.
    INFO 2023-05-14T10:38:14.597+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 165, visit: 930353, ...}
    INFO 2023-05-14T10:38:14.598+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 166, visit: 930353, ...}
    INFO 2023-05-14T10:38:14.598+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 168, visit: 930353, ...}
    INFO 2023-05-14T10:38:14.599+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 169, visit: 930353, ...}
    INFO 2023-05-14T10:38:19.483+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeWarp.py:448) - Processing calexp 1 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 165, visit: 930353, ...}
    INFO 2023-05-14T10:38:25.755+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:38:26.224+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:38:27.398+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:38:40.560+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:38:53.514+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:38:53.579+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeWarp.py:448) - Processing calexp 2 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 166, visit: 930353, ...}
    INFO 2023-05-14T10:38:54.004+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:38:54.166+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:38:54.585+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:38:58.963+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:39:02.174+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:39:02.199+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeWarp.py:448) - Processing calexp 3 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 168, visit: 930353, ...}
    INFO 2023-05-14T10:39:14.833+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:39:15.636+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:39:17.707+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:39:40.690+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:40:04.450+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:40:04.600+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeWarp.py:448) - Processing calexp 4 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 169, visit: 930353, ...}
    INFO 2023-05-14T10:40:07.384+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:40:07.680+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:40:08.483+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:40:16.870+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:40:24.716+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:40:24.778+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeWarp.py:494) - directWarp has 16076133 good pixels (91.1%)
    INFO 2023-05-14T10:40:24.781+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(makeWarp.py:494) - psfMatchedWarp has 15873200 good pixels (90.0%)
    INFO 2023-05-14T10:40:33.184+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...})(singleQuantumExecutor.py:232) - Execution of task 'makeWarp' on quantum {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...} took 142.185 seconds
    INFO 2023-05-14T10:40:33.200+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-05-14T10:40:33.856+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 4 quanta successfully, 0 failed and 3 remain out of total 7 quanta.
    INFO 2023-05-14T10:40:38.182+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 30, visit: 924057, ...}
    INFO 2023-05-14T10:40:38.183+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 31, visit: 924057, ...}
    INFO 2023-05-14T10:40:38.183+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 33, visit: 924057, ...}
    INFO 2023-05-14T10:40:38.183+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 34, visit: 924057, ...}
    INFO 2023-05-14T10:40:43.253+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeWarp.py:448) - Processing calexp 1 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 30, visit: 924057, ...}
    INFO 2023-05-14T10:40:50.114+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:40:50.545+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:40:51.775+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:41:04.543+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:41:17.507+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:41:17.574+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeWarp.py:448) - Processing calexp 2 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 31, visit: 924057, ...}
    INFO 2023-05-14T10:41:18.040+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:41:18.198+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:41:18.622+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:41:23.048+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:41:26.422+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:41:26.448+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeWarp.py:448) - Processing calexp 3 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 33, visit: 924057, ...}
    INFO 2023-05-14T10:41:40.652+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:41:41.460+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:41:43.758+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:42:07.117+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:42:31.068+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:42:31.221+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeWarp.py:448) - Processing calexp 4 of 4 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 34, visit: 924057, ...}
    INFO 2023-05-14T10:42:33.970+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:42:34.260+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:42:35.073+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:42:43.257+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:42:51.199+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:42:51.261+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeWarp.py:494) - directWarp has 16098179 good pixels (91.3%)
    INFO 2023-05-14T10:42:51.265+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(makeWarp.py:494) - psfMatchedWarp has 15894357 good pixels (90.1%)
    INFO 2023-05-14T10:42:59.225+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...})(singleQuantumExecutor.py:232) - Execution of task 'makeWarp' on quantum {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...} took 145.366 seconds
    INFO 2023-05-14T10:42:59.243+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-05-14T10:42:59.919+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 5 quanta successfully, 0 failed and 2 remain out of total 7 quanta.
    INFO 2023-05-14T10:43:01.395+00:00 lsst.makeWarp.select (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(selectImages.py:228) - Selecting calexp {instrument: 'LSSTCam-imSim', detector: 178, visit: 924085, ...}
    INFO 2023-05-14T10:43:02.787+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(makeWarp.py:448) - Processing calexp 1 of 1 for this Warp: id={instrument: 'LSSTCam-imSim', detector: 178, visit: 924085, ...}
    INFO 2023-05-14T10:43:06.059+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(modelPsfMatch.py:335) - compute Psf-matching kernel
    INFO 2023-05-14T10:43:06.328+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(modelPsfMatch.py:483) - Adjusted dimensions of reference PSF model from (23, 23) to (57, 57)
    INFO 2023-05-14T10:43:07.140+00:00 lsst.ip.diffim.generateAlardLuptonBasisList (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(makeKernelBasisList.py:192) - PSF sigmas are not available or scaling by fwhm disabled, falling back to config values
    INFO 2023-05-14T10:43:14.775+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(modelPsfMatch.py:358) - Psf-match science exposure to reference
    INFO 2023-05-14T10:43:21.876+00:00 lsst.makeWarp.warpAndPsfMatch.psfMatch (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(modelPsfMatch.py:373) - done
    INFO 2023-05-14T10:43:21.919+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(makeWarp.py:494) - directWarp has 831332 good pixels (4.7%)
    INFO 2023-05-14T10:43:21.921+00:00 lsst.makeWarp (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(makeWarp.py:494) - psfMatchedWarp has 805735 good pixels (4.6%)
    INFO 2023-05-14T10:43:24.869+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (makeWarp:{instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...})(singleQuantumExecutor.py:232) - Execution of task 'makeWarp' on quantum {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...} took 24.946 seconds
    INFO 2023-05-14T10:43:24.885+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-05-14T10:43:25.546+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 6 quanta successfully, 0 failed and 1 remain out of total 7 quanta.
    INFO 2023-05-14T10:43:27.536+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_directWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...} = 3.466
    INFO 2023-05-14T10:43:29.078+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_directWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...} = 4.384
    INFO 2023-05-14T10:43:29.768+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_directWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...} = 4.447
    INFO 2023-05-14T10:43:31.961+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_directWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...} = 4.550
    INFO 2023-05-14T10:43:34.291+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_directWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...} = 4.051
    INFO 2023-05-14T10:43:36.533+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_directWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...} = 3.769
    INFO 2023-05-14T10:43:36.535+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:427) - Found 6 deepCoadd_directWarp
    INFO 2023-05-14T10:43:38.125+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_psfMatchedWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 919515, ...} = 237.689
    INFO 2023-05-14T10:43:40.266+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_psfMatchedWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924057, ...} = 303.107
    INFO 2023-05-14T10:43:41.183+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_psfMatchedWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924085, ...} = 307.386
    INFO 2023-05-14T10:43:43.267+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_psfMatchedWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 924086, ...} = 294.087
    INFO 2023-05-14T10:43:45.606+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_psfMatchedWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 929477, ...} = 350.132
    INFO 2023-05-14T10:43:47.694+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:556) - Weight of deepCoadd_psfMatchedWarp {instrument: 'LSSTCam-imSim', skymap: 'DC2', tract: 4431, patch: 17, visit: 930353, ...} = 200.529
    INFO 2023-05-14T10:43:47.696+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:427) - Found 6 deepCoadd_psfMatchedWarp
    INFO 2023-05-14T10:43:47.696+00:00 lsst.assembleCoadd.assembleStaticSkyModel (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:654) - Assembling 6 deepCoadd_psfMatchedWarp
    INFO 2023-05-14T10:45:25.658+00:00 lsst.assembleCoadd.assembleStaticSkyModel.interpImage (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(interpImage.py:184) - Creating psf model for interpolation from fwhm(pixels) = 3.0 [default]
    INFO 2023-05-14T10:45:25.919+00:00 lsst.assembleCoadd.assembleStaticSkyModel.interpImage (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(interpImage.py:120) - fallbackValueType MEDIAN has been set to 0.0018
    INFO 2023-05-14T10:45:25.919+00:00 lsst.assembleCoadd.assembleStaticSkyModel.interpImage (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(interpImage.py:195) - Interpolated over 0 NO_DATA pixels.
    INFO 2023-05-14T10:45:28.948+00:00 lsst.assembleCoadd.detectTemplate (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 2763 positive peaks in 1888 footprints to 5 sigma
    INFO 2023-05-14T10:45:31.035+00:00 lsst.assembleCoadd.scaleWarpVariance (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(scaleVariance.py:130) - Renormalizing variance by 1.146336
    INFO 2023-05-14T10:45:31.693+00:00 lsst.assembleCoadd.detect (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 63 positive peaks in 35 footprints and 39 negative peaks in 24 footprints to 5 sigma
    INFO 2023-05-14T10:45:34.887+00:00 lsst.assembleCoadd.scaleWarpVariance (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(scaleVariance.py:130) - Renormalizing variance by 1.154961
    INFO 2023-05-14T10:45:35.499+00:00 lsst.assembleCoadd.detect (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 10 positive peaks in 4 footprints and 6 negative peaks in 5 footprints to 5 sigma
    INFO 2023-05-14T10:45:37.147+00:00 lsst.assembleCoadd.scaleWarpVariance (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(scaleVariance.py:130) - Renormalizing variance by 1.162910
    INFO 2023-05-14T10:45:37.821+00:00 lsst.assembleCoadd.detect (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 0 positive peaks in 0 footprints and 0 negative peaks in 0 footprints to 5 sigma
    INFO 2023-05-14T10:45:40.957+00:00 lsst.assembleCoadd.scaleWarpVariance (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(scaleVariance.py:130) - Renormalizing variance by 1.150889
    INFO 2023-05-14T10:45:41.561+00:00 lsst.assembleCoadd.detect (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 15 positive peaks in 12 footprints and 34 negative peaks in 20 footprints to 5 sigma
    INFO 2023-05-14T10:45:44.610+00:00 lsst.assembleCoadd.scaleWarpVariance (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(scaleVariance.py:130) - Renormalizing variance by 1.162911
    INFO 2023-05-14T10:45:45.250+00:00 lsst.assembleCoadd.detect (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 725 positive peaks in 151 footprints and 207 negative peaks in 126 footprints to 5 sigma
    INFO 2023-05-14T10:45:48.384+00:00 lsst.assembleCoadd.scaleWarpVariance (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(scaleVariance.py:130) - Renormalizing variance by 1.142096
    INFO 2023-05-14T10:45:49.045+00:00 lsst.assembleCoadd.detect (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(detection.py:598) - Detected 42 positive peaks in 36 footprints and 68 negative peaks in 25 footprints to 5 sigma
    INFO 2023-05-14T10:45:50.340+00:00 lsst.assembleCoadd (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(assembleCoadd.py:654) - Assembling 6 deepCoadd_directWarp
    INFO 2023-05-14T10:47:41.058+00:00 lsst.assembleCoadd.interpImage (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(interpImage.py:184) - Creating psf model for interpolation from fwhm(pixels) = 3.0 [default]
    INFO 2023-05-14T10:47:41.428+00:00 lsst.assembleCoadd.interpImage (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(interpImage.py:120) - fallbackValueType MEDIAN has been set to 0.0159
    INFO 2023-05-14T10:47:41.446+00:00 lsst.assembleCoadd.interpImage (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(interpImage.py:195) - Interpolated over 278 NO_DATA pixels.
    INFO 2023-05-14T10:47:46.729+00:00 lsst.ctrl.mpexec.singleQuantumExecutor (assembleCoadd:{band: 'i', skymap: 'DC2', tract: 4431, patch: 17})(singleQuantumExecutor.py:232) - Execution of task 'assembleCoadd' on quantum {band: 'i', skymap: 'DC2', tract: 4431, patch: 17} took 261.182 seconds
    INFO 2023-05-14T10:47:46.749+00:00 lsst.ctrl.mpexec.singleQuantumExecutor ()(singleQuantumExecutor.py:654) - Log records could not be stored in this butler because the datastore can not ingest files, empty record list is stored instead.
    INFO 2023-05-14T10:47:47.300+00:00 lsst.ctrl.mpexec.mpGraphExecutor ()(mpGraphExecutor.py:518) - Executed 7 quanta successfully, 0 failed and 0 remain out of total 7 quanta.
    Sun May 14 10:47:48 UTC 2023

The last line (before the timestamp printout) says "Executed 7 quanta successfully, 0 failed and 0 remain out of total 7 quanta". So that means every subcomponent of this custom coadd processing was successful.

Optional exercises for the learner
==========================================

* Try applying further downstream processing steps to your custom coadds, such as source detection run on the custom ``deepCoadd`` products.

* Try modifying other configuration parameters for the ``makeWarp`` and/or ``assembleCoadd`` tasks via the ``pipetask`` ``-c`` argument syntax.

* Try using the same two configuration parameter modifications as did this tutorial, but implementing them via a separate configuration (``.py``) file, rather than via the ``pipetask`` ``-c`` argument (hint: to do this, you'd use the ``-C`` argument for ``pipetask``).

* Run the ``pipetask qgraph`` command from section 4.1, but with the final line ``--show graph`` removed. This still takes roughly 15 minutes, but prints out a much more concise summary listing only the total number of quanta to be executed, which should be 7.
