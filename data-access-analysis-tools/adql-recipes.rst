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

ADQL can be used in both the Notebook and Portal aspects:
 - :ref:`Data-Access-Analysis-Tools-TAP-NB`
 - how to :ref:`Portal-Intro-ADQL-Queries` in the Portal aspect

Learn more about the `TAP-accessible DP0.2 catalogs <https://dp0-2.lsst.io/data-products-dp0-2/index.html#catalogs>`__ which are used in the examples below.

.. Important::
    If a query takes longer than you expect, please submit a `GitHub Issue <https://github.com/rubin-dp0/Support>`__
    or post in the "DP0 RSP Service Issues" category of the Rubin Community Forum.
    Rubin staff are happy to investigate and to help tweak queries for optimal execution.


.. _Adql-Recipes-General-Advice:

General Advice
==============

LSST Query Services (Qserv) provides access to the LSST Database Catalogs.
Users can query the catalogs using standard SQL query language with a few `restrictions <https://qserv.lsst.io/user/index.html#restrictions>`__.

**Fast queries:** 
Qserv stores catalog data sharded by coordinate (RA, Dec).
ADQL query statements that include constraints by coordinate do not requre a whole-catalog search,
and are typically faster (and can be *much* faster) than ADQL query statements which only include constraints for other columns.

**Recommended constraint:**
Include ``detect_isPrimary = True`` in queries for the ``Object``, ``Source``, and ``ForcedSource`` catalogs.
This parameter is ``True`` if a source has no children, is in the inner region of a coadd patch, is in the inner region of a coadd tract, and is not detected in a pseudo-filter.
Including this constraint will remove any duplicates (i.e., will not include *both* a parent and its deblended children).

Additional external resources for learning about SQL, ADQL, and Qserv include:
 - `W3 School's SQL Tutorial <https://www.w3schools.com/sql/default.asp>`__
 - `IVOA's ADQL Documentation <https://www.ivoa.net/documents/ADQL/20180112/PR-ADQL-2.1-20180112.html>`__
 - `LSST Qserv User Guide <https://qserv.lsst.io/user/index.html>`__


.. _Adql-Recipes-Explore-Tables:

Exploring tables
================

When learning about the contents of a table, it can be handy to simply retrieve all columns for "a bunch" (hundreds to thousands) of rows
and take a look at the results.
For this use-case, it is recommended to use the ``SELECT TOP`` statement, like in the example below that just retrieves the first 100 rows of the ``Object`` table.

.. code-block:: SQL

    SELECT TOP 100 * FROM dp02_dc2_catalogs.Object



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

As above, retrieve the ``coord_dec`` and ``coord_ra`` columns from the ``Object`` table for objects within a 0.05 degree radius of RA = 62, Dec = -37,
and also retrieve the g-band AB magnitude and magnitude error.
The ``scisql`` functions used below can be applied to any flux column.

.. code-block:: SQL

   SELECT coord_dec, coord_ra, 
   scisql_nanojanskyToAbMag(g_calibFlux) AS g_calibMag, 
   scisql_nanojanskyToAbMagSigma(g_calibFlux, g_calibFluxErr) as g_calibMagErr 
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), 
   CIRCLE('ICRS', 62, -37, 0.05)) = 1


.. _Adql-Recipes-Table-Joins:

Table joins
===========

Below, the Source and CcdVisit table are joined in order to obtain the date and seeing from the CcdVisit table.
Any two tables can be joined so long as they have an index in common.

This query also renames (nicknames) columns and tables using ``AS``,
and applies a spatial constraint, a temporal constraint (using ``obsStartMJD``), 
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

TruthSummary and MatchesTruth table joins
=========================================

The query below demonstrates how to retrieve the truth table identifier (``id_truth_type`` from the ``MatchesTruth`` table)
and true redshift (from the ``TruthSummary`` table) for a particular detected object with ``ObjectId`` = 1486698050427598336 (from the ``Object`` table)
using a triple table join.

**Director vs. ref match tables:** 
Note that the restriction for the given ``Object`` is written in the query below specifically as ``WHERE obj.objectId=1486698050427598336``.
If we were to write ``WHERE mt.match_objectId=1486698050427598336`` instead, the query could take orders of magnitude longer to execute.
This subtle difference exists because the ``TruthSummary`` and ``Object`` tables are stored in Qserv as what are known as `director tables <https://qserv.lsst.io/user/index.html#director-table>`__,
while the ``MatchesTruth`` table used to join them is stored as a somewhat more restricted "ref match" table.
Qserv has special mechanics to optimize queries with ``WHERE`` restrictions expressed in terms of director tables,
and can often dispatch these queries to just a few involved data shards.
These same mechanics, however, cannot be applied in general to "ref match" tables so the seemingly same restriction,
if expressed in terms of the "ref match" table, would necessitate a full scan of the entire catalog which could be quite time-consuming.

.. code-block:: SQL

    SELECT mt.id_truth_type AS mt_id_truth_type, 
    mt.match_objectId AS mt_match_objectId, 
    obj.objectId AS obj_objectId, 
    ts.redshift AS ts_redshift 
    FROM dp02_dc2_catalogs.MatchesTruth AS mt 
    JOIN dp02_dc2_catalogs.TruthSummary AS ts 
    ON mt.id_truth_type=ts.id_truth_type 
    JOIN dp02_dc2_catalogs.Object AS obj 
    ON mt.match_objectId=obj.objectId 
    WHERE obj.objectId=1486698050427598336 
    AND ts.truth_type=1 
    AND obj.detect_isPrimary=1 
    ORDER BY obj_objectId DESC


.. _Adql-Recipes-ObjectIds:

Individual objects
==================

**Searches for individual objects can take a surprisingly long time.**
Recall that the TAP tables are sharded by RA,Dec, and when RA,Dec constraints are not provided (as in the example below),
the entire table must be searched, and this can take a long time despite the small amount of data returned.

In the above example, a single object was desired, and a statement like ``WHERE objectId=1486`` was used.
However, more than a few single objects are desired and their ``objectId`` are known, a query built up of, e.g.,
``OR objectId=1487 OR objectId=1488 OR objectId=1489`` and so on would work, but there's a better way: ``WHERE objectId IN ()``.

Below, a list of just 12 ``objectId`` are put in a string called ``my_list``, formatted as a python tuple (with round brackets). 
This list could contain many more objects and be generated programmatically (e.g., from a different query, or by user analysis),
and then be included in the ADQL query statement and the TAP service would treat it the same way.
The number of results returned will equal the length of the list of ``objectId`` passed.

For this example, the 12 were selected to be bright stars with similar *g-r* and *i-z* colors,
so the query retrieves the *g*, *r*, *i*, and *z* band fluxes, but users should modify this to their own needs.

.. code-block:: python

    from lsst.rsp import get_tap_service, retrieve_query
    service = get_tap_service()
    
    my_list = "(1249537790362809267, 1252528461990360512, 1248772530269893180, "\
              "1251728017525343554, 1251710425339299404, 1250030371572068167, "\
              "1253443255664678173, 1251807182362538413, 1252607626827575504, "\
              "1249784080967440401, 1253065023664713612, 1325835101237446771)"
    
    query = "SELECT objectId, g_calibFlux, r_calibFlux, i_calibFlux, z_calibFlux "\
            "FROM dp02_dc2_catalogs.Object "\
            "WHERE objectId IN "+my_list
	    
    results = service.search(query)
    results.to_table()