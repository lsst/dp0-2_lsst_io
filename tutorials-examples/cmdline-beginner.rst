.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Cmndline-Beginner:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

####################################
01. Introduction to DP0.2 (beginner)
####################################

.. This section should provide a brief, top-level description of the page.

**Contact author:** Gloria Fonseca Alvarez

**Last verified to run:** 02/01/2023

**Targeted learning level:** Beginner

**Container size:** medium

**Introduction:** 
This tutorial is an introduction to the terminal and command line functionality within the Rubin Science Platform.
It is parallel to the Jupyter Notebook tutorial "Introduction to DP02" and demonstrates how to use the TAP service to query and retrieve catalog data;
matplotlib to plot catalog data; the LSST Butler package to query and retrieve image data; and the LSST afwDisplay image package.

This tutorial uses the Data Preview 0.2 (DP0.2) data set.
This data set uses a subset of the DESC's Data Challenge 2 (DC2) simulated images, which have been reprocessed by Rubin Observatory using Version 23 of the LSST Science Pipelines.
More information about the simulated data can be found in the DESC's `DC2 paper <https://ui.adsabs.harvard.edu/abs/2021ApJS..253...31L/abstract>`_ and in the `DP0.2 data release documentation <https://dp0-2.lsst.io>`_.


.. _DP0-2-Cmndline-Beginner-Step-1:

Step 1. Access the terminal and setup
=====================================

1.1. Log in to the Notebook Aspect. The terminal is a subcomponent of the Notebook Aspect.

1.2. In the launcher window under "Other", select the terminal.

.. figure:: /_static/other_terminal.png
	:alt: Options visible in the section of the launcher entitled other within the notebook aspect.  
		Selections from the left are: terminal launcher, text file, markdown file, python file, and a help button. 

1.3. Set up the Rubin Observatory environment.

.. code-block::

    setup lsst_distrib

1.4. Start an interactive Python session.

.. code-block::

    python


.. _DP0-2-Cmndline-Beginner-Step-2:

Step 2. Import packages
=======================

This tutorial makes use of several packages that will be commonly used when interacting with catalog and image data. 

2.1. Import general python packages.

.. code-block::

    import numpy
    import matplotlib
    import matplotlib.pyplot as plt

2.2. Import packages needed to access the catalog data.

.. code-block::

    import pandas 
    pandas.set_option('display.max_rows', 1000)
    from lsst.rsp import get_tap_service, retrieve_query

2.3. Import packages needed to access images.

.. code-block::

    import lsst.daf.butler as dafButler
    import lsst.geom
    import lsst.afw.display as afwDisplay



.. _DP0-2-Cmndline-Beginner-Step-3:

Step 3. Retrieve data using TAP for 10 objects
==============================================

Table Access Procotol (TAP) provides standardized access to the catalog data for discovery, search, and retrieval.
`Full documentation for TAP <https://www.ivoa.net/documents/TAP/>`_ is provided by the International Virtual Observatory Alliance (IVOA).
The TAP service uses a query language similar to SQL (Structured Query Langage) called ADQL (Astronomical Data Query Language).
The `documentation for ADQL <https://www.ivoa.net/documents/latest/ADQL.html>`_ includes more information about syntax and keywords.

Notice: Not all ADQL functionality is supported by the RSP for Data Preview 0.

This example uses the DP0.2 Object catalog, which contains sources detected in the coadded images (also called stacked, combined, or deepCoadd images).

3.1. Start the TAP service .

.. code-block::

    service = get_tap_service()
    
3.2. Define the coordinates for a cone search centered around the region covered by the DC2 simulation (RA,Dec = 62,-37).

.. code-block::

    use_center_coords = "62, -37"

3.3. Create a query named my_adql_query to retrieve the coordinates and g, r, i magnitudes for objects within 0.5 degrees of the center coordinates.

.. code-block:: 

   my_adql_query = "SELECT coord_ra, coord_dec, detect_isPrimary, " + \
                "r_calibFlux, r_cModelFlux, r_extendedness " + \
                "FROM dp02_dc2_catalogs.Object " + \
                "WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), " + \
                "CIRCLE('ICRS', " + use_center_coords + ", 0.5)) = 1 "

3.4. Retrieve and display the results of the query for 10 objects.

.. code-block::

    results = service.search(my_adql_query, maxrec=10)
    results_table = results.to_table()
    print(results_table)   

3.5. Convert fluxes into magnitudes.

The object and source catalogs store only fluxes.
There are hundreds of flux-related columns, and to store them also as magnitudes would be redundant, and a waste of space.
All flux units are nanojanskys (nJy).
To convert nJy to AB magnitudes use: |mab| = -2.5log(|fnJy|) + 31.4. 

.. |mab| replace:: m\ :sub:`AB`\ 
.. |fnJy| replace:: f\ :sub:`nJy`\

Add columns of magnitudes after retrieving columns of flux.

.. code-block::
   
     results_table['r_calibMag'] = -2.50 * numpy.log10(results_table['r_calibFlux']) + 31.4
     results_table['r_cModelMag'] = -2.50 * numpy.log10(results_table['r_cModelFlux']) + 31.4
     
Display the results table including the magnitudes.

.. code-block::

    print(results_table) 



.. _DP0-2-Cmndline-Beginner-Step-4:

Step 4. Retrieve data using TAP for 10,000 objects
==================================================

To retrieve columns of fluxes as magnitudes in an ADQL query, users can do this:
scisql_nanojanskyToAbMag(g_calibFlux) as g_calibMag,
and columns of magnitude errors can be retrieved with:
scisql_nanojanskyToAbMagSigma(g_calibFlux, g_calibFluxErr) as g_calibMagErr.

4.1. Retrieve g-, r- and i-band magnitudes for 10000 point-like objects.

In addition to a cone search, impose query restrictions that detect_isPrimary is True (this will not return deblended "child" sources), that the calibrated flux is greater than 360 nJy (about 25th mag), and that the extendedness parameters are 0 (point-like sources).

.. code-block::

 results = service.search("SELECT coord_ra, coord_dec, "
                         "scisql_nanojanskyToAbMag(g_calibFlux) as g_calibMag, "
                         "scisql_nanojanskyToAbMag(r_calibFlux) as r_calibMag, "
                         "scisql_nanojanskyToAbMag(i_calibFlux) as i_calibMag, "
                         "scisql_nanojanskyToAbMagSigma(g_calibFlux, g_calibFluxErr) as g_calibMagErr "
                         "FROM dp02_dc2_catalogs.Object "
                         "WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), "
                         "CIRCLE('ICRS', "+use_center_coords+", 1.0)) = 1 "
                         "AND detect_isPrimary = 1 "
                         "AND g_calibFlux > 360 "
                         "AND r_calibFlux > 360 "
                         "AND i_calibFlux > 360 "
                         "AND g_extendedness = 0 "
                         "AND r_extendedness = 0 "
                         "AND i_extendedness = 0",
                         maxrec=10000)

4.2. Store the data as a pandas dataframe. 

.. code-block::
    
    results_table = results.to_table()
    data = results_table.to_pandas()



.. _DP0-2-Cmndline-Beginner-Step-5:

Step 5. Make a color-magnitude diagram
======================================

5.1. Plot the color (r-i magnitudes) vs g magnitude.

.. code-block::

    plt.plot(data['r_calibMag'].values - data['i_calibMag'].values,
         data['g_calibMag'].values, 'o', ms=2, alpha=0.2)
	 
5.2. Define the axis labels and limits.

.. code-block::

    plt.xlabel('mag_r - mag_i', fontsize=16)
    plt.ylabel('mag_g', fontsize=16)
    plt.xticks(fontsize=16)
    plt.yticks(fontsize=16)

    plt.xlim([-0.5, 2.0])
    plt.ylim([25.5, 16.5])

5.3. Save the plot as a pdf.

.. code-block::

    plt.savefig('color-magnitude.pdf')

Use the file navigator on the left-hand side of the Notebook Aspect to navigate to the file "color-magnitude.pdf".
Double click on the filename to open and view the plot.
    
.. figure:: /_static/cl_color-magnitude.jpg
	:alt: Color-magnitude diagram plotting magnitude g on the y-axis and magnitude r minus magnitude i color on the x-axis.  
		There are a number of vertical bands representing various color magnitudes ranging from 0.6 to 1.7.  This feature is unique to this simulated data set. 


