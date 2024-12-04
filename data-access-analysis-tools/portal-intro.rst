.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.

.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

############################################################################
How to make a lightcurve of a clearly detected object with known coordinates
############################################################################

.. This section should provide a brief, top-level description of the page.

.. Most recent update:  November 7 2024

The Portal aspect of the Rubin Science Platform lends itself well to extracting and plotting a light curve of an object with known coordinates.
It can be accessed by clicking on the "Portal" panel on the main landing page at data.lsst.cloud.
This example uses the "UI Assisted" means (selected by pressing the "UI Assisted" button on the upper right).

**1.  Selecting a data table containing observing time**:  Plotting of a light curve requires a data table which contains the observation time.
For the simulated DP0.2 data, such table is the dp02_dc2_catalogs.DiaSource, but it contains fluxes at times when the object was detected at ``SNR > 5``.
This table can be accessed by selecting ``DP0.2 Catalogs`` tab on the left-hand side, and the ``dp02_dc2_catalogs.DiaSource`` tab on the right.

If the flux of the object at epochs when the ``SNR < 5`` is needed, a different table using forced photometry (``ForcedSourceOnDiaObject``) needs to be used and this is covered in another "HowTo" guide.

**2.  SN Ia as an example**:  An example here considers a low-redshift SNIa (67.4579, -44.0802) and will extract the ``SNR > 5`` flux data from that location.
Such flux is derived from the processed visit image (PVI; “direct” image), ``psfFlux``.

**3.  Selection criteria for object of interest**:  Selecting the data for the object of interest will require entering the object coordinates in the "Spatial" constraints on the left, selecting the "Cone shape" button and a 2 arcseconds radius.
The box next to "Temporal" needs to be uncheckd (allowing the display of all data points at the required RA and Dec).

**4.  Selection of desired output**:  For the output column, selection of the ``midPointTai`` will yield the time of the observation, ``psFlux`` will give the flux, and ``filterName`` will provide the filter used for the observation.
Pressing on the "funnel" icon will restrict the table on the right to show only the selected entries.

.. figure:: /_static/Howto_lightcurve_1.png
       :name: Howto_lightcurve_1
       :alt: Screenshot of RSP portal start page where the user can select table and constraints

**Screenshot of RSP portal start page with the selected constraints and required output columns.**

Pressing the "Search" button will execute the search, resulting in the three-panel display.  

**5.  Manipulating the resulting plot**:  The right-hand plot, by default, will plot the first two columns of the table.
To plot the flux against time, it is necessary to click on the "gear" icon, and select the "midPointTai-60000" for X and "psFlux" for Y as shown below.  
Note that the plotted flux is as measured in all filters.  

.. figure:: /_static/Howto_lightcurve_2.png
    :width: 300
    :name: Howto_lightcurve_2
    :alt: Screenshot of RSP portal start page where the user can select table and constraints

**Screenshot of the panel displaying the parameters needed to plot the source flux vs. time.**

.. figure:: /_static/Howto_lightcurve_3.png
..  :name: portal_tut02_step01a
..  :alt: Screenshot of RSP portal start page where the user can select table and constraints

**Screenshot of the query results, with the light curve on the right, and the table of the observations on the bottom.**

**6.  Restricting the results to a single filter observation**:  Note that the resulting plot on the right-hand side displays flux in all filters.
It is possible to restrict the plotted flux to be from a single filter by clicking the down-arrow under the "filterName" column heading in the table on the bottom, and selecting only the desired filter, say "r".  



