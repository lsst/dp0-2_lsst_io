.. This is the beginning of a new tutorial focussing on learning to study variability using features of the Rubin Portal

.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-howto-plots-custom:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#########################################################
08.1. How to add custom plots to the results active chart
#########################################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** intermediate 

**Introduction:**
This tutorial demonstrates how to manipulate the active chart and customize the plotted data in the Portal results tab.

**1. Execute a query.**
Go to the Portal's DP0.2 Catalogs tab, switch to the ADQL interface, and execute the query below.

.. code-block:: SQL

  SELECT coord_dec, coord_ra, detect_isPrimary, refExtendedness, 
         scisql_nanojanskyToAbMag(u_cModelFlux) AS u_cModelMag, 
         scisql_nanojanskyToAbMag(g_cModelFlux) AS g_cModelMag, 
         scisql_nanojanskyToAbMag(r_cModelFlux) AS r_cModelMag, 
         scisql_nanojanskyToAbMag(i_cModelFlux) AS i_cModelMag, 
         scisql_nanojanskyToAbMag(z_cModelFlux) AS z_cModelMag, 
         scisql_nanojanskyToAbMag(y_cModelFlux) AS y_cModelMag
  FROM dp02_dc2_catalogs.Object 
  WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), 
        CIRCLE('ICRS', 62, -37, 0.167)) =1 
        AND (detect_isPrimary =1 AND refExtendedness =1 
             AND u_cModelFlux >360 AND g_cModelFlux >360 
             AND r_cModelFlux >360 AND i_cModelFlux >360 
             AND z_cModelFlux >360 AND y_cModelFlux >360)


**2. View the default active chart** (Figure 1).
The default plot will use the first two columns of the returned data table (Figure 1).

.. figure:: /_static/portal-howto-plots-1.png
    :name: portal-howto-plots-1
    :alt: The default view of the active chart.

    Figure 1: The active chart panel in the Results tab, with default settings, for the query above.


**3. Customize the default plot.**
Click on the settings icon (J in Figure 1) to get the plot parameters pop-up window as seen in Figure 2.
Leave the default selection as modify the trace, which means to modify the axes and points in the plot.
For the X axis enter ``g_cModelMag - r_cModelMag`` and for the Y axis enter ``g_cModelMag``.
Ajust the trace options (plot style) and chart options (labels) as in Figure 2.
Click "Apply" and then "Close" in the plot parameters window.

.. figure:: /_static/portal-howto-plots-5.png
    :name: portal-howto-plots-5
    :alt: The plot parameters pop-up window to manipulate the axes and point styles.

    Figure 2: The plot parameters pop-up window with adjustments made to generate a color-magnitude diagram.


**4. Option to save the plot.**
Click on the save icon (G in Figure 1) to download a PNG file of the plot.
It should look like the one shown in Figure 3.

.. figure:: /_static/portal-howto-plots-6.png
    :name: portal-howto-plots-6
    :alt: An example of a color-magnitude diagram.

    Figure 3: The color-magnitude diagram created in step 11.


**5. Add a new chart.**
Click on the "new chart" icon (L in Figure 1), and create another scatter plot color-magnitude diagram
using different columns, point styles, and axis labels.
The new plot will appear as a second panel in the active chart region, as in Figure 4.

.. figure:: /_static/portal-howto-plots-7.png
    :name: portal-howto-plots-7
    :alt: Another example of a color-magnitude diagram.

    Figure 4: Another, different, color-magnitude diagram added as a new chart.


**Warning!** 
After changing the plot settings (e.g., changing which columns are plotted, point symbols and colors),
be wary of clicking the restore icon (H in Figure 1) because it entirely resets the plot to the default
axes and point style as shown in Figure 1.
To zoom out (reset to default zoom), click the icon under F in Figure 1, not the icon under H.


Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.