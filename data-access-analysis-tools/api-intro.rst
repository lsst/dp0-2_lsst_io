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

On the the main landing page at `data.lsst.cloud <https://data.lsst.cloud>`_ there is an "APIs" panel with more information on the API Aspect.
API stands for Application Programming Interface.
An API is, essentially, code that permits two other programs (applications) to communicate with each other.
If it helps, think of it as a request-and-response (or a client-server) situation:
one program (a client) requests something (data) and the other (a server) responds.

The API's services for DP0.2 include `TAP <https://www.ivoa.net/documents/TAP/20190927/index.html>`_, 
`ObsTAP <https://www.ivoa.net/documents/ObsCore/>`_, `SODA <https://www.ivoa.net/documents/SODA/20170517/index.html>`_ 
(image cutouts and mosaics), and `HiPS <https://aladin.u-strasbg.fr/hips/>`_.  
Currently, Rubin Community Science Team (CST) support for the RSP API services beyond TAP is limited, but more support will become available soon.
For the time being, this page will focus on the API's TAP services.

Longer term, Rubin Observatory will support `SCS <https://www.ivoa.net/documents/latest/ConeSearch.html>`_ for simple catalog searches, 
`SIAv2 <https://www.ivoa.net/documents/SIA/20150730/index.html>`_ for image searches, and `VOSpace <https://www.ivoa.net/documents/VOSpace/>`_ 
(in addition to `WebDAV <https://en.wikipedia.org/wiki/WebDAV>`_) for access to user files.

As described below, the API aspect permits Rubin data access both from inside the RSP environment (e.g., via the RSP notebook aspect) and 
from outside the RSP environment (e.g., via `TOPCAT <http://www.star.bris.ac.uk/~mbt/topcat/>`_ or from a ``pyvo``-enabled environment like 
NOIRLab's `Astro Data Lab <https://datalab.noirlab.edu/>`_).  

Currently, there are no additional database constraints imposed on external environments.  
As for the internal RSP enviroment, the database server will generally be unable to process queries that have an internal intermediate form 
that is larger than roughly 5GB, and the TAP service will have difficulties with final results that are over roughly 2GB in size.  
That said, this is by no means the final word on what limits might be in operations.


.. Important::
    The API Aspect has a lot of new features for DP0.2, which will eventually be added to this page.
    Check back soon for new information!


.. _Data-Access-Analysis-Tools-TAP-NB:

Use of TAP via the RSP Notebook Aspect
======================================

The primary means of accessing TAP is via the RSP's Portal and Notebook aspects.

Use of the TAP service to query catalogs via the Portal is described in :doc:`/data-access-analysis-tools/portal-intro`.

In the Notebook Aspect, a TAP service is instantiated in a python notebook and used to execute an `ADQL query <https://www.ivoa.net/documents/ADQL/>`_ and return a result set.
Within the RSP's Notebook Aspect, a set of utilities are provided to get a TAP service instance.

.. code-block:: python

    from lsst.rsp import get_tap_service, retrieve_query
    service = get_tap_service("tap")
    query = "SELECT TOP 100 * FROM dp02_dc2_catalogs.Object"
    results = service.search(query)
    results.to_table()

Several of the DP0 :ref:`DP0-2-Tutorials-Notebooks` demonstrate how to use the TAP service programmatically from a python notebook. 



.. _Data-Access-Analysis-Tools-TAP-TOPCAT:

Use of TOPCAT with the RSP TAP service
======================================

One popular and useful non-RSP utility that supports the TAP API is 
`TOPCAT <http://www.star.bris.ac.uk/~mbt/topcat/>`_.  With TOPCAT, 
it is possible to run ADQL queries on the Rubin DP0.2 data set, 
explore tables, and make a variety of 2D and 3D plots via an 
interactive graphical users interface (GUI).  (For a broader view 
of TOPCAT capabilities, please see the 
`TOPCAT webpage <http://www.star.bris.ac.uk/~mbt/topcat/>`_,
which includes documentation, examples, and tutorials.)

To access DP0.2 from a non-RSP TAP utility like TOPCAT, an RSP access token needs to be generated.
How to generate and use an RSP access token is described by the 
`Rubin Science Platform APIs <https://data.lsst.cloud/api-aspect>`_ webpage and
by the `Science Platform Tokens <https://nb.lsst.io/environment/tokens.html>`_ webpage.

.. Important::
    **Note that tokens should be treated like passwords:  they should not be shared with others.  
    Take precautions to keep tokens secure.  Never store tokens in git-tracked files.**

.. _Data-Access-Analysis-Tools-TAP-TOPCAT-get-started:

Get started with TOPCAT
-----------------------

This section provides a basic guide to get TOPCAT set up to explore the DP0.2 tables.

**1. Create an RSP access token.**  
See the `Creating user tokens webpage <https://rsp.lsst.io/guides/auth/creating-user-tokens.html>`_ 
for a step-by-step guide for creating an RSP access token.  It is recommended that the token you create has the
following propoerties:  a name that includes "TOPCAT" as a substring, a scope of ``read:tap``, 
and no expiration date.) The token will only be visible once.
*You must cut-and-paste the token to a secure file for future use.*
A new token is not needed for every TOPCAT session; the token can be reused, but it must be kept secure.
  
