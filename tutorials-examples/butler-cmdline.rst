###################################################################
02. The Rubin/LSST Data Butler from the Command Line (intermediate)
###################################################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Notebook (terminal command-line)

**Contact author:** Aaron Meisner

**Last verified to run:** 8/9/2024

**LSST Science Pipelines version**:  Weekly 2024_16

**Targeted learning level:** Intermediate

**Container size:** small

**Introduction:** This tutorial is an introduction to the "Butler" command line functionality available from the `LSST Science Pipelines <https://pipelines.lsst.io/>`_ on the `Rubin Science Platform <https://data.lsst.cloud/>`_ (RSP).
It is meant to parallel, in part, the `Jupyter Notebook tutorial <https://github.com/rubin-dp0/tutorial-notebooks>`_ "Data Discovery and Query with the Butler" (DP02_04b_Intermediate_Butler_Queries.ipynb).
The Butler is the LSST Science Pipelines' infrastructure that handles retrieval of pipeline inputs and saving of pipeline outputs in such a way that the end user does not need to know about any details like file names, locations, or formats. For this reason, Butler is sometimes referred to as the LSST Science Pipelines' "middleware". This tutorial emphasizes command line invocations of the Butler, but it is also common to use Butler from within Python; several Rubin Data Preview Jupyter `notebook tutorials <https://github.com/rubin-dp0/tutorial-notebooks>`_ demonstrate the usage of Butler from within Python. You can also learn more from the `Butler documentation <https://pipelines.lsst.io/modules/lsst.daf.butler/index.html>`_.

This tutorial uses the Data Preview 0.2 (DP0.2) data set.
This data set uses a subset of the DESC's Data Challenge 2 (DC2) simulated images, which have been reprocessed by Rubin Observatory using Version 23 of the LSST Science Pipelines.
More information about the simulated data can be found in the DESC's `DC2 paper <https://ui.adsabs.harvard.edu/abs/2021ApJS..253...31L/abstract>`_ and in the `DP0.2 data release documentation <https://dp0-2.lsst.io>`_.

Step 1. Access the terminal and set up
======================================

1.1. Log in to the RSP's Notebook Aspect. The JupyterLab terminal is a subcomponent of the Notebook Aspect.

1.2. In the launcher window under “Other”, select the terminal.

1.3. Set up the LSST Science Pipelines environment

.. code-block::

    setup lsst_distrib

Then verify that you do indeed have the expected recommended weekly version of the LSST Science Pipelines in your RSP JupyterLab terminal environment:

.. code-block::

    eups list lsst_distrib

1.4. First Butler command: look at the Butler help documentation options

Help documentation for Butler command line invocations is available as follows:

.. code-block::

    butler --help

Running the preceding command is possible because ``butler`` is an executable available once the LSST Science Pipelines environment has been set up (you can see the exact location of this executable by running ``which butler`` at the terminal, if desired). There are many Butler command line options shown in this help documentation. This command line tutorial only explores a subset of the Butler's full command line capabilities.

Step 2. Query dataset types
===========================

Typically, you will `identify a specific Rubin/LSST dataset <https://pipelines.lsst.io/modules/lsst.daf.butler/organizing.html>`_ using the following three pieces of information: the dataset type, the data ID, and the collection. You can think of dataset type as being the kind of data you wish to identify, such as a single-band coadded image, a calibrated visit image, or a coadd-level source catalog. The `data ID <https://pipelines.lsst.io/modules/lsst.daf.butler/dimensions.html#lsst-daf-butler-dimensions-data-ids>`_ is a concept that's been reviewed in multiple Rubin `tutorial notebooks <https://github.com/rubin-dp0/tutorial-notebooks>`_. For instance, in the tutorial notebook entitled "Detect and Measure Sources in a Custom Coadded Image", source detection is only run on one specific i-band coadd, which has its data ID specified by tract = 4431, patch = 17, band = "i", where the tract and patch together specify the sky region and the band specifies which LSST filter. The collection is a string that specifies a particular set of persisted data for Butler to examine (note that in many contexts it is possible to specify a list of collections for Butler to search rather than a single collection). The concept of a `collection <https://pipelines.lsst.io/modules/lsst.daf.butler/organizing.html#collections>`_ is valuable because it allows for tailoring queries to work with either the default, Rubin-provided DP0.2 data sets (this default collection is called ``2.2i/runs/DP0.2``), custom user-created collections, or both.

