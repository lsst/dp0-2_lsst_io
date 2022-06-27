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

The API's services for DP0.2 will include TAP, OBSTAP, SODA (image cutouts and mosaics), and HiPS (all acronyms to be defined here in future updates).

Longer term, Rubin Observatory will support SCS for simple catalog searches, SIAv2 for image searches, and VOSpace (in addition to WebDAV) for access to user files.


.. _Data-Access-Analysis-Tools-TAP-TOPCAT:


Use of TOPCAT with the RSP TAP service
======================================

One popular and useful TAP utility is `TOPCAT <http://www.star.bris.ac.uk/~mbt/topcat/>`_.

To access DP0.2 from the TAP utility, one needs to have an RSP access token.
How to generate and use an RSP access token is described by the `Rubin Science Platform APIs <https://data-int.lsst.cloud/api-aspect>`_ webpage and
by the `Science Platform Tokens <https://nb.lsst.io/environment/tokens.html>`_ webpage.

A step-by-step API tutorial like the one available in `this Rubin Community Forum post <https://community.lsst.org/t/will-there-be-external-tap-access-to-rsp-dp0-2-tables/6660/7>`_ will be added here soon.

In the meantime these two slides from a talk by Leanne Guy, `Rubin Science Platform – what to expect
<https://docushare.lsstcorp.org/docushare/dsweb/Get/presentation-1694/PST-SC%20-%20Rubin%20Science%20Platform%20-%20LeanneGuy%20-%2020220413.pdf>`_,
illustrates what users can expect in terms of the RSP's API Aspect.

.. figure:: /_static/API_LGuy_slide11.png
    :name: API_LGuy_slide11

.. figure:: /_static/API_LGuy_slide12.png
    :name: API_LGuy_slide12


.. _Data-Access-Analysis-Tools-TAP:

The Table Access Protocol (TAP) service
=======================================

Use of the TAP service to query catalogs via the Portal is described in :doc:`/data-access-analysis-tools/portal-intro`.

In the Notebook Aspect, a TAP service is instantiated in a python notebook and used to execute an `ADQL query <https://www.ivoa.net/documents/ADQL/>`_ and return a result set.
A set of utilities are provided to get a TAP service instance.

.. code-block:: python

   from rubin_jupyter_utils.lab.notebook import get_tap_service, retrieve_query
   service = get_tap_service()
   query = "SELECT TOP 100 * FROM dp02_dc2_catalogs.Object"
   results = service.search(query)
   results.to_table().show_in_notebook()

Several of the DP0 :ref:`DP0-2-Tutorials-Notebooks` demonstrate how to use the TAP service programmatically from a python notebook.
