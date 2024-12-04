.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-Portal-Intro:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

########################################################################################################
How to use and edit the Astronomical Data Query Language (ADQL) commands in the Portal Aspect of the RSP
########################################################################################################

.. This section should provide a brief, top-level description of the page.

.. Most recent update:  December 4 2024

The ADQL commands can be exectuted from the Portal Aspect of the Rubin Science Platform.
This can be accessed by clicking on the "Portal" panel of the main landing page at `data.lsst.cloud <https://data.lsst.cloud>`_ and selecting one of the "DP0" tabs.

ADQL is the `Astronomical Data Query Language <https://www.ivoa.net/documents/ADQL/>`_.
The language is used by the `IVOA <https://ivoa.net>`_ to represent astronomy queries posted to Virtual Observatory (VO) services, such as the Rubin LSST TAP service. ADQL is based on the Structured Query Language (SQL).

**1.  Accessing the ADQL query box**:  ADQL query box is acceesible by clicking the "Edit ADQL" box on the upper right of the Portal landing page, after selecting one of the "DP0" tabs.
This will change the user interface to display an empty box where users can supply their query statement.
Scrolling down in that interface will show several examples.

**2.  Converting the UI-assisted search to an ADQL query**:  It is possible to convert a query entered via the UI assisted (i.e., single table) means into an ADQL command.  
At any point while assembling a query using the UI assisted query interface, clicking on "Populate and edit ADQL" 
at the bottom of the page will transform the UI query into ADQL command.  
Note that any changes then made to the ADQL are not propogated back to the UI assisted query constraints.

Converting fluxes to magnitudes is much easier with the ADQL interface by using the ``scisql_nanojanskyToAbMag()`` functionality as demonstrated below.

**3. Querying the TAP schema**:  Information about the LSST TAP schema can be obtained via ADQL queries.
The example below illustrates how to get the detailed list of columns available in the "Object" table, their associated units and descriptions:

.. code-block:: SQL

   SELECT tap_schema.columns.column_name, tap_schema.columns.unit,
   tap_schema.columns.description
   FROM tap_schema.columns
   WHERE tap_schema.columns.table_name = 'dp02_dc2_catalogs.Object'

**4.  An example of an ADQL query to search the Object table near a specified RA and Dec location**:  This query will return RA, Dec, and g, i, and r_calibFlux for all objects within 0.05 degrees from RA = 67 deg and Dec = -37 deg and with respective fluxes between 20 and 1000 nanoJnsky:

.. code-block:: SQL

   SELECT coord_dec,coord_ra,g_calibFlux,i_calibFlux,r_calibFlux
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),CIRCLE('ICRS', 62, -37, 0.05))=1
   AND (g_calibFlux >20 AND g_calibFlux <1000
   AND i_calibFlux >20 AND i_calibFlux <1000
   AND r_calibFlux >20 AND r_calibFlux <1000).

Once entered into the ADQL box, the above query can be exectuted by clicking the "Search" button in the bottom-left corner.
It is advisable to set the "Row Limit" to be a small number, such as 10000, when testing queries.
The search results will populate the **Results View**.

**5.  Converting fluxes to magnitudes**:  The query above can be edited to return magnitudes rather than fluxes: 

.. code-block:: SQL

   SELECT coord_dec, coord_ra,
   scisql_nanojanskyToAbMag(g_calibFlux) AS g_calibMag,
   scisql_nanojanskyToAbMag(i_calibFlux) AS r_calibMag,
   scisql_nanojanskyToAbMag(r_calibFlux) AS i_calibMag
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62, -37, 0.05))=1
   AND g_calibFlux BETWEEN 20 AND 1000
   AND r_calibFlux BETWEEN 20 AND 1000
   AND i_calibFlux BETWEEN 20 AND 1000

**6.  Joining two or more tables**:  It is often desirable to access data stored in more than just one table.
This is possible to do using a JOIN clause to combine rows from two or more tables.
In the example below, the Source and CcdVisit table are joined in order to obtain the date and seeing from the CcdVisit table.
Any two tables can be joined so long as they have an index in common.

.. code-block:: SQL

   SELECT src.ccdVisitId, src.extendedness, src.band,
   scisql_nanojanskyToAbMag(src.psfFlux) AS psfAbMag,
   cv.obsStartMJD, cv.seeing
   FROM dp02_dc2_catalogs.Source AS src
   JOIN dp02_dc2_catalogs.CcdVisit AS cv
   ON src.ccdVisitId = cv.ccdVisitId
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62.0, -37, 1)) = 1
   AND src.band = 'i' AND src.extendedness = 0 AND src.psfFlux > 10000
   AND cv.obsStartMJD > 60925 AND cv.obsStartMJD < 60955

.. _Portal-Intro-Image-Queries:

