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

Step 1. Accessing the terminal
==========================

1.1. Log in to the Notebook Aspect.
1.2. In the launcher window under "Other", select the terminal

.. figure:: /_static/other_terminal.png

1.3. Start an interactive python session

.. _DP0-2-Cmndline-Beginner-Step-2:

Step 2. Package imports
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

