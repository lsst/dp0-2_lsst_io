.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-Python-Functions:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.


################
Python Functions
################

.. This section should provide a brief, top-level description of the page.

All of these can be copy-pasted into notebooks or python scripts.


.. _Python-Functions-Cutout-Coadd:

Cutout coadd
============

In the future, the RSP will have an image cutout service and this function will not be necessary.
A demonstration of its use can be found in tutorial notebook 03a, Image Display and Manipulation.

.. code-block:: python

    def cutout_coadd(butler, ra, dec, band='r', datasetType='deepCoadd',
                     skymap=None, cutoutSideLength=51, **kwargs):
        """
        Produce a cutout from a coadd at the given ra, dec position.
        Adapted from DC2 tutorial notebook by Michael Wood-Vasey.
	
        Parameters
        ----------
        butler: lsst.daf.persistence.Butler
            Servant providing access to a data repository
        ra: float
            Right ascension of the center of the cutout, in degrees
        dec: float
            Declination of the center of the cutout, in degrees
        band: string
            Filter of the image to load
        datasetType: string ['deepCoadd']
            Which type of coadd to load.  Doesn't support 'calexp'
        skymap: lsst.afw.skyMap.SkyMap [optional]
            Pass in to avoid the Butler read.  Useful if you have lots of them.
        cutoutSideLength: float [optional]
            Size of the cutout region in pixels.
	
        Returns
        -------
        MaskedImage
        """
	
        radec = geom.SpherePoint(ra, dec, geom.degrees)
        cutoutSize = geom.ExtentI(cutoutSideLength, cutoutSideLength)
	
        if skymap is None:
            skymap = butler.get("skyMap")
	
        tractInfo = skymap.findTract(radec)
        patchInfo = tractInfo.findPatch(radec)
        xy = geom.PointI(tractInfo.getWcs().skyToPixel(radec))
        bbox = geom.BoxI(xy - cutoutSize // 2, cutoutSize)
        patch = tractInfo.getSequentialPatchIndex(patchInfo)
        coaddId = {'tract': tractInfo.getId(), 'patch': patch, 'band': band}
        parameters = {'bbox': bbox}
	
        cutout_image = butler.get(datasetType, parameters=parameters,
                                  dataId=coaddId)
	
        return cutout_image



.. _Python-Functions-Cutout-Calexp:

Cutout calexp
=============

In the future, the RSP will have an image cutout service and this function will not be necessary.
A demonstration of its use can be found in tutorial notebook 03a, Image Display and Manipulation.

.. code-block:: python

    def cutout_calexp(butler, ra, dec, visit, detector, 
                      cutoutSideLength=51, **kwargs):

        """
        Produce a cutout from a calexp at the given ra, dec position.
        Adapted from cutout_coadd which was adapted from a DC2 tutorial
        notebook by Michael Wood-Vasey.
        
        Parameters
        ----------
        butler: lsst.daf.persistence.Butler
            Servant providing access to a data repository
        ra: float
            Right ascension of the center of the cutout, in degrees
        dec: float
            Declination of the center of the cutout, in degrees
        visit: int
            Visit id of the calexp's visit
        detector: int
            Detector for the calexp
        cutoutSideLength: float [optional]
            Size of the cutout region in pixels.
        
        Returns
        -------
        MaskedImage
        """
        
        dataId = {'visit': visit, 'detector': detector}    
        radec = geom.SpherePoint(ra, dec, geom.degrees)
        cutoutSize = geom.ExtentI(cutoutSideLength, cutoutSideLength)    
        calexp_wcs = butler.get('calexp.wcs', **dataId)
        xy = geom.PointI(calexp_wcs.skyToPixel(radec))
        bbox = geom.BoxI(xy - cutoutSize // 2, cutoutSize)
        parameters = {'bbox': bbox}
	
        cutout_image = butler.get('calexp', parameters=parameters, **dataId)
        
        return cutout_image



.. _Python-Functions-Remove-Figure:

Remove figure
=============

.. code-block:: python

    def remove_figure(fig):
        """
        Remove a figure to reduce memory footprint.
        
        Parameters
        ----------
        fig: matplotlib.figure.Figure
            Figure to be removed.
        
        Returns
        -------
        None
        """
	
        # get the axes and clear their images
        for ax in fig.get_axes():
            for im in ax.get_images():
                im.remove()
        fig.clf()       # clear the figure
        plt.close(fig)  # close the figure
        gc.collect()    # call the garbage collector
