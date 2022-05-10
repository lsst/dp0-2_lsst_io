.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Data-Products-DP0-2-schema-obj-tm-principal:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

.. This file will not be included in a toctree because it is a reference page.
.. The ``orphan`` metadata field is used to suppress the "WARNING: document isn't included in any toctree."

:orphan:

#####################################################
Principal Columns for Object and Truth Match Catalogs
#####################################################

.. This section should provide a brief, top-level description of the page.

The following two images show the principal columns of the DC2 Objects and Truth Match tables, as seen in the Table View of the Portal Aspect of the Rubin Science Platform.
Learn more in :doc:`/data-access-analysis-tools/portal-intro`.
Other schemas are listed under :ref:`DP0-2-Data-Products-DPDD-Catalogs`.

.. _schema-obj-tm-principal-Objects:

Objects: Principal Columns
==========================

.. figure:: /_static/objects_principal_columns.png
    :name: objects_principal_columns

    Although only the g-band column name and description are shown for ``cModelFlux_flag_g``, ``mag_g_cModel``, ``magerr_g_cModel``, and ``snr_g_cModel`` in this image, the principal columns include these four parameters for all six filters.

.. _schema-obj-tm-principal-TM:

Truth Match: Principal Columns
==============================

.. figure:: /_static/truthmatch_principal_columns.png
    :name: objects_truthmatch_principal_columns

    Although only the g-band column name and description are shown for ``flux_g`` in this image, the principal columns include this parameters for all six filters. However, the Truth Match Catalog only includes ``mag_r``.
