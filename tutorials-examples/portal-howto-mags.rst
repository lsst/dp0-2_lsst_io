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
.. _Tutorials-Examples-DP0-2-Portal-howto-mags:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#################################################
05. How to convert fluxes to magnitudes with ADQL
#################################################

.. This section should provide a brief, top-level description of the page.

**RSP Aspect:** Portal

**Contact authors:** Greg Madejski and Melissa Graham

**Last verified to run:** 2025-02-04

**Targeted learning level:** beginner 

**Introduction:**
This tutorial demonstrates how to convert fluxes to magnitudes using a special ADQL function.

**Warning!** Fluxes measured in difference images can be negative.
Negative fluxes should not be converted to magnitudes using this special ADQL function.

**1. Go to the DP0.2 catalog ADQL interface.**
Navigate to the Portal's DP0.2 Catalogs tab and switch to the ADQL interface.

**2. For magnitudes, use the ``scisql_nanojanskyToAbMag()`` function.**
This function will convert a flux value with the units of nanoJanskies (nJy) into an AB magnitude.
The conversion is :math:`m = -2.5 log(f) + 31.4`, where :math:`m` is magnitude and :math:`f` is flux.

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


**3. For magnitude errors, use the ``scisql_nanojanskyToAbMagSigma()`` function.**
This funtion will convert the corresponding flux errors, in nJy, into AB magnitude errors.

.. code-block:: SQL

  SELECT coord_dec, coord_ra, detect_isPrimary, refExtendedness, 
         scisql_nanojanskyToAbMag(u_cModelFlux) AS u_cModelMag, 
         scisql_nanojanskyToAbMagSigma(u_cModelFlux, u_cModelFluxErr) AS u_cModelMagErr, 
         scisql_nanojanskyToAbMag(g_cModelFlux) AS g_cModelMag, 
         scisql_nanojanskyToAbMagSigma(g_cModelFlux, g_cModelFluxErr) AS g_cModelMagErr, 
         scisql_nanojanskyToAbMag(r_cModelFlux) AS r_cModelMag, 
         scisql_nanojanskyToAbMagSigma(r_cModelFlux, r_cModelFluxErr) AS r_cModelMagErr, 
         scisql_nanojanskyToAbMag(i_cModelFlux) AS i_cModelMag, 
         scisql_nanojanskyToAbMagSigma(i_cModelFlux, i_cModelFluxErr) AS i_cModelMagErr, 
         scisql_nanojanskyToAbMag(z_cModelFlux) AS z_cModelMag, 
         scisql_nanojanskyToAbMagSigma(z_cModelFlux, z_cModelFluxErr) AS z_cModelMagErr, 
         scisql_nanojanskyToAbMag(y_cModelFlux) AS y_cModelMag,
         scisql_nanojanskyToAbMagSigma(y_cModelFlux, y_cModelFluxErr) AS y_cModelMagErr, 
  FROM dp02_dc2_catalogs.Object 
  WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), 
        CIRCLE('ICRS', 62, -37, 0.167)) =1 
        AND (detect_isPrimary =1 AND refExtendedness =1 
             AND u_cModelFlux >360 AND g_cModelFlux >360 
             AND r_cModelFlux >360 AND i_cModelFlux >360 
             AND z_cModelFlux >360 AND y_cModelFlux >360)


For a demonstration of how to convert fluxes to magnitudes after a query is executed,
see the tutorial on how to use the results table data.

Return to the list of DP0.2 :ref:`DP0-2-Tutorials-Portal`.
