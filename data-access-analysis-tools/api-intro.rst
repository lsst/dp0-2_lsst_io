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

.. Important:
    The API Aspect has a lot of new features for DP0.2, which will eventually be added to this page.
    Check back soon for new information!

**(Is this true?  I don't know anything about the ObsTAP, SODA, or HiPS services.)** 
The API's services for DP0.2 include `TAP <https://www.ivoa.net/documents/TAP/20190927/index.html>`_, 
`ObsTAP <https://www.ivoa.net/documents/ObsCore/>`_, `SODA <https://www.ivoa.net/documents/SODA/20170517/index.html>`_ 
(image cutouts and mosaics), and `HiPS <https://aladin.u-strasbg.fr/hips/>`_.  
Currently, CST support for the RSP API services beyond TAP is limited, but more support will be available later.

Longer term, Rubin Observatory will support `SCS <https://www.ivoa.net/documents/latest/ConeSearch.html>`_ for simple catalog searches, 
`SIAv2 <https://www.ivoa.net/documents/SIA/20150730/index.html>`_ for image searches, and `VOSpace <https://www.ivoa.net/documents/VOSpace/>`_ 
(in addition to `WebDAV <https://en.wikipedia.org/wiki/WebDAV>`_) for access to user files.


.. _Data-Access-Analysis-Tools-TAP-NB:

Use of TAP via the RSP Notebook Aspect
======================================

The primary means of accessing TAP is via the RSP's Portal and Notebook aspects.

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



.. _Data-Access-Analysis-Tools-TAP-TOPCAT:

Use of TOPCAT with the RSP TAP service
======================================

One popular and useful non-RSP TAP utility is `TOPCAT <http://www.star.bris.ac.uk/~mbt/topcat/>`_.

To access DP0.2 from a non-RSP TAP utility, one needs to generate an RSP access token.
How to generate and use an RSP access token is described by the `Rubin Science Platform APIs <https://data.lsst.cloud/api-aspect>`_ webpage and
by the `Science Platform Tokens <https://nb.lsst.io/environment/tokens.html>`_ webpage.

A TOPCAT-based Step-by-Step Guide
---------------------------------

0. Create an RSP access token as described above.  (See the `Creating user tokens webpage 
   <https://rsp.lsst.io/guides/auth/creating-user-tokens.html>`_ for a step-by-step guide 
   for creating an RSP access token.  It is recommended that the token you create has the
   following propoerties:  a name that includes "TOPCAT" as a substring, a scope of `read:tap`, 
   and no expiration date.)  It is highly recommended to cut-and-paste the token somewhere
   for future reference.
  
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


.. _Data-Access-Analysis-Tools-TAP-NB-NOIRLAB:

Use of the NOIRlab Data Lab with the RSP TAP service
====================================================

One may wish to access the rubin data from outside the RSP environment.
One way to do this is via the ``pyvo`` python module.
As with the TOPCAT example above, to do this one needs to generate an RSP access token.
For simplicity, the token generated above for the TOPCAT example can be used here as well.
Here, as an example, we make use of the NOIRlab Astro Data Lab.

** See K.-T. Lim's reply and Michael Wood-Vasey's ``test_rsp_tap_service.py`` from 
https://community.lsst.org/t/will-there-be-external-tap-access-to-rsp-dp0-2-tables/6660/7 **

A NOIRlab Astro Data Lab-based Step-by-Step Guide
-------------------------------------------------

1. Go to the NOIRLAB DataLab ( https://datalab.noirlab.edu/ ) and launch a Jupyter Notebook.

2. At the very minimum, import the ``pyvo`` python module::

	import pyvo

3. Define the data.lsst.cloud TAP server URL and your security token::

	RSP_TAP_SERVICE = "https://data.lsst.cloud/api/tap"
	#tap_url = 'https://data.lsst.cloud/api/tap'
	# having the token in your code is poor security.
	# See Michael Wood-Vasey's solution below.
	#token = 'yy-xxxxxx'   # insert your own RSP TAP server security token here.

4. Set up appropriate authorization to access the RSP TAP server::

	cred = pyvo.auth.CredentialStore()
	token_file = "read_tap.token"
	with open(token_file, "r") as f:
    		token_str = f.readline()
	cred.set_password("x-oauth-basic", token_str)
	credential = cred.get("ivo://ivoa.net/sso#BasicAA")
	rsp_tap = pyvo.dal.TAPService(RSP_TAP_SERVICE, credential)

5. Run a query::

	query = "SELECT * FROM tap_schema.schemas"
	results = rsp_tap.run_sync(query)
	results.to_table()


