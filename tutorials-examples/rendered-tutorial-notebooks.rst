.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
    - If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Tutorials-Examples-DP0-2-Rendered-Tutorial-Notebooks:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

###########################
Rendered tutorial notebooks
###########################

| Title  | Brief Description  |
|---|---|
| 01. `Introduction to DP02 <https://dp0-2.lsst.io/_static/nb_html/DP02_01_Introduction_to_DP02.html>`_ 
 | Use the Jupyter Notebooks and Rubin python packages to access LSST data products. |
| 02. `Catalog Queries with TAP <https://dp0-2.lsst.io/_static/nb_html/DP02_02_Catalog_Queries_with_TAP.html>`_ 
 | Explore the DP0.2 catalogs via TAP and execute complex queries to retrieve data. |
| 03a. `Image Display and Manipulation <https://dp0-2.lsst.io/_static/nb_html/DP02_03a_Image_Display_and_Manipulation.html>`_ 
 | Learn how to display and manipulate images using the LSST Science Pipelines. |
| 03b. `Image Display with Firefly <https://dp0-2.lsst.io/_static/nb_html/DP02_03b_Image_Display_with_Firefly.html>`_ 
 | Use the Firefly interactive interface for image data. |
| 03c. `Survey Property Maps <https://dp0-2.lsst.io/_static/nb_html/DP02_03c_Survey_Property_Maps.html>`_ 
 | Use the tools to visualize full-area survey property maps. |
| 04a. `Introduction to the Butler <https://dp0-2.lsst.io/_static/nb_html/DP02_04a_Introduction_to_the_Butler.html>`_ 
 | Use the Butler to query DP0 images and catalogs. |
| 04b. `Intermediate Butler Queries <https://dp0-2.lsst.io/_static/nb_html/DP02_04b_Intermediate_Butler_Queries.html>`_ 
 | Learn to discover data and apply query constraints with the Butler. |
| 05. `Introduction to Source Detection <https://dp0-2.lsst.io/_static/nb_html/DP02_05_Introduction_to_Source_Detection.html>`_ 
 | Access, display, and manipulate images; detect, deblend, and measure sources; and extract, plot, and use object footprints. |
| 06a. `Interactive Image Visualization <https://dp0-2.lsst.io/_static/nb_html/DP02_06a_Interactive_Image_Visualization.html>`_ 
 | Create interactive image visualizations with the HoloViews and Bokeh open-source python libraries. |
| 06b. `Interactive Catalog Visualization <https://dp0-2.lsst.io/_static/nb_html/DP02_06b_Interactive_Catalog_Visualization.html>`_ 
 | Create interactive catalog visualizations for large datasets with HoloViews, Bokeh, and Datashader. |
| 07a. `DiaObject Samples <https://dp0-2.lsst.io/_static/nb_html/DP02_07a_DiaObject_Samples.html>`_ 
 | Use the DiaObject table parameters to identify a sample of time-variable objects of interest. |
| 07b. `Variable Star Lightcurves <https://dp0-2.lsst.io/_static/nb_html/DP02_07b_Variable_Star_Lightcurves.html>`_ 
 | Use the DP0.2 catalogs to identify variable stars and plot their lightcurves. |
| 08. `Truth Tables <https://dp0-2.lsst.io/_static/nb_html/DP02_08_Truth_Tables.html>`_ 
 | Explore, retrieve, and compare data from the truth and measurement tables. |
| 09a. Custom Coadd  
 | Create a custom "deepCoadd" using only a subset of the input visits. |
| 09b. Custom Coadd Sources 
 | Detect and measure sources in a custom "deepCoadd" image. |
| 10. `Deblender Data Products <https://dp0-2.lsst.io/_static/nb_html/DP02_10_Deblender_Data_Products.html>`_
 | Use the outputs of the multiband deblender to explore the footprints of parent and child objects. |
| 11. Working with User Packages | An example of how to install and set up user packages. |
| 12a. `PSF Data Products <https://dp0-2.lsst.io/_static/nb_html/DP02_12a_PSF_Data_Products.html>`_
 | A demonstration of how to access calexp and deepCoadd PSF properties. |
| 12b. `PSF Science Demo <https://dp0-2.lsst.io/_static/nb_html/DP02_12b_PSF_Science_Demo.html>`_ | Demonstration of the use of measured PSF properties in weak lensing analysis. |
| 13a. `Image Cutout SciDemo <https://dp0-2.lsst.io/_static/nb_html/DP02_13a_Image_Cutout_SciDemo.html>`_
 | Demonstration of the use of the image cutout tool with a few science applications. |
| 14. `Injecting Synthetic Sources <https://dp0-2.lsst.io/_static/nb_html/DP02_14_Injecting_Synthetic_Sources.html>`_
 | Inject artificial stars and galaxies into images. |

More tutorials coming soon!
