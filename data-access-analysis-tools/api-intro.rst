.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-API-Intro:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

##################################
Introduction to the RSP API Aspect
##################################

.. This section should provide a brief, top-level description of the page.

On the the main landing page at `data.lsst.cloud <https://data.lsst.cloud>`_ there is an "APIs" panel with more information about the API Aspect.

.. Important::
    The API Aspect has a lot of new features for DP0.2, which will be added to this page after the DP0.2 release (during July 2022).
    Check back soon for new information!

The API's services for DP0.2 will include `TAP <https://www.ivoa.net/documents/TAP/20190927/index.html>`_, `ObsTAP <https://www.ivoa.net/documents/ObsCore/>`_, `SODA <https://www.ivoa.net/documents/SODA/20170517/index.html>`_ (image cutouts and mosaics), and `HiPS <https://aladin.u-strasbg.fr/hips/>`_.

Longer term, Rubin Observatory will support `SCS <https://www.ivoa.net/documents/latest/ConeSearch.html>`_ for simple catalog searches, `SIAv2 <https://www.ivoa.net/documents/SIA/20150730/index.html>`_ for image searches, and `VOSpace <https://www.ivoa.net/documents/VOSpace/>`_ (in addition to `WebDAV <https://en.wikipedia.org/wiki/WebDAV>`_) for access to user files.


.. _Data-Access-Analysis-Tools-TAP-TOPCAT:


Use of TOPCAT with the RSP TAP service
======================================

One popular and useful TAP utility is `TOPCAT <http://www.star.bris.ac.uk/~mbt/topcat/>`_.

To access DP0.2 from the TAP utility, one needs to have an RSP access token.
How to generate and use an RSP access token is described by the `Rubin Science Platform APIs <https://data-int.lsst.cloud/api-aspect>`_ webpage and
by the `Science Platform Tokens <https://nb.lsst.io/environment/tokens.html>`_ webpage.

A TOPCAT-based Step-by-Step Guide
---------------------------------

1. Start up TOPCAT (see `TOPCAT homepage <http://www.star.bris.ac.uk/~mbt/topcat/>`_).

2. Click on "Table Access Protocal (TAP) Query" under the “VO” menu.

.. figure:: /_static/API_TOPCAT_DLT_1.png
    :name: API_TOPCAT_DLT_1
    :alt: TBD

3.  Fill in `https://data.lsst.cloud/api/tap` in the “TAP URL” window and click the “Use Service” button.

.. figure:: /_static/API_TOPCAT_DLT_2.png
    :name: API_TOPCAT_DLT_2
    :alt: TBD

4. Fill in your security token under “User” in the Authentication window that pops up. Leave the “Password” blank. Click OK.

.. figure:: /_static/API_TOPCAT_DLT_3.png
    :name: API_TOPCAT_DLT_3
    :alt: TBD

5. Now you have access to the RSP TAP service from TOPCAT.

.. figure:: /_static/API_TOPCAT_DLT_4.png
    :name: API_TOPCAT_DLT_4
    :alt: TBD




.. _Data-Access-Analysis-Tools-TAP-NB:

Use of TAP via the Notebook Aspect
==================================

Use of the TAP service to query catalogs via the Portal is described in :doc:`/data-access-analysis-tools/portal-intro`.

In the Notebook Aspect, a TAP service is instantiated in a python notebook and used to execute an `ADQL query <https://www.ivoa.net/documents/ADQL/>`_ and return a result set.
A set of utilities are provided to get a TAP service instance.

.. code-block:: python

   from lsst.rsp import get_tap_service, retrieve_query
   service = get_tap_service()
   query = "SELECT TOP 100 * FROM dp02_dc2_catalogs.Object"
   results = service.search(query)
   results.to_table().show_in_notebook()

Several of the DP0 :ref:`DP0-2-Tutorials-Notebooks` demonstrate how to use the TAP service programmatically from a python notebook.
