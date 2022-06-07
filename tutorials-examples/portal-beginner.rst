.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Portal-Beginner:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###############################################################
Beginner TAP Tutorial - Single Table Usage in the Portal Aspect
###############################################################

.. This section should provide a brief, top-level description of the page.

This brief tutorial will show you how to perform the same data retrieval and analysis that is shown in the first of the :ref:`DP0-2-Tutorials-Notebooks` (titled "Intro to DP0") by using the Portal Aspect's Single Table TAP search function.

In this tutorial we will extract data from a small region of sky in the ``object`` table and build a Color-Magnitude Diagram.

This tutorial assumes you have read the basic introduction to the Portal Aspect in :doc:`/data-access-analysis-tools/portal-intro`.


.. _DP0-2-Portal-Beginner-Step-1:

Select portal aspect from RSP
=============================

After logging into the Portal Aspect, select Single Table (UI assisted) from the **Select Query Type**, then select the ``dp02_dc2_catalogs`` (left) and ``dp02_dc2_catalogs.Object`` (right) from the **Select Table** drop down menus.
This is demonstrated in the next figure.

.. figure:: /_static/Portal_aspect.png
	:name: Single_Table

Next, select the "Spatial" checkbox under **Enter Constraints**, and for the "Longitude Column" and "Latitude Column" enter ``coord-ra`` and ``coord-dec``.
Enter the coordinates of ``62.0, -37.0`` in the "Coordinates or Object Name:" area.
Choose a radius of ``0.1 degree`` and select a row limit of ``10000``, as shown in the next figure.

.. figure:: /_static/Spacial_data.png
    :name: Spatial_data


.. _DP0-2-Portal-Beginner-Step-2:

Select columns for analysis
===========================

In the "Output Column Selection and Constraints" window on the lower right-hand side of the under **Enter Constraints**, select the following items:
``coord_ra``, ``coord_dec``, ``g_cModelFlux``, ``i_cModelFlux``, ``r_cModelFlux``

..  ``clean``, ``dec``, ``extendedness``, ``good``, ``mag_g``, ``mag_i``, ``mag_r``, ``magerr_g``, ``magerr_i``, ``magerr_r``, and ``ra``.

A portion of this step is demonstrated in the next figure.
Use the search box under "column_name" to quickly find columns of interest: for example, type "Flux" into that box and press enter to see only column names that contain "Flux".

.. figure:: /_static/Table_column_selection.png
    :name: Table_column_selection

Then, press the filter icon to select only those items for analysis, as shown in the next figure.

.. figure:: /_static/Table_column_filter.png
    :name: Table_column_filter


.. _DP0-2-Portal-Beginner-Step-3:

Select columns constraints
==========================

After you press the filter icon, you should have only those items you selected shown in the "Output Column Selection and Constraints" table.
You may now add your column constaints to the table.
For this example, use the following values, which limi the source fluxes to the range of 20 - 1000 nanojansky: 
``coord_ra`` leave blank, ``coord_dec`` leave blank, ``g_cModelFlux`` >20 and < 1000, ``i_cModelFlux ``>20 and < 1000, ``r_cModelFlux`` >20 and < 1000,

.. ``clean`` = 1, ``dec`` leave blank, ``xtendedness`` = 0, ``good`` = 1, ``mag_g`` <24, ``mag_i`` <24, ``mag_r`` <24, ``magerr_g`` < 0.1, ``magerr_i`` < 0.1, ``magerr_r`` < 0.1, ``ra`` (leave blank).

Then, press the "Search" button as shown in the next figure.

.. figure:: /_static/Search_with_selected_parameters.png
    :name: Search_with_selected_parameters


.. _DP0-2-Portal-Beginner-Step-4:

Select configure the graph to create a color magnitude diagram
==============================================================

The next figure shows the results of the search.
The gaps in the spatial coverage of the returned catalog objects is due to the limit of 10,000.
The gaps for your search might be different from what is shown below.

.. figure:: /_static/Results_tri_view.png
    :name: Results_tri_view

Next, click on the double gear icon on the upper right-hand window, as shown in the next figure.

.. figure:: /_static/Select_double_gear.png
    :name: Select_double_gear

Finally, change the parameters in the selection box.
Set **X** to be ``-1.0857*log(r_calibFlux/3.631e12+1.0857*log(i_calibFlux/3.631e12)`` and set **Y** to be ``1.0857*log(g_calibFlux/3.631e12)``.
Under **Chart Options**, select "reverse" under the "Y Label".

.. figure:: /_static/Edit_chart_data.png
    :name: Edit_chart_data

After including any other information such as a "Chart title," "X Label," and "Y Label", hit "Apply."
The plot that you make will be slightly different from what is shown below, and different from the plot in the first of the :ref:`DP0-2-Tutorials-Notebooks` due to random sampling and the 10,000 maximum that we used.

.. figure:: /_static/Final_data.png
    :name: Final_data
