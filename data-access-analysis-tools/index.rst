.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
    - If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

##############################
Data Access and Analysis Tools
##############################

.. This section should provide a brief, top-level description of the page.

The **Rubin Science Platform (RSP)** is the set of integrated web-based applications, services, and tools to query, visualize, subset, and analyze LSST data.

Throughout DP0 the RSP will be in active development by Rubin Observatory staff, with access provided to science community members on a shared-risk basis.

See `Rubin Science Platform Documentation <https://data.lsst.cloud/docs>`_ page for additional information.

Note that the contents of this page address the current, DP0-era functionality.
Use of the DP0-era RSP comes with some risks and responsibilities, as described below.
Scroll down to the bottom of this page for more information about the future RSP functionality.


.. _Data-Access-Analysis-Tools-RSP:

Rubin Science Platform (RSP)
============================

The Rubin Science Platform (RSP) provides access to Rubin Observatory data products via three aspects: 
Portal, Notebooks, and API (Application Programming Interface).
All three aspects enable users to query, retrieve, and visualize the image and catalog data, but in different ways, 
and with different analysis options.

The :ref:`Tools-RSP-Portal` provides a GUI (graphical user interface) that enables access and visualization without 
ADQL (Astronomical Data Query Language) or python, 
however, analysis tools such as trend regression are not available.
The :ref:`Tools-RSP-Notebook` enables programmatic analysis of the data products in a python environment that includes the 
LSST Science Pipelines and common packages like numpy, scipy, bokeh, and datashader.
The :ref:`Tools-RSP-API` offers remote access via Virtual Observatory (VO) interfaces such as TOPCAT (Tool for OPerations on Catalogues And Tables).

**Still unsure which aspect to choose?** 
Read on below for more details of what is possible with each of the RSP's three aspects, or
try working through the introductory Portal and Notebook :doc:`DP0.2 tutorials </tutorials-examples/index>`.


.. figure:: /_static/RSP_home.png
    :name: RSP_home
    :alt: Screenshot of the rubin science platform login screen.  Image has a menu on the top for the user to select the portal, notebooks, api, documentation, or community forum.
        The center of the image shows three panels to allow the user to select the portal, notebook, or API apsects.

    Screenshot of the `data.lsst.cloud <https://data.lsst.cloud/>`_ dashboard.
    Enter an aspect using the top menu bar or by clicking on the icon.


.. _Data-Access-Analysis-Tools-Warnings:

RSP usage: risks and responsibilities
-------------------------------------

**All RSP users are responsible for being aware of the risks inherent in using software in active development, and must familiarize themselves with these risks.**

.. toctree::
    :maxdepth: 2
    :glob:

    rsp-warnings


.. _Tools-RSP-Portal:

Portal Aspect
-------------

The Portal Aspect of the RSP provides an environment for data discovery, query, filtering, and visualization.
Note that the Portal Aspect is expected to evolve significantly before the first LSST data release.

.. toctree::
    :maxdepth: 2
    :glob:

    portal-intro


.. _Tools-RSP-Notebook:

Notebook Aspect
---------------

The Notebook Aspect of the RSP provides Python-based access to DP0.2 data products via a custom implementation of web-based JupyterLab Notebooks (`JupyterLab documentation <https://jupyterlab.readthedocs.io/en/stable/index.html>`_), as well as a command-line interface.

Within the RSP Notebook Aspect users can query and retrieve data sets, manipulate and display images, calculate derived properties, plot results, reprocess data with the `LSST Science Pipelines <https://pipelines.lsst.io>`_, and most other analyses you can imagine performing with Python on astronomical images and catalogs.

A stable software environment is provided and maintained for users, which includes many commonly-used packages and the `LSST Science Pipelines <https://pipelines.lsst.io>`__.
For DP0, this environment will only support Python 3.
To view a list of packages available to you in the Notebook Aspect of the RSP, type ``pip list`` in a terminal.

.. toctree::
    :maxdepth: 2
    :glob:

    nb-intro

.. _Tools-RSP-API:

API Aspect
----------

The API (Application Programming Interface) Aspect of the RSP enables programmatic access to the Rubin data products via Virtual Observatory (VO) interfaces.
Users will be able to remotely access the LSST data and `Data Access Center <https://www.lsst.org/about/dm/facilities>`_ (DAC) services using tools they’re already familiar with,
e.g. `TOPCAT <http://www.star.bris.ac.uk/~mbt/topcat/>`__ or libraries such as `Astropy <https://www.astropy.org>`__.
The Portal and Notebook Aspects of the RSP make use of the same APIs to internally access the LSST datasets.

The API Aspect of the RSP is very powerful and will eventually allow for federation with other astronomical archives, bringing added value to the LSST dataset.

.. toctree::
    :maxdepth: 2
    :glob:

    api-intro



.. _Tools-ADQL-Recipes:

ADQL Recipes
------------

.. toctree::
    :maxdepth: 2
    :glob:

    adql-recipes


.. _Tools-Python-Functions:

Python Functions
----------------

.. toctree::
    :maxdepth: 2
    :glob:

    python-functions




.. _Data-Access-Analysis-Tools-Data-Processing:

Data processing tools
=====================

Documentation for the LSST Science Pipelines, a software package which is available to all RSP users via the Notebook Aspect, can be found at `pipelines.lsst.io <https://pipelines.lsst.io>`_.

A brief summary of how the LSST Science Pipelines were used to create the DP0.2 data products can be found in this :doc:`/data-products-dp0-2/data-processing`.



.. _Data-Access-Analysis-Tools-Future:

RSP Future Functionality
========================

During DP0, the RSP has limited functionality (see :ref:`Data-Access-Analysis-Tools-Warnings`) compared to the Operations-era RSP
as described in the RSP Vision Document, `LSE-319 <https://ls.st/lse-319>`_.

For example, during Rubin Observatory Operations, the RSP will feature more tools in the Application Programming Interface (API) aspect than are described above, 
and more options for using the Portal and Notebook aspects in tandem.

See the following FAQ (and references therein) for more details on the future functionality of the RSP.


.. toctree::
    :maxdepth: 2
    :glob:

    rsp-future-faq

.. toctree::
    :maxdepth: 2
    :glob:

    portal-future-faq
