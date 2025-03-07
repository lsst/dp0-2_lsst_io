.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Tutorials:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###############
DP0.2 Tutorials
###############

.. This section should provide a brief, top-level description of the page.

These tutorials are for DP0 users using the Rubin Science Platform (RSP) deployed at the Interim Data Facility (IDF; the Google Cloud).

Before following these tutorials, users should:

| 1. have gotten their `RSP account <https://rsp.lsst.io/guides/getting-started/get-an-account.html>`_ and be able to log in at `data.lsst.cloud <https://data.lsst.cloud/>`_,
| 2. be familiar with this list of :doc:`/data-access-analysis-tools/rsp-warnings`,
| 3. have reviewed the basic introductions to the RSP's :ref:`Tools-RSP-Portal` or :ref:`Tools-RSP-Notebook`, and
| 4. know their options for `getting support <https://dp0.lsst.io/delegate-resources/support.html>`_.


All RSP tutorials are created by Rubin staff and adhere to
the set of guidelines and best practices described in `RTN-045 <https://rtn-045.lsst.io/>`_,
unless otherwise noted (e.g., the :ref:`DP0-2-Tutorials-Contributed`).

`Suggest a new tutorial topic <https://community.lsst.org/t/suggest-a-new-dp0-2-tutorial/6556>`_.


.. _DP0-2-Tutorials-Whats-New:

Major Changes Log
=================

.. toctree::
    :titlesonly:
    :glob:

    major-updates-log


.. _DP0-2-Tutorials-Portal:

Portal tutorials
================

A beginner-level overview for the Portal Aspect is provided in this :doc:`/data-access-analysis-tools/portal-intro`.
More information can also be found in the `about firefly <https://data.lsst.cloud/portal/app/onlinehelp/>`_ page on the `Rubin Science Platform Documentation <https://data.lsst.cloud/docs>`_ page.

The tutorials below are step-by-step demonstrations of how to use the Portal Aspect for science investigations with the DP0 data set.

How-to tutorials
----------------

Short tutorials that focus on how to use one Portal function or tool,
typically without scientific context or motivation - just simple examples for quick reference.

.. toctree::
    :titlesonly:
    :glob:

    portal-howto-nav
    portal-howto-uiquery
    portal-howto-adql
    portal-howto-results
    portal-howto-mags
    portal-howto-join
    portal-howto-hips
    portal-howto-hips-alt
    portal-howto-plots
    portal-howto-plots-custom
    portal-howto-histograms
    portal-howto-lightcurves
    portal-howto-table
    portal-howto-table-filter
    portal-howto-table-addcol
    portal-howto-query-image-viaObsTAP
    portal-howto-image-add-layers
    portal-howto-image-extract-pixelvalues



Science tutorials
-----------------

Longer tutorials that demonstrate common workflows for scientific analyses that use multiple Portal tools in sequence,
and that include scientific context and motivation for why the data and tools are used. 

.. toctree::
    :titlesonly:
    :glob:

    portal-beginner
    portal-beginner-ES
    portal-intermediate
    portal-images
    portal-4
    Portal-5
    Portal-6


.. _DP0-2-Tutorials-Notebooks:

Notebook tutorials
==================

After logging in to the Notebook Aspect of the RSP, click on the "Tutorials" menu item and select the
desired tutorial notebook from the drop-down list.
A writeable version of the file will automatically open and be saved in the ``/notebooks/tutorials/`` folder.
Spanish-language Jupyter Notebook tutorials have filenames ending in "ES.ipynb". 

Jupyter Notebook tutorials are kept in the `tutorial-notebooks repository <https://github.com/lsst/tutorial-notebooks>`_.
See that repo's `readme <https://github.com/lsst/tutorial-notebooks/blob/main/README.md>`_ file for details.
Find further instructions and FAQ in the `Notebook Aspect user guide <https://rsp.lsst.io/guides/notebooks/index.html>`_.

.. toctree::
    :titlesonly:
    :glob:

    rendered-tutorial-notebooks

.. _DP0-2-Tutorials-CommandLine:

Command line tutorials
======================

Much of the contents of the tutorial notebooks (above) can also be executed via the terminal in the Notebook Aspect of the RSP.

.. toctree::
    :titlesonly:
    :glob:

    cmdline-beginner
    cmdline-beginner-ES
    butler-cmdline
    cmdline-custom-coadd


.. _DP0-2-Tutorials-API:

API tutorials
=============

The API tutorials will be coming in many flavors, including tutorials using 
`TAP <https://www.ivoa.net/documents/TAP/20190927/index.html>`_, 
`ObsTAP <https://www.ivoa.net/documents/ObsCore/>`_, 
`SODA <https://www.ivoa.net/documents/SODA/20170517/index.html>`_ 
(image cutouts and mosaics), and `HiPS <https://aladin.u-strasbg.fr/hips/>`_, 
and, eventually, `SCS <https://www.ivoa.net/documents/latest/ConeSearch.html>`_ for simple catalog searches, 
`SIAv2 <https://www.ivoa.net/documents/SIA/20150730/index.html>`_ for image searches, and `VOSpace <https://www.ivoa.net/documents/VOSpace/>`_ 
(in addition to `WebDAV <https://en.wikipedia.org/wiki/WebDAV>`_) for access to user files.

As a first step, tutorials using the TAP service are provided.

A beginner-level overview for the API Aspect is provided in this :doc:`/data-access-analysis-tools/api-intro`.

The tutorials below are step-by-step demonstrations of how to use the API Aspect for science investigations with the DP0 data set.

.. toctree::
    :titlesonly:
    :glob:

    api-topcat-beginner



.. _DP0-2-Tutorials-ES:

Spanish-language tutorials
==========================

**Credit:** The Argentinian International In-Kind Program team, in particular Dante Paz, Carolina Villalón, and Marco Augusto Rocchietti,
have translated several DP0.2 tutorials into Spanish.

**Portal tutorials**

.. toctree::
    :titlesonly:
    :glob:

    portal-beginner-ES


**Notebook tutorials**

The introductory DP0.2 Notebook tutorial (DP02_01_Introduccion_a_DP02_ES.ipynb) is available in the
`tutorial-notebooks repository <https://github.com/lsst/tutorial-notebooks>`_ repository.


**Command-line tutorials**

.. toctree::
    :titlesonly:
    :glob:

    cmdline-beginner-ES



.. _DP0-2-Tutorials-Contributed:

Contributed tutorials
=====================

**Where do contributed tutorials go?** 
In the shared GitHub repository `delegate-contributions-dp02 <https://github.com/rubin-dp0/delegate-contributions-dp02>`_.
Contributions are stored in sub-directories by topic, such as "extendedness" or "variable stars".
View the readme files in each sub-directory for more information about the contents and who contributed them.

**Who can contribute a tutorial?**
Everyone is welcome to contribute tutorials or science demonstrations to this repo.
All are welcome to drop in to a `Rubin Science Assembly <https://dp0.lsst.io/delegate-resources/virtual-events.html#dp0-delegate-resources-virtual-events-assemblies>`_ session to workshop a tutorial topic or get assistance.

**How are contributions made?**
The `README <https://github.com/rubin-dp0/delegate-contributions-dp02/blob/main/README.md>`_ file for this repo 
contains instructions and best practices for contributions.
Rubin staff do not apply any quality control reviews to the contributed content in this repo.

**What topics can be contributed?**
Any and all topics are welcome, so long as they can be covered by the DP0.2 data set. 
Here is a short list of potential science topics that DP0.2 could be useful for.

 - TAP catalog queries that access external catalogs
 - galaxy shape parameter analysis (weak lensing?)
 - options for Milky Way dust corrections
 - supernova host galaxy association
 - supernova lightcurve fits (cosmology)
 - photometric redshifts
 - galaxy cluster detection and analysis
 - large scale structure (cosmology)
 - variable star lightcurves analysis
 - astrometry-based analyses


Portal usability test answer keys
=================================

Answer keys for Portal usability tests can also be used as step-by-step tutorials.

.. toctree::
    :titlesonly:
    :glob:

    portal-usabilitytest-answerkey