**2. Start up TOPCAT on your own computer.**
See `TOPCAT homepage <http://www.star.bris.ac.uk/~mbt/topcat/>`_ for download and install instructions.

**3. Click on "Table Access Protocol (TAP) Query" under the “VO” menu.**
This will open up a separate Table Access Protocol (TAP) Query window. 

.. figure:: /_static/API_TOPCAT_DLT_1.png
    :name: API_TOPCAT_DLT_1
    :alt: A screenshot of the main TOPCAT window with the Table Access Protocol item 
	  highlighted by the cursor under the VO drop-down menu.

    The main TOPCAT window, with the "VO" menu pulled down and the "Table Access Protocol (TAP) Query" highlighted.

**4. Fill in the relevant in the “TAP URL” window and click the “Use Service” button in the Table Access Protocol (TAP) Query window.**
For DP0.2, use ``https://data.lsst.cloud/api/tap``.  If you wish to access DP0.3 -- which 
is a database of solar system objects that supplements the main DP0.2 database -- use 
``https://data.lsst.cloud/api/ssotap`` instead.

.. figure:: /_static/API_TOPCAT_DLT_2.png
    :name: API_TOPCAT_DLT_2
    :alt: A screenshot of the the Table Access Protocol (TAP) Query window in which the value
          for the TAP URL has been filled in with the URL
	  https://data.lsst.cloud/api/tap .  A blue oval indicates the location of the 
          Selected TAP Service panel in the window.

    The Table Access Protocol (TAP) Query window with the location of the "Selected TAP Service" panel indicated by a blue oval.

**5. Populate the Authentication window that pops up.**  
Fill in ``x-oauth-basic`` for the "User" and your security token forthe "Password" and click "OK".

.. figure:: /_static/API_TOPCAT_DLT_3.png
    :name: API_TOPCAT_DLT_3
    :alt: A screenshot of the Authentication window. The user has been filled in with a value of x-oauth-basic, 
	  and the password is shown (for security purposes) as a series of filled black circles.

    The Authentication window with the values for the user and the password filled in.

**6. Note that the RSP TAP service is now accessible from your instance of TOPCAT.**  
An indicator that the service is now accessible is that a list of DP0.1 and DP0.2 tables available has appeared in the Metadata panel of the TAP Query window.

.. figure:: /_static/API_TOPCAT_DLT_4.png
    :name: API_TOPCAT_DLT_4
    :alt: A screenshot of the Table Access Protocol (TAP) Query window.
          The Table Access Protocol (TAP) Query window now shows three panels, stacked vertically.  The
	  top panel is the Metadata panel, and it shows a list of DP0.1 and DP0.2 schemas and tables that
	  are available to query.  The middle panel is the Service Capabilities panel, and it shows that
	  the available Query Language is ADQL-2.0.  The bottom panel is the ADQL Text panel, and it 
	  indicates the current Mode is Synchronous; the bottom panels text box is currently empty.

    The Table Access Protocol (TAP) Query window; a list of DP0.1 and DP0.2 tables 
    available for query can be be seen in the Metadata panel.

**7. Explore.**
At this stage, the Rubin DP0.2 data set can be explored via TOPCAT.  For an example, see the 
:doc:`/tutorials-examples/api-topcat-beginner`.

.. _Data-Access-Analysis-Tools-TAP-pyvo:

Use of pyvo with the RSP TAP service
====================================

Another way to access the Rubin data from outside the RSP environment is via the 
`pyvo <https://pyvo.readthedocs.io/en/latest/>`_ python module, an affiliated
`astropy <https://www.astropy.org/>`_ package for `providing access to remote data
and services of the Virtual Observatory using python <https://github.com/astropy/pyvo>`_.    
By this method, if ``pyvo`` is installed, one can access the RSP TAP service directly from one's own laptop.
If not, one can access the RSP TAP service from other freely accessible services 
that have ``pyvo`` pre-installed (like, e.g., NOIRLab's 
`Astro Data Lab <https://datalab.noirlab.edu/>`_ Jupyter Notebook server).


