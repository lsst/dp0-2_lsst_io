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

##############################
How to manipulate plotted data
##############################

.. This section should provide a brief, top-level description of the page.

For the purpose of this exercise, if is necessary to select data for plotting.  This will be accomplised by executing the 

**Manipulating the plotted data and converting fluxes to magnitudes**:
Manipulation of the plotted data can be done by selecting the single gear "settings" icon above the active chart.
This will result in an opening of a pop-up window as illustrated in the next figure.  
This example shows how to plot the data using magnitudes rather than fluxes.  
Currently, the tables contain fluxes (no magnitudes).
In the future, magnitudes will be available.

To create a color-magnitude diagram from the fluxes, for DP0.2 it is necessary 
to apply the `standard conversion from nanojansky to AB magnitude <https://en.wikipedia.org/wiki/AB_magnitude>`_ 
in the X and Y boxes as, e.g., "-2.5 * log10(g_calibFlux) + 31.4" for the Y axis, and "-2.5 * log10(r_calibFlux)+2.5 * log10(i_calibFlux)" for te X axis.  

Add a chart title and label the axes, choose a point color, and click "Apply" and then "Close".

.. figure:: /_static/portal_intro_DP02e.png
    :name: portal_results_xy_settings_DP02
    :alt: Screenshot of the plot settings pop up window where the user can select various values and plot types to display the data from a query.  
    	From here, the user can select parameters, lable the x and y axes, and add a new plot, overplot, or modify a previous plot
    :width: 200

     The plot settings pop-up window.

At this point, additional cuts can be applied to the table data being plotted.
In the figure below, the g-band flux is limited to >100 (via the constraint entered in the header of the column "g_calibFlux"), and this imposes a sharp cutoff in the y-axis values at 
26.4 mag. 
Convert the plot to "Tables Coverage Charts" using the "hamburger" menu at upper left and select only the "Active Chart" tab.  
Click on any row in the table on the left, and notice how the corresponding plot point for the selected row in the table is differently colored, and that 
hovering the mouse over the plotted data will show the x- and y-values in a pop-up window.

.. figure:: /_static/portal_intro_DP02f.png
    :name: portal_results_final_DP02
    :alt: Screenshot of the results from the query described above.  The top image shows a color magnitude diagram with magnitude g brightness plotted against the color r minus color i magnitude.
    	Below the plot is the data table generated during the query.  
	An updated results view in which the plotted data has been manipulated.

**Learn more.**
See also :ref:`DP0-2-Tutorials-Portal` for additional demonstrations of how to use the Portal's UI assisted 
Query.

.. _Portal-Intro-ADQL-Queries:

