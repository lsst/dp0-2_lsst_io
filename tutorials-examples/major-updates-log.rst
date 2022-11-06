.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
    - If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Major-Updates-Log:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#############################
Log of Major Tutorial Updates
#############################


Oct 26 2022
===========

Notebook 03a (image display) updated to replace use of ``objectTable`` via the butler with a TAP query.

Notebook 07a (DiaObject samples) updated to use the recently released ``ForcedSourceOnDiaObject`` table.

Notebooks 09a and 09b (custom coadds) added.


Oct 4 2022
==========

Notebook 08 (truth tables) updated to optimize TAP query.


Sep 29 2022
===========

Notebook 08 (truth tables) added.

The recommended image of the RSP was bumped to version Weekly 40.

Permissions for users' "notebooks/tutorial-notebooks" directory changed to read-only.
For details, see :ref:`NB-Intro-Use-Tutorial-NBs` and :ref:`NB-Intro-Use-A-NB-faq-readonly`,
or `this Forum topic on the permission changes <https://community.lsst.org/t/7087>`_.


Aug 20 2022
===========

Notebooks 03c (survey property maps) and 04b (intermediate butler queries) added.


June 27 2022
============

All tutorials updated for the release of DP0.2.