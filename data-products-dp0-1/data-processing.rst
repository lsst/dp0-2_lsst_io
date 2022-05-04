.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-1-Data-Processing-Overview:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

########################
Data Processing Overview
########################

.. This section should provide a brief, top-level description of the page.

The imaging data and catalogs included in DP0.1 are based on the wide-fast-deep data generated as part of the LSST Dark Energy Science Collaboration (DESC) Data Challenge 2 (DC2).
This page provides a brief overview of the production and processing of those data. A much more comprehensive description of DC2 can be found in `LSST Dark Energy Science Collaboration (2020) <https://arxiv.org/abs/2010.05926>`_.
This page draws heavily from those sources.


.. _Data-Processing-Overview-Image-Simulation:

Image simulation
================

The DESC DC2 image simulations are described in `Section 6 <https://arxiv.org/pdf/2010.05926.pdf#page=19>`_ of the `DC2 Paper <https://arxiv.org/abs/2010.05926>`_.
These data consist of simulated LSST images generated for 5 years of LSST wide-fast-deep observations covering ~300 \deg\ :sup:`2` of the sky centered at ``(RA, DEC)`` = ``55.064, −29.783`` degrees.
Images are simulated by the `imSim <https://github.com/LSSTDESC/imSim>`_ software package, a modular Python code that calls the GalSim software library (`Rowe et al. 2015 <https://arxiv.org/abs/1407.7676>`_) for astronomical object rendering
and is run in the LSST Science Pipelines and LSST Simulation Framework software environment (`Connolly et al. 2014 <https://ui.adsabs.harvard.edu/abs/2014SPIE.9150E..14C>`_).
The LSST software libraries provide the telescope and hardware-specific information necessary to simulate an LSST exposure, such as pixel coordinates on the focal plane, telescope filter characteristics, and the brightness of the sky.
Using that description of LSSTCam, imSim produces output files that simulate the pixel data after readout.
While imSim includes many realistic aspects of the LSST imaging (e.g., CCD geometry, electronic readout, cosmic rays, and bleed trails), there are some aspects such as scattered and reflected light from bright objects that are not included.
The input catalogs of astronomical sources are described in `Section 5 <https://arxiv.org/pdf/2010.05926.pdf#page=13>`_ of the DC2 paper.

There are several astronomical inputs into the DC2 image simulations.
The extra-galactic catalog is described in detail in `Korytov et al. (2019) <https://arxiv.org/abs/1907.06530>`_ and is based on the Outer Rim dark-matter-only cosmological simulations (`Heitmann et al. 2019 <https://arxiv.org/abs/1904.11970>`_).
Supernova are also included in the DC2 data, modeled with a volumetric rate and time evolution that matches observed data (`Dilday et al. 2010 <https://arxiv.org/abs/1001.4995>`_, `Guy et al. 2007 <https://arxiv.org/abs/astro-ph/0701828>`_).
Stars are drawn from the Galfast model of `Juric et al. (2008) <https://arxiv.org/abs/astro-ph/0510520>`_ with approximately 10% of the stellar sources assumed to be variable.
Solar system objects are not included. A flat sky background is assumed in each filter.


.. _Data-Processing-Overview-Single-Image-Processing:

Single-image processing
=======================

