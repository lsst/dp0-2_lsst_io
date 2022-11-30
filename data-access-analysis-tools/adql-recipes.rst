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
The language is used by the `IVOA <https://ivoa.net>`_ to represent astronomy queries posted to Virtual Observatory (VO) services, such as the Rubin LSST Table Access Protocol (TAP) service.
ADQL is based on the Structured Query Language (SQL).

ADQL can be used in both the Notebook and Portal aspects of the Rubin Science Platform (RSP).
 - :ref:`Data-Access-Analysis-Tools-TAP-NB`
 - how to :ref:`Portal-Intro-ADQL-Queries` in the Portal aspect

Learn more about the `TAP-accessible DP0.2 catalogs <https://dp0-2.lsst.io/data-products-dp0-2/index.html#catalogs>`__.

.. Important::
    If a query takes longer than you expect, please submit a `GitHub Issue <https://github.com/rubin-dp0/Support>`__
    or post in the "DP0 RSP Service Issues" category of the Rubin Community Forum.
    Staff with familiarity with Qserv are happy to investigate and to help tweak queries for optimal execution.


.. _Adql-Recipes-General-Advice:

General Advice
==============

LSST Query Services (Qserv) provides access to the LSST Database Catalogs.
Users can query the catalogs using standard SQL query language with a few `restrictions <https://qserv.lsst.io/user/index.html#restrictions>`__.

**Fast queries:** 
Qserv stores catalog data sharded by coordinate (RA, Dec), and catalogs typically have a primary index which is an ``objectId`` (a long integer unique to the catalog).
ADQL query statements that include constraints by coordinate or primary index thus do not requre a whole-catalog search,
and so are typically faster (and can be *much* faster) than ADQL query statements which only include constraints for other columns.

**Recommended constraint:**
Include ``detect_isPrimary = True`` in queries for the ``Object``, ``Source``, and ``ForcedSource`` catalogs.
This parameter is ``True`` if a source has no children, is in the inner region of a coadd patch, is in the inner region of a coadd tract, and is not detected in a pseudo-filter.
Including this constraint will remove any duplicates (i.e., will not include *both* a parent and its deblended children).

Additional external resources for learning about SQL, ADQL, and Qserv include:
 - `W3 School's SQL Tutorial <https://www.w3schools.com/sql/default.asp>`__
 - `IVOA's ADQL Documentation <https://www.ivoa.net/documents/ADQL/20180112/PR-ADQL-2.1-20180112.html>`__
 - `LSST Qserv User Guide <https://qserv.lsst.io/user/index.html>`__




.. _Adql-Recipes-Cone-Search:

Cone Search
===========

Retrieve the ``coord_dec`` and ``coord_ra`` columns from the ``Object`` table for objects within a 0.05 degree radius of RA = 62, Dec = -37.

.. code-block:: SQL

   SELECT coord_dec, coord_ra
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62, -37, 0.05)) = 1



.. _Adql-Recipes-FluxToMags:

Convert fluxes to magnitudes
============================

As above, retrieves the ``coord_dec`` and ``coord_ra`` columns from the ``Object`` table for objects within a 0.05 degree radius of RA = 62, Dec = -37,
but also retrieves the g-band AB magnitude and magnitude error.

.. code-block:: SQL

   SELECT coord_dec, coord_ra,
   scisql_nanojanskyToAbMag(g_calibFlux) AS g_calibMag,
   scisql_nanojanskyToAbMagSigma(g_calibFlux, g_calibFluxErr) as g_calibMagErr
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62, -37, 0.05)) = 1


.. _Adql-Recipes-Table-Joins:

Table Joins
===========

*Cite resource for different types of table joins.*

In the example below, the Source and CcdVisit table are joined in order to obtain the date and seeing from the CcdVisit table.
Any two tables can be joined so long as they have an index in common.

Note that the example below demonstrates how to rename (nickname) columns and tables using ``AS``,
and also applies a spatial constraint, a temporal constraint (using ``obsStartMJD``), 
and constraints on the band, extendedness, and flux value.

Additional external resources on SQL table joins:
 - `W2 School's SQL tutorial: joins <https://www.w3schools.com/sql/sql_join.asp>`__
 - `The Data School: SQL Joins Explained Visually <https://dataschool.com/how-to-teach-people-sql/sql-join-types-explained-visually/>`__

.. code-block:: SQL

   SELECT src.ccdVisitId AS src_ccdVisitId,
   src.extendedness AS src_extendedness,
   src.band AS src_band,
   scisql_nanojanskyToAbMag(src.psfFlux) AS src_psfAbMag,
   cv.obsStartMJD AS cv_obsStartMJD,
   cv.seeing AS cv_seeing
   FROM dp02_dc2_catalogs.Source AS src
   JOIN dp02_dc2_catalogs.CcdVisit AS cv
   ON src.ccdVisitId = cv.ccdVisitId
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec),
   CIRCLE('ICRS', 62.0, -37, 1)) = 1
   AND src.band = 'i' 
   AND src.extendedness = 0 
   AND src.psfFlux > 10000
   AND cv.obsStartMJD > 60925 
   AND cv.obsStartMJD < 60955



.. _Adql-Recipes-Truth-Summary:

TruthSummary table joins
========================

*The efficient way to do this.*


