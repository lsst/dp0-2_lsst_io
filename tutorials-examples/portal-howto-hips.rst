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
.. _Tutorials-Examples-DP0-2-Portal-howto-hips:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

####################################################
07. How to use the results coverage chart (HiPS map)
####################################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** intermediate 

**Introduction:**
This tutorial demonstrates how to manipulate the coverage chart and HiPS map panel in the Portal results tab.

Terminology:

* `HiPS <https://aladin.cds.unistra.fr/hips/>`_: Hierarchical Progressive Surveys 
* `MOC <https://www.ivoa.net/documents/MOC/>`_: Multi-Order Coverage map 
* `ADQL <https://www.ivoa.net/documents/latest/ADQL.html>`_: Astronomy Query Data Language
* `HEALpix <https://healpix.sourceforge.io/>`_: Hierarchical Equal Area isoLatitude Pixelation of a sphere
* `2MASS <https://irsa.ipac.caltech.edu/Missions/2mass.html>`_: Two Micron All Sky Survey 
* `regions <https://ds9.si.edu/doc/ref/region.html>`_ file: a standard format for marking regions in an image
* WCS: World Coordinate System (the convention that defines the coordinates per pixel)
* PNG: Portable Network Graphic


**1. Execute a query.**
Go to the Portal's DP0.2 Catalogs tab, switch to the ADQL interface, and execute the query below.

.. code-block:: SQL

  SELECT coord_dec, coord_ra, detect_isPrimary, refExtendedness, 
         u_cModelFlux, g_cModelFlux, r_cModelFlux, 
         i_cModelFlux, z_cModelFlux, y_cModelFlux 
  FROM dp02_dc2_catalogs.Object 
  WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), 
        CIRCLE('ICRS', 62, -37, 0.167)) =1 
        AND (detect_isPrimary =1 AND refExtendedness =1 
             AND u_cModelFlux >360 AND g_cModelFlux >360 
             AND r_cModelFlux >360 AND i_cModelFlux >360 
             AND z_cModelFlux >360 AND y_cModelFlux >360)

**2. View the default coverage chart** (Figure 1).
The default view is a HEALpix grid showing the number of returned objects per grid region.
Small red squares mark individual objects outside the grid.
The background is a color HiPS map of the DP0.2 deeply coadded images.

.. figure:: /_static/portal-howto-hips-1.png
    :name: portal-howto-hips-1
    :alt: The default view of the coverage chart.

    Figure 1: The coverage chart panel in the Results tab, with default settings, for the query above. When the screenshot was taken the mouse was positioned on the green crosshair symbol, so the WCS Coordinates at lower left (item D) show the mouse position.


**3. Mouse-over for pop-up notes.**
In the coverage chart panel (Figure 1) use the mouse to hover over the menus and icons to see pop-up explanations of the functionality.

**4. Explore menus and icons.**
In the coverage chart panel (Figure 1) click on each of the drop-down menus and icons listed below, and see the pop-up windows of options and tools.

* A: **HiPS/MOC** options to change the underlying HiPS map or add a MOC layer.
* B: **WCS** options to choose the orientation and projection of the underlying HiPS map.
* C: **Zoom** in, out, or to fit the window. (It is also possible to use the mouse to zoom.)
* D: **WCS Coordinates** of the mouse position. Click the box-and-arrow icon at left to view coordinates in a separate window.
* E: **Toggle lock** to "on" to lock the WCS Coordinates to the location of the last mouse click, and "off" for continuous position.
* F: **Tools** menu with options to save, reset, or orient the display; add compass, ruler, points, etc.
* G: **Color table** menu to choose a different color map.
* H: **Recenter** by entering coordinates for the desired display center.
* I: **Spatial selection** (not currently active for HiPS maps).
* J: **Overlays** manipulation to change the options or color for the HEALpix and points overlay.
* K: **Image lock** and alignment (tools for when multiple images are displayed).
* L: **Expand panel** to have the coverage chart take the full browser window.

**5. Change the HiPS image.**
Under A in Figure 1, click on "HiPS/MOC" and then "Change HiPS image".
The pop-up window offers options of color images made from different filter combinations and single-filter DP0.2 images.
There is also the option of a blank background or 2MASS color images (the real 2MASS images will not match the location of the simulated DP0.2 objects).
Select the DP0.2 i-band image.

**6. Add a north arrow.**
Click on the tools icon (F in Figure 1) and in the row for Layers, select the north arrow icon (the compass with north-up, east-left).
The north arrow will appear in the image. 

**7. Invert the color map.**
Click on the color palette icon (G in Figure 1) and select the color bar showing white-to-black left-to-right.
The HiPS map display will be inverted and the stars will be dark on a light background.

**8. Recenter on a bright star.**
Click on the target icon (H in Figure 1) and enter ``4h08m32.54s, -36d57m44.2s`` in the box.
Click "Go & Mark".
The display will recenter on a bright star and it will be marked with a crosshair icon.

**9. Manipulate the layers.**
Click on the layers icon (J in Figure 1).
Make changes as shown in Figure 2.
Change the colors of the north arrow to purple and the marked bright star to green.
Under "Coverage", next to "Min Group" select "40" from the drop down menu to change the HEALpix grid overlay.
Toggle off the layer to display the central search position from the ADQL query.

.. figure:: /_static/portal-howto-hips-2.png
    :name: portal-howto-hips-2
    :alt: The pop-up window for overlays.

    Figure 2: The pop-up window to manipulate the layers, with the changes of step 9 implemented.

**10. Zoom in.**
Above C in Figure 1, click the "zoom in" icon (magnifying glass with a + inside) three times to zoom in.

**11. View the new coverage chart.**
It should look similar to Figure 3.

.. figure:: /_static/portal-howto-hips-3.png
    :name: portal-howto-hips-3
    :alt: The new view of the manipulated coverage chart.

    Figure 3: The coverage chart panel with modifications from steps 5, 6, 7, 8, 9, and 10 applied.


**12. Option: save a PNG of the coverage chart.**
Click on the tools icon (F in Figure 1) and select the disk icon next to "Save...".
Leave the default selection of PNG file and click "Save".
An image of the coverage chart will automatically download.
Note the option to export the overlays as a regions file.

**13. Reset the coverage chart.**
Click on the tools icon (F in Figure 1) and select the circlular arrow icon next to "Save..." to restore to default options.

**14. Select a single object.**
Zoom in on the coverage map until individual object markers are displayed instead of the HEALpix grid.
Click on any marker, and notice that it's row will be highlighted orange in the table panel and its symbol will be orange in the active chart.

**15. What about the spatial selection tool?**
Using this tool (I in Figure 1) with HiPS maps is still a work in progress.

**Exercises for the learner.**

* Remove the north arrow.
* Delete the marker for the bright star.
* Switch the coverage overlay from HEALpix to heatmap.
* Switch the color palette to "cool".

Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