The LSST DESC DC2 image processing is described in `Section 7 <https://arxiv.org/pdf/2010.05926.pdf#page=24>`_ of the `DC2 Paper <https://arxiv.org/abs/2010.05926>`_.
The simulated images were processed with the Data Release Production (DRP) pipeline included as part of the `v19.0.0 <https://pipelines.lsst.io/releases/v19_0_0.html>`_ of the LSST Science Pipelines.
More detailed descriptions of the LSST Science Pipelines can be found in `Bosch et al. (2018) <https://arxiv.org/abs/1705.06766>`_ and `Bosch et al. (2019) <https://arxiv.org/abs/1812.03248>`_.
Briefly, image processing with the DRP pipeline involves four major steps – single-frame processing, joint calibration, image coaddition, and coadd processing. For single-frame processing, individual visits are processed on a per-CCD basis.
This step starts with instrument signature removal (ISR) that consists of bias subtraction, crosstalk correction, non-linearity correction, flat fielding, brighter-fatter correction, and masking of bad and saturated pixels
(see `Appendix A <https://arxiv.org/pdf/2010.05926.pdf#page=38>`_ of the DC2 paper for details).
ISR is followed by an image characterization step that performs background estimation and subtraction, Point-Spread Function (PSF) modeling, cosmic-ray detection and removal, source detection, source deblending, and source measurement.
Various measurement algorithms are applied including centroiding, aperture photometry, PSF photometry, model photometry, and shape fitting.
The image catalogs are compared to a reference catalog to generate photometric and astrometric calibrations for the images and associated catalogs.
For DC2, the photometric and astrometric calibrations are based on a simulated reference catalog.
The resulting calibrated images are known formally as "Processed Visit Images" (PVI) and informally as "calibrated exposures" (`calexps`).


.. _Data-Processing-Overview-Coadded-Image-Processing:

Coadded-image processing
========================

Calibrated images are resampled onto a common pixel grid on the sky and combined to generated deeper coadded images.
The coadd image grid is defined in terms of "tracts" and "patches", where each tract is composed of 7 × 7 patches, and each patch is 4,100 × 4,100 pixels with a pixel scale of 0.2 arcsec.
Tracts have dimensions of 1.6 degrees on a side, while patches are ~13.7 arcmin on a side (roughly the size of a CCD).
Patches overlap by 100 pixels along each edge so that objects lying on the edge of one patch are typically fully contained on the neighboring overlapping patch.
Similarly, tracts overlap their neighbors by 1 arcmin.
When producing the coadded images variable sources and artifacts using resampled PSF-matched images to produce a static image of the sky.
As described in `Aihara et al. (2019) <https://arxiv.org/abs/1905.12221>`_, each image is resampled, PSF-matched, and stacked into a 2-sigma-clipped mean coadd that serves as a model of the static scene.
A difference image was created for each image with respect to this model to identify regions associated with transient detections that only appear in a small number of epochs.
With these regions identified, the final coadded image is created as a weighted mean stack of images where the transient detections are ignored.
The PSF at any location point in the coadded image is calculated by taking a weighted sum of the PSFs from individual visit that have been resampled and weighted in the same way as the coadds.
Regions that have clipped areas will not have the correct PSF, and these are flagged for individual objects.
Before individual images are combined to form the coadd, an empirical background model is fit to the entire focal plane to control the extent to which extended features are included in the background model.


.. _Data-Processing-Overview-Coadded-Catalogs:

Coadded catalog production
==========================

The coadd catalog creation consists of five main steps: (1) above-threshold detection in each band, (2) merging the detections across bands,
(3) deblending the merged detections to generate "objects" and measuring object properties in each band, (4) identifying a reference band for each object and merging the per-band catalogs into a single object catalog to use for forced photometry,
and (5) performing forced measurements in each band using the reference band positions and shapes.
This last step produces a catalog of independent per-band object measurements that are provided to science users.


.. _Data-Processing-Overview-Postprocessing:

Post-processing
===============

The DESC DC2 data were simulated and processed using v19.0.0 of the LSST Science Pipelines which relied on the "Gen2" Butler.
For release as part of DP0.1, these data products were converted to the "Gen3" Butler system and ingested into the Interim Data Facility (IDF).
Since this was a post-processing conversion rather than a native processing with the Gen3 Butler, there may be some slight inconsistencies in the data structure that raise warnings when accessed by the user (see the :doc:`/data-access-analysis-tools/rsp-warnings`).
This should be corrected in DP0.2 when the DC2 data will be natively reprocessed with the Gen3 Butler.
We also note that the post-processing organization of the DC2 catalogs described in `Section 4 of DC2 Data Release Note <https://arxiv.org/abs/2101.04855>`_ have not been applied to the DP0.1 data.
These data are instead intended to be accessed from the Rubin Observatory TAP service.
