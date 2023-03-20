.. This is the beginning of a new tutorial focussing opn learning to study variability using features of the Rubin Portal

.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-Beginner:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###################################################
05.  (beginner)
###################################################

.. This section should provide a brief, top-level description of the page.

**Contact authors:** Melissa Graham and Greg Madejski

**Last verified to run:** 2023-03-20

**Targeted learning level:** beginner

**Introduction:**

Generally, the DiaSource table can be used to plot light curves, but it only includes SNR>5 detections in the difference images. 
If your science goal requires lower-SNR measurements (e.g. including fluxes of a given object measured during all visits to the location of the 
object), then one can use the forced photometry in the ForcedSourceOnDiaObjects table instead.  

Let's say there is a specific object whose light curve looks particularly interesting. 
In order to explore the flux of the object in all sets of differences images (not just those with detected sources), one can explore the 
ForcedSourceOnDiaObject catalog.  The Table in this catalog contains point-source forced-photometry measurements on individual 
single-epoch visit images and difference images, based on and linked to the entries in the DiaObject table.

For more information, see the schema of the ForcedSourceOnDiaObject catalog.


.. _DP0-2-Portal-5-Step-1:

Step 1. Set the query constraints
=================================

1.1. Log in to the Portal Aspect.
