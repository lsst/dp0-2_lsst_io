.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-Adql-Recipes:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.


############
ADQL Recipes
############

.. This section should provide a brief, top-level description of the page.

ADQL is the `Astronomical Data Query Language <https://www.ivoa.net/documents/ADQL/>`_.
The language is used by the `IVOA <https://ivoa.net>`_ to represent astronomy queries posted to Virtual Observatory (VO) services, such as the Rubin LSST TAP service.
ADQL is based on the Structured Query Language (SQL).


`W3 Schools SQL Tutorial <https://www.w3schools.com/sql/default.asp>`__

`LSST Qserv User Guide <https://qserv.lsst.io/user/index.html>`__



.. _Adql-Recipes-General-Advice:

General Advice
==============

*Detectisprimary=true*

*words about how qserv stores data by ra/dec and so that is fast but patch is not*




.. _Adql-Recipes-Cone-Search:

Cone Search
===========

.. code-block:: SQL

   SELECT coord_dec, coord_ra
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),CIRCLE('ICRS', 62, -37, 0.05))=1



.. _Adql-Recipes-FluxToMags:

Convert fluxes to magnitudes
============================

.. code-block:: SQL

   SELECT coord_dec, coord_ra,
   scisql_nanojanskyToAbMag(g_calibFlux) AS g_calibMag,
   scisql_nanojanskyToAbMag(i_calibFlux) AS r_calibMag,
   scisql_nanojanskyToAbMag(r_calibFlux) AS i_calibMag
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62, -37, 0.05))=1




.. _Adql-Recipes-Table-Joins:

Table Joins
===========

*Cite resource for different types of table joins.*

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



.. _Adql-Recipes-Truth-Summary:

TruthSummary table joins
========================

*The efficient way to do this.*


