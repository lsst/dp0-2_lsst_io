.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-1-Tutorials:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###############
DP0.1 Tutorials
###############

.. This section should provide a brief, top-level description of the page.

These tutorials and user guides are for DP0 delegates using the Rubin Science Platform (RSP) deployed at the Interim Data Facility (IDF), the Google cloud.

Before following these tutorials, delegates should have gotten their :ref:`Delegate-Homepage-RSP-Accounts`, be familiar with this list of :doc:`/data-access-analysis-tools/rsp-warnings`
and :ref:`the basic components of the RSP <Data-Access-Analysis-Tools-RSP>`, and know how and where to :ref:`get support <Delegate-Homepage-Getting-Support>`. 


.. _DP0-1-Tutorials-Notebooks:

Jupyter notebook tutorials
==========================

The tutorial notebooks in the ``rubin-dp0`` GitHub Organization's `tutorial-notebooks repository <https://github.com/rubin-dp0/tutorial-notebooks>`_ will be available by default in a folder in each user's home directory in the RSP's Notebook Aspect.
See that repository's README file for descriptions of the notebooks.

**Acknowledgments:** Many of these tutorial notebooks were originally developed by `Stack Club <https://github.com/LSSTScienceCollaborations/StackClub>`_ members and have been altered and updated to be appropriate for DP0. 
If these notebooks are used for a journal publication, please consider adding an acknowledgment that gives credit to the original creator(s) as listed in the notebook's header.


.. _DP0-1-Tutorials-Portal:

Portal aspect demonstrations
============================

An overview of the RSP Portal functionality is provided in this :doc:`/data-access-analysis-tools/portal-intro`. 
Below are two step-by-step demonstrations of how to use the Portal for science investigations.

.. toctree::
    :titlesonly:
    :glob:

    portal-beginner
    portal-advanced