Zooming out one level, collections exist within Butler repositories or "repos". On the RSP, the standard DP0.2 repo of Rubin-provided content is called ``dp02``. ``dp02`` therefore appears as a command line argument in many of the Butler invocations throughout this tutorial.

2.1. View the list of Butler dataset types within DP0.2

The aforementioned ``butler --help`` command shows that there is a Butler invocation pattern beginning with ``butler query-dataset-types`` with help description "Get the dataset types in a repository.'' This is useful for understanding what types of data products are or are not contained within a given Butler repo. The following command will print out a list of all dataset types within the DP0.2 repository on the RSP:

.. code-block::

    butler query-dataset-types dp02

Specifying a collection is not needed here; only the repository name ``dp02`` is provided as an argument. The :doc:`full output </tutorials-examples/query-dataset-types-printouts>` is shown on a separate page for brevity. There are more than 900 dataset types in the DP0.2 repo on RSP! Some of these are relatively recognizable and commonly used dataset types, including ``deepCoadd``, ``deepCoadd_obj``, ``raw``, ``calexp``, ``bias``, ``src``, and ``srcMatch``.

Note that you can also get help documentation specific to the ``butler query-dataset-types`` invocation pattern from the command line:

.. code-block::
    
    butler query-dataset-types --help

Step 3. Query dimension records
===============================

Per the LSST Science Pipelines `documentation <https://pipelines.lsst.io/modules/lsst.daf.butler/dimensions.html#lsst-daf-butler-dimensions-overview>`_, the Butler has a notion of ``Dimensions``, summarized as "astronomical concepts that are used to label and organize datasets...Examples of dimensions include instruments, detectors, visits, and tracts." So a ``Dimension`` is any type of parameter you might use to help fully specify a dataset of interest.

The Butler command line utility includes an invocation pattern that begins with ``butler query-dimension-records``. These ``query-dimension-records`` commands can be very valuable for exploring the content of a Butler repository from the command line. For instance, as shown below, ``query-dimension-records`` can be used to learn what different filters, visit numbers, and detectors are present within a given Butler repository, all from the command line. Full help documentation for ``butler query-dimension-records`` is available via ``butler query-dimension-records --help``.

3.1. Explore the list of filters from the command line

Let's ask and answer the following question with ``butler query-dimension-records``: what filters are present within the ``dp02`` Butler repository? In this context, ``band`` is the ``Dimension`` of interest, and ``query-dimension-records`` lists the unique ``band`` dimension values represented within the ``dp02`` repository. Execute the following command:

.. code-block::

    butler query-dimension-records dp02 band

The two arguments for the above command are the Butler repository (``dp02``) and the ``Dimension`` of interest, in this case ``band`` because of the desire to obtain the list of filters. It is not necessary to specify a collection name for ``butler query-dimension-records``. The :doc:`full output </tutorials-examples/query-dimension-records-printouts>` is shown on a separate page for brevity. From the results, it appears that there are some "bonus" bands included within the DP0.2 repository, beyond the ugrizy bands that will be present in the Rubin/LSST science survey. It is recommended to only work with the Rubin/LSST science filters ugrizy within DP0.2 on the RSP; the other ``band`` values listed generally correspond to early engineering exercises.

3.2. Instruments included in the dp02 Butler repository

For several commands later in this tutorial, it's useful to restrict to data generated by the LSST "`imSim <https://github.com/LSSTDESC/Imsim>`_" image simulation tool. Let's check what unique ``Instrument`` values are present in the ``dp02`` repo on RSP (noting that these are simulated data and so the instruments are simulation software packages not actual hardware):

.. code-block::

    butler query-dimension-records dp02 instrument

The output of the above command is:

.. code-block::

         name      visit_max exposure_max detector_max          class_name        
    -------------- --------- ------------ ------------ ---------------------------
    LSSTCam-PhoSim   9999999      9999999         1000 lsst.obs.lsst.LsstCamPhoSim
    LSSTCam-imSim   9999999      9999999         1000  lsst.obs.lsst.LsstCamImSim

