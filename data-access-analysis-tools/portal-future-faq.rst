.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-Portal-Future-FAQ:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the link check process.


############################
Portal Future Functionality FAQ
############################

This page contains answers to frequently asked questions (FAQ) about the future full functionality of the Portal Aspect of the Rubin Science Platform (RSP).


Will the portal have the functionality to compute statistics such as mean, standard deviation (stdev), and median absolute deviation (mad)?
-------------------------------------------------------------------------------------------------------------------------------------------
Currently, for a FITS image, the image toolbox has a ``Select a Region`` icon, which contains the ``Obtain Statistics`` option (with an icon that resembles an uppercase greek sigma letter).
After a region has been selected and this option chosen, the  statistics option results in a pop-upwindow that contains ststistics such as the mean, the standard deviation, the integrated flux, the minimum and maximum flux in the region, etc. 


Will the portal support the creation of regression models?
----------------------------------------------------------
Currently, the Portal does not support direct creation of regression models, such as fitting a line to a plot of data.
The development focus is on enabling seamless integration with external tools, like the Notebook Aspect of the RSP, which can perform a wide range of fit functions.
This approach leverages the extensive capabilities of the scientific Python community and provides more robust and flexible fitting options.

Is there a maximum row limit for query output in the portal?
------------------------------------------------------------
The row limit for query outputs is adjustable by the user, typically set by default to a small number (e.g., 10,000) when testing queries. The maximum number of rows to return is 5000000.

Will there be a feature to estimate the number of rows a query will return without retrieving the full dataset?
---------------------------------------------------------------------------------------------------------------
Yes, the `COUNT` function can be used in ADQL (Astronomical Data Query Language) similarly to how it is used in SQL.
This function can be currently used in the `Edit ADQL` view section in the Portal.

Additonal Questions
-------------------

To ask additional questions, please use the "Support -- Rubin Science Platform" category in the Rubin Observatory `Community Forum <https://community.lsst.org/c/support/lsp/39>`_