.. _DP0-2-Cmndline-Beginner-Step-6:

Step 6. Retrieve image data using the butler
============================================

The two most common types of images that DP0 delegates will interact with are calexps and deepCoadds.

calexp: A single image in a single filter.

deepCoadd: A combination of single images into a deep stack or Coadd.

The LSST Science Pipelines processes and stores images in tracts and patches. To retrieve and display an image at a desired coordinate, users have to specify their image type, tract, and patch.

tract: A portion of sky within the LSST all-sky tessellation (sky map); divided into patches.

patch: A quadrilateral sub-region of a tract, of a size that fits easily into memory on desktop computers.

The butler (`butler documentation <https://pipelines.lsst.io/modules/lsst.daf.butler/index.html>`_) is an LSST Science Pipelines software package to fetch LSST data without having to know its location or format. The butler can also be used to explore and discover what data exists. Other tutorials demonstrate the full butler functionality.

6.1. Define a butler configuration and collection.

.. code-block::

    butler = dafButler.Butler('dp02', collections='2.2i/runs/DP0.2')

6.2. Define the coordinates of a known galaxy cluster in the DC2. 

.. code-block::

    my_ra_deg = 55.745834
    my_dec_deg = -32.269167

6.3. Use lsst.geom to define a SpherePoint for the cluster's coordinates (`lsst.geom documentation <https://pipelines.lsst.io/modules/lsst.geom/index.html>`_).

.. code-block::

    my_spherePoint = lsst.geom.SpherePoint(my_ra_deg*lsst.geom.degrees, my_dec_deg*lsst.geom.degrees)
    print(my_spherePoint)

6.3. Retrieve the DC2 skymap (`skymap documentation <https://pipelines.lsst.io/modules/lsst.skymap/index.html>`_) and identify the tract and patch.

.. code-block::

    skymap = butler.get('skyMap')
    tract = skymap.findTract(my_spherePoint)
    patch = tract.findPatch(my_spherePoint)

    my_tract = tract.tract_id
    my_patch = patch.getSequentialIndex()

    print('my_tract: ', my_tract)
    print('my_patch: ', my_patch)

6.4. Retrieve the deep i-band Coadd.

.. code-block::

    dataId = {'band': 'i', 'tract': my_tract, 'patch': my_patch}
    my_deepCoadd = butler.get('deepCoadd', dataId=dataId)


.. _DP0-2-Cmndline-Beginner-Step-7:

Step 7. Display the image
=========================

Image data retrieved with the butler can be displayed several different ways.

7.1. Display the image using afwDisplay (`afwDisplay documentation <https://pipelines.lsst.io/modules/lsst.afw.display/index.html>`_).

.. code-block::

    afwDisplay.setDefaultBackend('matplotlib')

.. code-block::
    
    fig = plt.figure(figsize=(10, 8))
    afw_display = afwDisplay.Display(1)
    afw_display.scale('asinh', 'zscale')
    afw_display.mtv(my_deepCoadd.image)
    plt.gca().axis('on')
    plt.savefig('my_deepCoadd.pdf')
    
Use the file navigator on the left-hand side of the Notebook Aspect to navigate to the file "my_deepCoadd.pdf".
Double click on the filename to open and view the image.
    
.. figure:: /_static/cl_my-deep-Coadd.jpg
	:alt: A four thousand by four thousand pixel screen capture of an astronomical image that has been plotted in a Jupyter notebook.  
		A large concentration of elongated points is concentrated at the lower-left quadrant and suggests a cluster of galaxies.  
    
7.2. Display the image using Firefly (`Firefly documentation <https://pipelines.lsst.io/modules/lsst.display.firefly/index.html>`_).

.. code-block::

    afwDisplay.setDefaultBackend('firefly')
    afw_display = afwDisplay.Display(frame=1)
    afw_display.mtv(my_deepCoadd)
   
Optional: For a demonstration of the Firefly interactive interface, work through "03b Image Display with Firefly" of the :ref:`DP0-2-Tutorials-Notebooks`.

7.3. When you're done, exit python to return to the regular command line.

.. code-block::

    exit()

