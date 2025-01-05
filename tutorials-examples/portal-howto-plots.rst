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
.. _Tutorials-Examples-DP0-2-Portal-howto-plots:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

######################################################
08. How to use the results active chart (plotted data)
######################################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to manipulate the active chart and customize the plotted data in the Portal results tab.

**1. Execute a query.**
Go to the Portal's DP0.2 Catalogs tab, switch to the ADQL interface, and execute the query below.

Terminology:

* `ADQL <https://www.ivoa.net/documents/latest/ADQL.html>`_: Astronomy Query Data Language
* PNG: Portable Network Graphic
* color: The difference in magnitude (brightness) between adjacent bands (e.g., g-r, r-i).

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
The default plot will use the first two columns of the returned data table.
In Figure 1, this is the Declination coordinate on the y-axis and the Right Ascension coordinate on the x-axis.
This plot will switch to a two-dimensional histogram if so many objects are returned that individual points cannot be distinguished.

.. figure:: /_static/portal-howto-plots-1.png
    :name: portal-howto-plots-1
    :alt: The default view of the active chart.

    Figure 1: The active chart panel in the Results tab, with default settings, for the query above.


**3. Mouse-over for pop-up notes.**
In the active chart panel (Figure 1) use the mouse to hover over the menus and icons to see pop-up explanations of the functionality.
Hover the mouse over any point in the plot, and a pop-up of the coordinates will appear.

**4. Select an object.**
Click on any point in the plot and it will be colored orange and highlighted in the table panel and in the coverage map.
Click on the "Details" tab (item A in Figure 1) to see the values for all returned columns for the selected object.

**4. Explore menus and icons.**
In the active chart panel (Figure 1) click on each of the icons listed below and review the information, options, and tools.

* B: **Pin** - keep this chart as a tab in the active chart panel.
* C: **Zoom** - enter zoom mode (click-and-drag in the plot to zoom in).
* D: **Pan** - enter pan mode (click-and-drag in the plot to pan around).
* E: **Select** - enter select mode (click-and-drag to create a selection box).
* F: **Unzoom** - reset zoom back to default.
* G: **Save** - open a pop-up window with the option to save the plot as a PNG file.
* H: **Restore** - undo all plot manipulation and restore to the default as in Figure 1.
* I: **Filter** - open a pop-up window to manipulate the filters applied to the data.
* J: **Settings** - open a pop-up window to manipulate the plotted data.
* K: **Expand panel** - have the active chart take the full browser window.
* L: **Add chart** - add a new chart (a new plot) to the active chart panel.

**5. Zoom, pan, and unzoom.**
Click on the zoom icon (C in Figure 1) to enter zoom mode. 
Click-and-drag in the plot to zoom in.
Click on the pan icon (D in Figure 1) to enter pan mode.
Click-and-drag in the plot to recenter the plotted data.
Click on the zoom reset icon (H in Figure 1) to return to the default zoom.

**6. Use the box select tool.**
Click on the box icon (E in Figure 1).
Click-and-drag in the plot to select points (A in Figure 2).
Two new icons will appear to "select" (B in Figure 2) or "filter on" (C in Figure 2) the points.

.. figure:: /_static/portal-howto-plots-2.png
    :name: portal-howto-plots-2
    :alt: Using the selection box tool in the active chart panel.

    Figure 2: After using the box select tool to create a box in the plot (A), two new icons appear (B and C).


**7. Select objects.**
Click on the select icon (B in Figure 2).
The will be marked with a different color in the active chart and the coverage chart, and will be selected in the
table, as shown in Figure 3.

.. figure:: /_static/portal-howto-plots-3.png
    :name: portal-howto-plots-3
    :alt: The full Portal Results tab with points selected in the active chart.

    Figure 3: The full Portal Results tab after points have been selected in the active chart.


**8. Filter on the selected objects.**
Click on the select icon (B in Figure 2) to unselect objects.
Repeat step 6.
Click on the filter icon (C in Figure 2).
The selected objects will now be the only points shown in the active chart, the coverage map, and the table, as in Figure 4.

.. figure:: /_static/portal-howto-plots-4.png
    :name: portal-howto-plots-4
    :alt: The full Portal Results tab with points filtered in the active chart.

    Figure 4: The full Portal Results tab after points have been selected and filtered on in the active chart.

**9. Remove the filter.**
Click on the filter icon (C in Figure 2) to remove the filter and return to the default plot of Figure 1.

**10. Manipulate the plotted data.**
Click on the settings icon (J in Figure 1) to get the plot parameters pop-up window as seen in Figure 5.
Leave the default selection to modify the trace, which means to modify the axes and points in the plot.
For the X axis enter ``g_cModelMag - r_cModelMag`` and for the Y axis enter ``g_cModelMag``.
Ajust the trace options (plot style) and chart options (labels) as in Figure 5.
Click "Apply" and then "Close" in the plot parameters window.

.. figure:: /_static/portal-howto-plots-5.png
    :name: portal-howto-plots-5
    :alt: The plot parameters pop-up window to manipulate the axes and point styles.

    Figure 5: The plot parameters pop-up window with adjustments made to generate a color-magnitude diagram.


**11. Option to save the plot.**
Click on the save icon (G in Figure 1) to download a PNG file of the plot.
It should look like the one shown in Figure 6.

.. figure:: /_static/portal-howto-plots-6.png
    :name: portal-howto-plots-6
    :alt: An example of a color-magnitude diagram.

    Figure 6: The color-magnitude diagram created in step 10.


**12. Add a new chart.**
Click on the "new chart" icon (L in Figure 1), and create another scatter plot color-magnitude diagram
using different columns, point styles, and axis labels.
The new plot will appear as a second panel in the active chart region, as in Figure 7.

.. figure:: /_static/portal-howto-plots-7.png
    :name: portal-howto-plots-7
    :alt: Another example of a color-magnitude diagram.

    Figure 7: Another, different, color-magnitude diagram added as a new chart.


**Warning!** 
After changing the plot settings (e.g., changing which columns are plotted, point symbols and colors),
be wary of clicking the restore icon (H in Figure 1) because it entirely resets the plot to the default
axes and point style as shown in Figure 1.
To zoom out to the original range, click the icon under F in Figure 1, not the icon under H.

Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
