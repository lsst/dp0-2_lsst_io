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

This "How-to" exercise will show how to plot data, and manipulate such a plot.
The example below will illustrate it for a color-magnitude diagram for a sample of objects.

**1.  Selection of data**:  For the purpose of this exercise, it is necessary to first select data for plotting.
This can be accomplished in the "UI assisted" aspect of the Portal, by executing a search in the ``DP0.2 Object`` catalog using a 3 arcminute cone near the DC2's central coordinates.
The search will return only the five data columns: "coord_ra", "coord_dec", and "g" "r" and "i_calibFlux" - those are selected by checking boxes to the left of the desired row.
It will also impose the constraints that the flux must be between 20 and 1000 nanojansky.
The ready-to-execute search is in the screenshot below.
Note that the displayed rows are limited only to the checked ones:  this is accomplished by clicking on the funnel above the selected boxes.

.. figure:: /_static/portal_intro_DP02b.png
    :name: portal_example_search_DP02
    :alt: Screenshot of the rubin science platform portal query page.  The user can select the type of service, the table from which to gather data, and select attributes
    	from the table and put constraints on those attributes.  The user may also select the number of data entries to return.

   **An example query of the DC2 Object catalog.**

**2.  Manipulating the plotted data**:
Once the data were retrieved by executing "search" on the query above, the manipulation of the plotted data can be done by selecting the single gear "Plot Parameters" icon above the active chart.
This will result in an opening of a pop-up window as illustrated in the next figure.
This example shows how to plot the data using magnitudes rather than fluxes.
Currently, the tables contain only fluxes (no magnitudes).
In the future, magnitudes will be available.

**3.  Converting fluxes to magnitudes**:  To create a color-magnitude diagram from the fluxes, it is necessary 
to apply the `standard conversion from nanojansky to AB magnitude <https://en.wikipedia.org/wiki/AB_magnitude>`_
in the X and Y boxes as, e.g., "-2.5 * log10(g_calibFlux) + 31.4" for the Y axis, and "-2.5 * log10(r_calibFlux)+2.5 * log10(i_calibFlux)" for the X axis.
Note that the Y axis needs to be reversed (via checking the "reverse" button as shown on the screen shot), to have the faint objects at the bottom, and the bright objects at the top.

**4.  Adding axis labels and a title**:  The pop-up window also allows to add the chart title and label the axes (via the "Chart Options" box), and to choose a color for the data points (via the "Trace Options" box).
To modify the plot, one needs to click "Apply" and then "Close".

.. figure:: /_static/portal_intro_DP02e.png
    :name: portal_results_xy_settings_DP02
    :alt: Screenshot of the plot settings pop up window where the user can select various values and plot types to display the data from a query.  From here, the user can select parameters, label the x and y axes, and add a new plot, overplot, or modify a previous plot

    :width: 300

   ** The plot settings pop-up window.**

**5.  Imposing additional cuts on the plotted data**:  At this point, additional cuts can be applied to the table data being plotted.
In the figure below, the g-band flux is limited to > 100 (via the constraint entered in the header of the column "g_calibFlux").
This imposes a sharp cutoff in the y-axis values at 26.4 mag. 
The windows which are displayed can be adjusted by using the "hamburger" menu at upper left.
Clicking on that icon will drop down a "Results Layout" sub-menu, which in turn allows selecting the desired display.

**6.  Exploring the links between the table entries and plotted data points**:  Note that the displayed data in the table and the plotted data points are linked.
Clicking on any row in the table on the left will result in the corresponding plot point for the selected row in the table will be differently colored.
Also, hovering the mouse over the plotted data will show the x- and y-values in a pop-up window.

.. figure:: /_static/portal_intro_DP02f.png
    :name: portal_results_final_DP02
    :alt: Screenshot of the results from the query described above.  The top image shows a color magnitude diagram with magnitude g brightness plotted against the color r minus color i magnitude.
    	Below the plot is the data table generated during the query.
	An updated results view in which the plotted data has been manipulated.

    **Screenshot of the results from the query described above, with the table on the left, and the r-i color vs. g magnitude plot on the right.**