Generally, restricting to images generated by imSim (``Instrument`` = LSSTCam-imSim) is helpful for the purposes of this tutorial; "PhoSim" (Instrument = ``LSSTCam-PhoSim``) is a lower level photon simulator.

3.3. Explore the list of detectors from the command line

Another reasonable question to ask when initially exploring the DP0.2 data products on RSP would be: what is the list of detectors that contribute to the overall data inventory? To do this, use ``butler query-dimension-records`` with ``detector`` as the dimension rather than ``band``. ``detector`` here means a specific CCD. Run the following command:

.. code-block::

    butler query-dimension-records dp02 detector

Like before, the two arguments for the above command are the Butler repository (``dp02``) and the ``Dimension`` of interest, in this case ``detector`` because of the desire to obtain the list of CCDs. It is not necessary to specify a collection name for ``butler query-dimension-records``. From the above command's results, it's interesting to note that there are some ``WAVEFRONT`` and ``GUIDER`` CCDs present in the simulated DP0.2 data set, in addition to the ``SCIENCE`` CCDs. It is recommended to only work with the simulated ``SCIENCE`` CCDs within DP0.2 on the RSP. The :doc:`full output </tutorials-examples/detectors-printouts>` of the above command is shown on a separate page for brevity. Note that this output contains both ``LSSTCam-imSim`` and ``LSSTCam-PhoSim`` results, which will be addressed in the next subsection.

3.4. Refine a Butler dimension record query

``butler query-dimension-records``, and other Butler command line invocation patterns, offer the very valuable ability to perform SQL-like filtering of returned results via the ``--where`` argument. The ``where`` argument for Butler command line invocations must be a string enclosed in quotes, with syntax similar to that used for ``WHERE`` clauses in `SQL <https://en.wikipedia.org/wiki/SQL>`_ or `ADQL <https://www.ivoa.net/documents/ADQL/20180112/PR-ADQL-2.1-20180112.html>`_ queries.

Here's an example of a ``butler query-dimension-records`` invocation that also brings in a SQL-like ``where`` clause to limit the amount of output, and focus only on detectors with ``id`` numbers between 6 and 8 (inclusive):

.. code-block::

    butler query-dimension-records dp02 detector --where "instrument='LSSTCam-imSim' AND detector.id IN (6..8)"

The output of the above command is:

.. code-block::

      instrument   id full_name name_in_raft raft purpose
    ------------- --- --------- ------------ ---- -------
    LSSTCam-imSim   6   R01_S20          S20  R01 SCIENCE
    LSSTCam-imSim   7   R01_S21          S21  R01 SCIENCE
    LSSTCam-imSim   8   R01_S22          S22  R01 SCIENCE

The ``instrument='LSSTCam-imSim'`` portion of the query is required (if absent, an error would result). The LSST Science Pipelines `documentation <https://pipelines.lsst.io/modules/lsst.daf.butler/queries.html>`_ contains further information about Butler query syntax.

3.5. Spatially restricted query of DP0.2 exposures

Putting together Butler's ``query-dimension-records`` and ``where`` argument filtering, perform a spatial query on exposures in the dp02 Butler repo as follows:

.. code-block::
    
    butler query-dimension-records dp02 exposure --where "instrument='LSSTCam-imSim' AND exposure.tracking_ra > 53.0 AND exposure.tracking_ra < 53.0002" 

The output of the above command is:

.. code-block::

      instrument     id   physical_filter  obs_id exposure_time dark_time observation_type observation_reason day_obs  seq_num group_name group_id target_name science_program    tracking_ra       tracking_dec        sky_angle         zenith_angle                  timespan (TAI)              
    ------------- ------- --------------- ------- ------------- --------- ---------------- ------------------ -------- ------- ---------- -------- ----------- --------------- ----------------- ------------------ ------------------ ------------------ ------------------------------------------
    LSSTCam-imSim  202462       g_sim_1.4  202462          30.0      30.0          science              imsim 20221001       0     202462   202462     UNKNOWN          202462 53.00018875481526 -27.39918586728378   300.340730287346 30.851948317324634 [2022-10-02T05:10:33, 2022-10-02T05:11:03)
    LSSTCam-imSim  427087       z_sim_1.4  427087          30.0      30.0          science              imsim 20230830       0     427087   427087     UNKNOWN          427087 53.00006696621878  -31.6170143466886  74.39265729448658 14.782812793171615 [2023-08-31T08:29:14, 2023-08-31T08:29:44)
    LSSTCam-imSim  470443       i_sim_1.4  470443          30.0      30.0          science              imsim 20231118       0     470443   470443     UNKNOWN          470443 53.00006155463241 -27.50071382700686  41.46698793005794  38.04876864900619 [2023-11-19T01:29:17, 2023-11-19T01:29:47)
    LSSTCam-imSim  709719       z_sim_1.4  709719          30.0      30.0          science              imsim 20241112       0     709719   709719     UNKNOWN          709719 53.00003150603273 -27.35089052186188  69.77305663201832   35.7790473845536 [2024-11-13T07:27:01, 2024-11-13T07:27:31)
    LSSTCam-imSim  732227       z_sim_1.4  732227          30.0      30.0          science              imsim 20241217       0     732227   732227     UNKNOWN          732227 53.00011899044281 -27.53881903559373  257.8766252269814  21.50198032659604 [2024-12-18T04:03:34, 2024-12-18T04:04:04)
    LSSTCam-imSim  950384       u_sim_1.4  950384          30.0      30.0          science              imsim 20251023       0     950384   950384     UNKNOWN          950384  53.0000299236379   -27.406067390404  48.48529963673576  43.61972031905932 [2025-10-24T02:43:36, 2025-10-24T02:44:06)
    LSSTCam-imSim  955121       r_sim_1.4  955121          30.0      30.0          science              imsim 20251029       0     955121   955121     UNKNOWN          955121 53.00000406576612 -27.37569446275185 227.18038983167162  36.82874161171403 [2025-10-30T02:51:42, 2025-10-30T02:52:12)
    LSSTCam-imSim  976771       z_sim_1.4  976771          30.0      30.0          science              imsim 20251209       0     976771   976771     UNKNOWN          976771 53.00006086158266 -27.35854559192086 185.72856377252242   8.46669843785567 [2025-12-10T03:34:51, 2025-12-10T03:35:21)
    LSSTCam-imSim 1194599       y_sim_1.4 1194599          30.0      30.0          science              imsim 20261016       0    1194599  1194599     UNKNOWN         1194599 53.00007698977164 -27.44389935977285  291.1579519122609 21.546698575031996 [2026-10-17T04:54:23, 2026-10-17T04:54:53)

The first two arguments for the above command are, as seen previously, the Butler repository (``dp02``) and the ``Dimension`` of interest (in this case ``exposure``). Without the ``where`` argument, a dramatically longer list of simulated DP0.2 exposures would be printed out. The ``where`` clause specified above restricts the list of returned exposures to only 9 items. As shown in the `DP0.2 Data Products Definition Document <https://dp0-2.lsst.io/data-products-dp0-2/index.html#dp0-2-data-products-definition-document-dpdd>`_, DP0.2 covers a subregion within the eventual LSST footprint, with RA values spanning from roughly 50 degrees to 75 degrees, hence why the above query has chosen to look at a narrow range of RA around RA = 53 degrees. The ``instrument='LSSTCam-imSim'`` portion of the ``where`` argument query is required (if absent, an error would result); this specifies the instrument for Butler to consider when retrieving the exposure list. It is not currently possible to perform a ``butler`` command line query that would do a cone search based on the RA and Dec coordinates of exposures.

3.6. Temporally restricted query

It is also possible to perform a temporally constrained query rather than a spatially constrained query. The following command is an example using the ``where`` argument of ``query-dimension-records``:

.. code-block::
    
    butler query-data-ids dp02 exposure --where "instrument='LSSTCam-imSim' AND exposure.timespan OVERLAPS (T'2023-11-19T01:29:17',T'2023-11-19T01:31:25')"

The output of the above command is:

.. code-block::

      instrument  exposure band physical_filter
    ------------- -------- ---- ---------------
    LSSTCam-imSim   470444    i       i_sim_1.4
    LSSTCam-imSim   470445    i       i_sim_1.4
    LSSTCam-imSim   470446    i       i_sim_1.4
    LSSTCam-imSim   470447    i       i_sim_1.4

This example command uses the ``OVERLAPS`` `operator <https://pipelines.lsst.io/modules/lsst.daf.butler/queries.html#overlaps-operator>`_. Note that time literals like ``T'2023-11-19T01:29:17'`` in the query begin with ``T`` and enclose the timestamp in single quotes. Then two timestamp literals separated by a comma and enclosed together within parentheses specifies a time interval within which to search. The `Butler query documentation <https://pipelines.lsst.io/modules/lsst.daf.butler/queries.html>`_ provides further information about timestamp literals, time intervals, and the ``OVERLAPS`` operator.

Step 4. Querying dataID values
==============================

To identify lists of relevant datasets, which are specified by data IDs, use the ``butler query-data-ids`` invocation pattern. ``butler query-data-ids`` prints out a list of all datasets of a user-specified type. Full help for ``butler query-data-ids`` is available via the following command:

.. code-block::

    butler query-data-ids --help

Let's start off with a relatively standard, familiar dataset type within DP0.2: ``deepCoadd``. Recall that an LSST Science Pipelines ``deepCoadd`` data product is a stacked image using all good exposures to make a coadd that emphasizes depth (as apposed to, say, ``goodSeeingCoadd``, which emphasizes angular resolution). ``deepCoadd`` data products are very generally useful, for instance to study faint galaxies or distant stars within the Milky Way. The following command prints out a full list of ``deepCoadd`` tract identifiers within the ``dp02`` Butler repository on RSP:

.. code-block::

    butler query-data-ids dp02 tract --collections 2.2i/runs/DP0.2 --datasets 'deepCoadd' 

Recall that a tract is a relatively large sky region within a given sky map, and then patches are smaller subregions within each tract. The first argument to ``butler query-data-ids`` above specifies, as usual, the ``dp02`` Butler repo on RSP. The second argument specifies the ``Dimension`` of interest -- that Butler should return the list of unique ``tract`` values corresponding to ``deepCoadd`` products in the DP0.2 repository. The third ``--collections`` argument specifies that Butler should consider only the production DP0.2 output collection; this will ignore any results that might be found from bespoke user-created collections on RSP. The :doc:`full output </tutorials-examples/query-dataids-tracts-printouts>` of the above command is shown on a separate page for brevity.

Let's restrict the output to only the returned data rows, as follows, upon noting that each data row contains the string "DC2" for the ``skymap``, and then count the number of returned results with the ``wc`` unix utility program:

.. code-block::

    butler query-data-ids dp02 tract --collections 2.2i/runs/DP0.2 --datasets 'deepCoadd' |grep DC2 |wc -l
    157

This value of 157 makes sense, as there are 157 tracts worth of sky coverage in DP0.2.

Now use Butler from the command line to figure out how many coadd patches there are in the DP0.2 data set:

.. code-block::

    butler query-data-ids dp02 patch --collections 2.2i/runs/DP0.2 --datasets 'deepCoadd' |grep DC |wc -l
    7693

Note that this command is almost identical to the one before it, but with ``patch`` rather than ``tract`` specified as the ``Dimension`` of interest. The resulting value of 7693 makes sense, because there are 157 DP0.2 coadd tracts, and each of these tracts consists of a grid of 7x7 = 49 patches. So then there should be 157 tracts x 49 patches/tract = 7693 patches in DP0.2.

Step 5. Optional exercises for the learner
==========================================

1. ``butler query-data-ids`` also accepts a ``where`` argument to narrow down queries. Try issuing a ``butler query-data-ids`` command that only returns a list of i-band ``deepCoadd`` products, rather than all bands.
2. Use ``butler query-data-ids`` to obtain a list of tracts that have ``goodSeeingCoadd`` data products within the DP0.2 repository on RSP.
3. Refine the Section 3.3 query for available detectors so as to remove results that arise from the "PhoSim" simulator using a query restriction based on instrument.

