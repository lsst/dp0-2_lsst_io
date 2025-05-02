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

These rendered notebooks have been confirmed to display properly with Chrome.
Note that there have been reports of some figures not displaying properly in Firefox.

+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| Title                                                                                                                                | Brief Description                                                                        |
+======================================================================================================================================+==========================================================================================+
| NB 01. `Introduction to DP02 <https://dp0-2.lsst.io/_static/nb_html/DP02_01_Introduction_to_DP02.html>`_                             | Use the Jupyter Notebooks and Rubin python packages to access LSST data products.        |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 02a. `Introduction to the TAP Service <https://dp0-2.lsst.io/_static/nb_html/DP02_02a_Introduction_to_TAP.html>`_                 | Explore the DP0.2 catalogs with the TAP service.                                         |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 02b. `Catalog Queries with TAP <https://dp0-2.lsst.io/_static/nb_html/DP02_02b_Catalog_Queries_with_TAP.html>`_                   | Execute complex ADQL queries with the TAP service. Visualize catalog data sets.          |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 02c. `Image Queries with TAP <https://dp0-2.lsst.io/_static/nb_html/DP02_02c_Image_Queries_with_TAP.html>`_                       | Retrieve and display images using the ObsTAP service.                                    |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 03a. `Image Display and Manipulation <https://dp0-2.lsst.io/_static/nb_html/DP02_03a_Image_Display_and_Manipulation.html>`_       | Learn how to display and manipulate images using the LSST Science Pipelines.             |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 03b. `Image Display with Firefly <https://dp0-2.lsst.io/_static/nb_html/DP02_03b_Image_Display_with_Firefly.html>`_               | Use the Firefly interactive interface for image data.                                    |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 03c. `Big deepCoadd Cutout <https://dp0-2.lsst.io/_static/nb_html/DP02_03c_Big_deepCoadd_Cutout.html>`_                           | Create a big cutout image which spans multiple patches and tracts.                       |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 04a. `Introduction to the Butler <https://dp0-2.lsst.io/_static/nb_html/DP02_04a_Introduction_to_the_Butler.html>`_               | Use the Butler to query DP0 images and catalogs.                                         |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 04b. `Intermediate Butler Queries <https://dp0-2.lsst.io/_static/nb_html/DP02_04b_Intermediate_Butler_Queries.html>`_             | Learn to discover data and apply query constraints with the Butler.                      |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 05. `Source Detection and Measurement <https://dp0-2.lsst.io/_static/nb_html/DP02_05_Source_Detection_and_Measurement.html>`_     | Manipulate images; measure sources; and extract, plot, and use object footprints.        |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 06a. `Interactive Image Visualization <https://dp0-2.lsst.io/_static/nb_html/DP02_06a_Interactive_Image_Visualization.html>`_     | Image visualizations with the HoloViews and Bokeh open-source python libraries.          |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 06b. `Interactive Catalog Visualization <https://dp0-2.lsst.io/_static/nb_html/DP02_06b_Interactive_Catalog_Visualization.html>`_ | Visualizations for large datasets with HoloViews, Bokeh, and Datashader.                 |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 07a. `DiaObject Samples <https://dp0-2.lsst.io/_static/nb_html/DP02_07a_DiaObject_Samples.html>`_                                 | Identify a sample of time-variable objects of interest.                                  |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 07b. `Variable Star Lightcurves <https://dp0-2.lsst.io/_static/nb_html/DP02_07b_Variable_Star_Lightcurves.html>`_                 | Use the DP0.2 catalogs to identify variable stars and plot their lightcurves.            |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 08. `Truth Tables <https://dp0-2.lsst.io/_static/nb_html/DP02_08_Truth_Tables.html>`_                                             | Explore, retrieve, and compare data from the truth and measurement tables.               |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 10. `Deblender Data Products <https://dp0-2.lsst.io/_static/nb_html/DP02_10_Deblender_Data_Products.html>`_                       | Explore the footprints of parent and child objects.                                      |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 11. Working with User Packages                                                                                                    | An example of how to install and set up user packages.                                   |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 12a. `PSF Data Products <https://dp0-2.lsst.io/_static/nb_html/DP02_12a_PSF_Data_Products.html>`_                                 | A demonstration of how to access calexp and deepCoadd PSF properties.                    |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 12b. `PSF Science Demo <https://dp0-2.lsst.io/_static/nb_html/DP02_12b_PSF_Science_Demo.html>`_                                   | Demonstration of the use of measured PSF properties in weak lensing analysis.            |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 13a. `Image Cutout SciDemo <https://dp0-2.lsst.io/_static/nb_html/DP02_13a_Image_Cutout_SciDemo.html>`_                           | Demonstration of the use of the image cutout tool with a few science applications.       |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 14. `Injecting Synthetic Sources <https://dp0-2.lsst.io/_static/nb_html/DP02_14_Injecting_Synthetic_Sources.html>`_               | Inject artificial stars and galaxies into images.                                        |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 15. `Survey Property Maps <https://dp0-2.lsst.io/_static/nb_html/DP02_15_Survey_Property_Maps.html>`_                             | Use the tools to visualize full-area survey property maps.                               |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 16. `Galaxy Cluster Weak Lensing <https://dp0-2.lsst.io/_static/nb_html/16_Galaxy_Cluster_Weak_Lensing.html>`_                    | Demonstration of the weak lensing signal around a rich galaxy cluster.                   |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 17. `Anomaly Detection with DiaObjects <https://dp0-2.lsst.io/_static/nb_html/17_DiaObject_Anomaly_Detection.html>`_              | Apply anomaly detection techniques to DIA Objects.                                       |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 18. `Galaxy Photometry <https://dp0-2.lsst.io/_static/nb_html/DP02_18_Galaxy_Photometry.html>`_                                   | Demonstration of galaxy photometry in objectTable.                                       |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| NB 19. `Introduction to AI <https://dp0-2.lsst.io/_static/nb_html/19_Introduction_to_AI.html>`_                                      | An introduction to the classification of images with AI-based classification algorithms. |
+--------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+



More tutorials coming soon!