.. Important::
    **Recall that tokens should be treated like passwords:  they should not be shared with others.  
    Take precautions to keep tokens secure.  Never store tokens in git-tracked files.**


.. _Data-Access-Analysis-Tools-TAP-pyvo-get-started:

Get started with pyvo
---------------------

This section provides a basic guide to provide access to the DP0.2
TAP service via python code on your own computer or on an online service like NOIRLab's 
`Astro Data Lab <https://datalab.noirlab.edu/>`_ Jupyter Notebook server.  

**1. Copy an RSP access token into a file in your home directory.**
As with the TOPCAT example above, one needs an RSP access token.  
Either generate one as described above in :ref:`Data-Access-Analysis-Tools-TAP-TOPCAT`, 
or just use a previously generated (but unexpired) RSP access token.
Ideally, copy the RSP access token into a file in your home directory
that is only read/write accessible by the file owner and that is accessible to 
the python session that will be accessed in the steps below.  Specifically, 
in a UNIX/MacOS/Linux environment, the following commands can be performed
in order to create this file in a secure manner that avoids exposing the
RSP token to outside resources for even a short period of time.

* Open a terminal window (**not** a Jupyter notebook) on your computer or in your non-RSP user environoment.

* Change directory to the home directory.

.. code-block:: python

   cd ~

* In the home directory, create an empty file that will eventually contain the RSP token.  One can do this via the ``touch`` command.  Note that using a 'hidden' file -- one with a name that starts with a ``.`` -- improves security.

.. code-block:: python

   touch .rsp-tap.token

* Change the permissions on this file to remove world and group read/write access.  The ``chmod 600`` command will do this while maintaining read/write access for the file owner.

.. code-block:: python

   chmod 600 .rsp-tap.token

* Insert the RSP token into this file securely.  The following command permits this by requesting the file owner to enter the RSP token at the first prompt.

.. code-block:: python

   cat <<EOF > .rsp-tap.token

* Close this file by issuing an "end of file" command at the second prompt.  After entering this command, the file will be ready for use for as long as the RSP token is unexpired.

.. code-block:: python

   EOF

**2. Start up a python session.**  This could be a standalone python session running on (say) a laptop, or a Jupyter notebook running elsewhere but displayed on one's own browser.

**3. Import relevant python modules.**  At the minimum, import the ``pyvo`` and ``os`` python modules. 

.. code-block:: python

   import pyvo
   import os

**4. Define the relevant TAP server URL and read in your security token.** For DP0.2, the proper TAP server URL is ``https://data.lsst.cloud/api/tap``, as is shown below.  (For DP0.3, use ``https://data.lsst.cloud/api/ssotap`` instead.)  The ``os.path.expanduser('~')`` command is a cross-platform method for identifying the home directory without hardwiring its path into the code.  (As a side benefit, it works in both the UNIX/MacOS/Linux and Windows environments.) 

.. code-block:: python

   RSP_TAP_SERVICE = 'https://data.lsst.cloud/api/tap'
   homedir = os.path.expanduser('~')
   token_file = os.path.join(homedir,'.rsp-tap.token')
   with open(token_file, 'r') as f:
       token_str = f.readline()

**5. Set up appropriate authorization to access the RSP TAP server.** In line 1 of the following code block, a ``pyvo`` `CredentialStore <https://pyvo.readthedocs.io/en/latest/api/pyvo.auth.CredentialStore.html>`_ is instantiated.  In line 2, the TAP user (``"x-oauth-basic"``) and the RSP token (``token_str``) is passed to the ``CredentialStore``.  Line 3 establishes that the RSP TAP service conforms to the `interface requirements of the International Virtual Observatory (IVOA) for HTTP basic authentication <https://www.ivoa.net/documents/SSO/20170411/PR-SSOAuthMech-2.0-20170411.html#tth_sEc4>`_; hence the ``ivo://ivoa.net/sso#BasicAA`` security method is designated.  Finally, in line 4, a request session to the RSP TAP service is established. 

.. code-block:: python

   cred = pyvo.auth.CredentialStore()
   cred.set_password("x-oauth-basic", token_str)
   credential = cred.get("ivo://ivoa.net/sso#BasicAA")
   rsp_tap = pyvo.dal.TAPService(RSP_TAP_SERVICE, session=credential)


**6. Run a query.**  For example, in the following case, the query requests a list of the catalogs that are available from the RSP TAP service.  More examples of useful DP0.2 queries can be found in the DP0.2 :ref:`DP0-2-Tutorials-Notebooks` and on the :doc:`/data-access-analysis-tools/adql-recipes` page.

.. code-block:: python

   query = "SELECT * FROM tap_schema.schemas"
   results = rsp_tap.run_sync(query)
   results.to_table()

