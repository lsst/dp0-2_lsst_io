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

###########################
01. Command Line (beginner)
###########################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Gloria Fonseca Alvarez

**Last verified to run:** 

**Targeted learning level:** Beginner

**Introduction:** This tutorial is an introduction to the terminal and command line functionality within the Rubin Science Platform. It is parallel to the 
                  Jupyter Notebook tutorial "Introduction to DP02"

.. _DP0-2-Cmndline-Beginner-Step-1:

Step 1. Access the terminal
==========================

1.1. Log in to the Notebook Aspect.
1.2. In the launcher window under "Other", select the terminal

.. figure:: /_static/other_terminal.png

1.3. Start an interactive python session

.. _DP0-2-Cmndline-Beginner-Step-2:

Step 2. Import packages
==========================
2.1. Import general packages

.. code-block::

    import numpy
    import matplotlib
    import matplotlib.pyplot as plt

2.2. Import packages for Section 2.0 Catalog Accessing

.. code-block::

    import pandas 
    pandas.set_option('display.max_rows', 1000)
    from lsst.rsp import get_tap_service, retrieve_query

2.3. Import packages for Section 3.0 Image Accessing

.. code-block::

    import lsst.daf.butler as dafButler
    import lsst.geom
    import lsst.afw.display as afwDisplay

Step 3. Explore catalog tables and columns using TAP
==========================

3.1. Start the TAP service 

.. code-block::

    service = get_tap_service()

3.2. Exercise 1

Retrieve and display a list of all the table names and descriptions that are available via the TAP server.

.. code-block::

    my_adql_query = "SELECT description, table_name FROM TAP_SCHEMA.tables"
    results = service.search(my_adql_query)
    results_table = results.to_table().to_pandas()
    results_table

Optionally, save the table results to a text file

3.3. Exercise 2

Retrieve and display a list of column names in the DP0.2 Object catalog. 

.. code-block::

 my_adql_query = "SELECT * from TAP_SCHEMA.columns WHERE table_name = 'dp02_dc2_catalogs.Object'"
 res = service.search(my_adql_query)
 print(res.fieldnames)

3.4. Exercise 3

Retrieve and display column names, data types, description, and units for all columns in the DP0.2 Object Catalog

.. code-block::

 my_adql_query = "SELECT column_name, datatype, description, unit FROM TAP_SCHEMA.columns WHERE table_name = 'dp02_dc2_catalogs.Object'"
 results = service.search(my_adql_query)
 results_table = results.to_table().to_pandas()
 print('Number of columns available in the Object catalog: ', len(results_table))

Only display names and description for columns that contain the string 'cModelFlux'.

.. code-block::
    
    my_string = 'cModelFlux'
    for col,des in zip(results_table['column_name'],results_table['description']):
        if col.find(my_string) > -1:
            print('%-40s %-200s' % (col,des))

Note about for loops and indentation on interactive python

Step 4. Retrieve data using TAP
==========================

4.1 Retrieve 10 objects of any kind

Retrieve the coordinates and g, r, i magnitudes for 10 objects within 0.5 degrees of the center coordinates 62, -37

.. code-block::

    use_center_coords = "62, -37"

Create a new my_adql_query

.. code-block:: 
     my_adql_query = "SELECT coord_ra, coord_dec, detect_isPrimary, " 
                     "r_calibFlux, r_cModelFlux, r_extendedness " 
                     "FROM dp02_dc2_catalogs.Object "
                     "WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), "
                     "CIRCLE('ICRS', " + use_center_coords + ", 0.5)) = 1 "

    results = service.search(my_adql_query, maxrec=10)
    results_table = results.to_table()

4.2 Convert fluxes into magnitudes

.. code-block::
   
     results_table['r_calibMag'] = -2.50 * numpy.log10(results_table['r_calibFlux']) + 31.4
     results_table['r_cModelMag'] = -2.50 * numpy.log10(results_table['r_cModelFlux']) + 31.4

Print results

.. code-block::

    results

4.2 Retrieve 10,000 point-like objects

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
    results_table = results.to_table()
    print(len(results_table))

4.3 Save the data as a pandas dataframe 

.. code-block::
    data = results_table.to_pandas()


Step 5. Make a color-magnitude diagram
==========================

5.1 Plot magnitudes

.. code-block::
    plt.plot(data['r_calibMag'].values - data['i_calibMag'].values,
         data['g_calibMag'].values, 'o', ms=2, alpha=0.2)

    plt.xlabel('mag_r - mag_i', fontsize=16)
    plt.ylabel('mag_g', fontsize=16)
    plt.xticks(fontsize=16)
    plt.yticks(fontsize=16)

    plt.xlim([-0.5, 2.0])
    plt.ylim([25.5, 16.5])

5.2 Save figure

.. code-block::
    plt.savefig('color-magnitude.pdf')

Step 6. Retrieve image data using the butler
==========================

6.1 Create an instance of the butler

Define Butler configuration and collection 

.. code-block::
    config = 'dp02'
    collection = '2.2i/runs/DP0.2'
    butler = dafButler.Butler(config, collections=collection)

6.2 Identify and retrieve a deepCoadd

.. code-block::
    my_ra_deg = 55.745834
    my_dec_deg = -32.269167

    my_spherePoint = lsst.geom.SpherePoint(my_ra_deg*lsst.geom.degrees, my_dec_deg*lsst.geom.degrees)
    print(my_spherePoint)

6.3 Retrive the DC2 skymap and identify the tract and patch

.. code-block::
    skymap = butler.get('skyMap')
    tract = skymap.findTract(my_spherePoint)
    patch = tract.findPatch(my_spherePoint)

    my_tract = tract.tract_id
    my_patch = patch.getSequentialIndex()

    print('my_tract: ', my_tract)
    print('my_patch: ', my_patch)

6.4 Retrieve the deep i-band Coadd 

.. code-block::
    dataId = {'band': 'i', 'tract': my_tract, 'patch': my_patch}
    my_deepCoadd = butler.get('deepCoadd', dataId=dataId)

6.5 Display the image with afwDisplay

.. code-block::
    afwDisplay.setDefaultBackend('matplotlib')

.. code-block::
    fig = plt.figure(figsize=(10, 8))
    afw_display = afwDisplay.Display(1)
    afw_display.scale('asinh', 'zscale')
    afw_display.mtv(my_deepCoadd.image)
    plt.gca().axis('on')
    plt.savefig('image.pdf')