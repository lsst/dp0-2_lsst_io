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

#############################################################
How to plot one- and two-dimensional histograms in the Portal
#############################################################

.. This section should provide a brief, top-level description of the page.

.. Most recent update:  October 9 2024

=====================

The Portal aspect of the Rubin Science Platform lends itself well to retrieve apparent magnitudes of (for instance) extended objects in a region of the sky.  
It provides convenient and easy to use tools to plot 1- and 2-dimensional histograms to explore their apparent magnitude and color distributions.

For the retrieval of the required data, this "How to" uses the Astronomy Data Query Language (ADQL), which is similar to SQL (Structured Query Language).
The option to use the ADQL in the Portal aspect of the Rubin Science Platform is selected by clicking on "Edit ADQL" in the upper right-hand side of the Portal landing page.  

For more information about the DP0.2 catalogs, tables, and columns, visit the DP0.2 Data Products Definition Document (DPDD) 
:ref:`DP0-2-Data-Products-DPDD` or the `DP0.2 Catalog Schema Browser <https://sdm-schemas.lsst.io/dp02.html>`_.  

.. _DP0-2-Portal-Histogram-Step-1:

1.  Preparation and execution of the ADQL query
===============================================

The sample query below uses the ``dp02_dc2_catalogs.Object`` catalog to extract the g-band and r-band fluxes (respectively ``g_calibFlux`` and ``r_calibFlux``) of all extended objects (by selecting ``g_extendedness = 1`` and ``r_extendedness = 1``) in a ~ 1.5 sq. degree region of the sky.  
(The ``calibFlux`` is the flux within a 12 pixel aperture; aperture fluxes are appropriate to use when calculating extended object colors.)
The query converts the fluxes to magnitudes, by the use of an ADQL function ``scisql_nanojanskyToAbMag()`` where the respective flux is the argument (and renames them as ``gmag`` and ``rmag``).  
It restricts the search to return only objects with g- and i-magnitudes less than 23.
It limits the search to those objects located in a circular region with a radius of 0.75 degree, around the direction with RA of 55.75 deg and and Dec of -32.27 deg, via the restriction ``CONTAINS(POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 55.75, -32.27, 0.75) = 1``.

.. code-block:: SQL 

   SELECT coord_dec, coord_ra, 
   scisql_nanojanskyToAbMag(g_calibFlux) as gmag, 
   scisql_nanojanskyToAbMag(r_calibFlux) as rmag, 
   g_extendedness, 
   r_extendedness  
   FROM dp02_dc2_catalogs.Object 
   WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 55.75, -32.27, 0.75)) = 1 
   AND g_extendedness = 1 
   AND r_extendedness = 1 
   AND scisql_nanojanskyToAbMag(g_calibFlux) < 23 
   AND scisql_nanojanskyToAbMag(r_calibFlux) < 23 

2.  Plotting the histogram of g-magnitudes
==========================================

Executing the ADQL query is via clicking the “Search” button in the lower left corner.  
The resulting display will by default show the sky coverage on the left, and the plot of the 1st column as a function of the 2nd column on the right.
To plot the distribution of g magnitudes, it is necessary to add another plot panel, by clicking on the "+" button on the upper left-hand side of the active chart, and selecting "Histogram" as the Plot Type.
The resulting  pop-up window allows a selection of the quantity for the plotted histogram - in ths case, "Column or expression" box needs to have "gmag" entered.
Clicking "Apply" will result in displaying an additional plot window, with g magnitude histogram.
The "coord_ra vs/ coord_dec" plot can be removed by clicking on the "x" in the upper right-hand side of the plot window.
This will result in the dispay as below.  

.. figure:: /_static/Howto_Histogram_1d.png
	:name: Howto_Histogram_1d.png
	:alt: Screenshot of the 1-d histogram of g-magnitudes in the selectred region, obtained by executing an ADQL query.

**Screenshot of the 1-d histogram of g-magnitudes of extended objects in the selectred region, obtained by executing an ADQL query.**

.. _DP0-2-Portal-Histogram-Step-2:

3.  Plotting the 2-d histogram (heatmap) of the g-r colors vs. g magnitudes
===========================================================================

The two-dimensional histogram (heatmap) of the g-r colors vs. g-magnitudes can be prepared by clicking on the "+" button on the upper left-hand side of the active chart.
To plot the heatmap, this needs to be selected in the resulting pop-up window by clicking on "Heatmap" as the plot type.
Plotting of the heatmap of g-r color vs. g-magnitude is accomplished via entering ``gmag`` for X, and ``gmag-rmag`` for Y.
The resulting display will now have the 1-d histogram of magnitudes and 2-d histogram (heatmap) of colors vs. magnitudes, as below.

.. figure:: /_static/Howto_Histogram_2d.png
	:name: Howto_Histogram_1d.png
	:alt: Screenshot of the 2-d histogram of g-r color vs. g-magnitudes in the selectred region, obtained by executing an ADQL query.

**Screenshot showing the 1-d histogram of g-magnitudes as well as the 2-d histogram of g-r color vs. g-magnitudes of the extended objects in the selected region, obtained by executing an ADQL query.**

