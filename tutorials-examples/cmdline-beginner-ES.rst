.. Revisar el README para obtener instrucciones sobre cómo contribuir.
.. Revisar la guía de estilo para mantener un enfoque consistente en la documentación.
.. Los objetos estáticos, como las figuras, deben almacenarse en el directorio _static. Revisar _static/README para obtener instrucciones sobre cómo contribuir.
.. No eliminar los comentarios que describen cada sección. Se incluyen para brindar orientación a los colaboradores.
.. No eliminar otro contenido proporcionado en las plantillas, como por ejemplo una sección. En su lugar, comentar el contenido y agregar comentarios para explicar la situación. Por ejemplo:
  - Si no se necesita una sección dentro de la plantilla, comentar el título de la sección y la referencia de la etiqueta. No eliminar el título de sección esperado, la referencia ni los comentarios relacionados proporcionados por la plantilla.
  - Si un archivo no puede incluir un título (rodeado por ampersands (#)), comentar el título desde la plantilla e incluir un comentario explicando por qué se implementa esto (además de aplicar la directiva ``title``).

.. Esta es la etiqueta que se puede utilizar para hacer referencia cruzada a este archivo.
.. El formato recomendado para todas las etiquetas es "Nombre del Directorio"-"Nombre del Título" -- Los espacios deben reemplazarse por guiones.
.. _Tutorials-Examples-DP0-2-Cmndline-Beginner-ES:
.. Cada sección debe incluir una etiqueta para hacer referencia cruzada a una área específica.
.. El formato recomendado para todas las etiquetas es "Nombre del Título"-"Nombre de la Sección" -- Los espacios deben reemplazarse por guiones.
.. Para hacer referencia a una etiqueta que no está asociada con un objeto reST, como un título o una figura, se debe incluir el enlace y el título explícito utilizando la sintaxis :ref:`texto del enlace <nombre-de-la-etiqueta>`.
.. Una advertencia alertará sobre etiquetas idénticas durante el proceso de verificación de enlaces.

############################################
01 (ES). Introducción a DP0.2 (principiante)
############################################

.. Esta sección debería ofrecer una descripción breve y de alto nivel de la página.
.. This section should provide a brief, top-level description of the page.

**Faceta del RSP:** Notebook (línea-de-comandos en la terminal)

.. **RSP Aspect:** Notebook (terminal command-line)

**Autoría:** Gloria Fonseca Alvarez

.. **Contact author:** Gloria Fonseca Alvarez

**Última verificación de ejecución:** 11 sep 2023

.. **Last verified to run:** Sep 11 2023


**Versión de las pipelines científicas de LSST::** Weekly 2023_35

.. **!!!LSST Science Pipelines!!!{uso traducción del glosario} version:** !!!Weekly!!! 2023_35

**Nivel de aprendizaje:** Principiante

.. **!!!Targeted!!! learning level:** Beginner

**Tamaño del contenedor (Container size):** medium

**Introducción:**
Este tutorial es una introducción a las funcionalidades de la terminal y línea de comandos de la plataforma científica de Rubin (Rubin Science Plataform - RSP).
Es paralelo al tutorial de Jupyter Notebook "Introducción a DP02" y muestra cómo utilizar el servicio TAP para consultar y recuperar datos del catálogo;
usar matplotlib para graficar los datos de un catálogo; el paquete Butler de LSST para consultar y recuperar datos de imágenes.

.. This tutorial is an introduction to the terminal and command line functionality within the Rubin Science Platform.
.. It is parallel to the Jupyter Notebook tutorial "Introduction to DP02" and demonstrates how to use the TAP service to query and retrieve catalog data;
.. matplotlib to plot catalog data; the LSST Butler package to query and retrieve image data; and the LSST afwDisplay image package.

Este tutorial usa el conjunto de datos Vista previa de datos 0.2 (DP0.2 - Data Preview 0.2).
Este conjunto de datos utiliza un subconjunto de las imágenes simuladas del Desafío de datos 2 de DESC (DC2 - DESC's Data Challenge 2), las cuales han sido reprocesadas por el Observatorio de Rubin usando la versión 23 de las pipelines científicas del LSST (LSST Science Pipelines).
Se puede encontrar más información sobre los datos simulados en el `artículo científico de DC2 <https://ui.adsabs.harvard.edu/abs/2021ApJS..253...31L/abstract>`_ de DESC y en la `documentación del lanzamiento de datos de DP0.2 <https://dp0-2.lsst.io>`_.

.. This tutorial uses the Data Preview 0.2 (DP0.2) data set.
.. This data set uses a subset of the DESC's Data Challenge 2 (DC2) simulated images, which have been reprocessed by Rubin Observatory using Version 23 of the LSST Science Pipelines.
.. More information about the simulated data can be found in the DESC's `DC2 paper <https://ui.adsabs.harvard.edu/abs/2021ApJS..253...31L/abstract>`_ and in the `DP0.2 !!!data release!!! documentation <https://dp0-2.lsst.io>`_.


.. _DP0-2-Cmndline-Beginner-ES-Step-1:

Paso 1. Acceso a la terminal y configuración
============================================

.. Step 1. Access the terminal and setup
.. =====================================

1.1. Iniciar sesión en la Faceta Notebook. La terminal es un subcomponente de la Faceta Notebook.

.. 1.1. Log in to the Notebook Aspect. The terminal is a subcomponent of the Notebook Aspect.

1.2. En la ventana de lanzadores abajo de "Other", seleccionar la "Terminal".

.. 1.2. In the launcher window under "Other", select the terminal.


.. figure:: /_static/other_terminal.png
	:alt: Opciones visibles en la sección del lanzador titulada "Other" dentro de la faceta notebook.
		Las selecciones desde la izquierda son: lanzador de terminal, archivo de texto, archivo de markdown, archivo de Python y un botón de ayuda.

.. :alt: Options visible in the section of the launcher entitled other within the notebook aspect.  
.. Selections from the left are: terminal launcher, text file, markdown file, python file, and a help button. 

1.3. Configurar el entorno del Observatorio de Rubin.

.. 1.3. Set up the !!!Rubin Observatory!!!{no se si es un producto también} environment.

.. code-block::

    setup lsst_distrib

1.4. Iniciar una sesión interactiva de Python.

.. 1.4. Start an interactive Python session.

.. code-block::

    python


.. _DP0-2-Cmndline-Beginner-ES-Step-2:

Paso 2. Importar paquetes
=========================

.. Step 2. Import packages
.. =======================

Este tutorial hace uso de numerosos paquetes que serán utilizados con frecuencia cuando se interactúe con los datos de catálogos y de las imágenes.

.. This tutorial makes use of several packages that will be commonly used when interacting with catalog and image data. 

2.1. Importar paquetes generales de python.

.. 2.1. Import general python packages.

.. code-block::

    import numpy
    import matplotlib
    import matplotlib.pyplot as plt

2.2. Importar paquetes necesarios para acceder a los datos de los catálogos.

.. 2.2. Import packages needed to access the catalog data.

.. code-block::

    import pandas 
    pandas.set_option('display.max_rows', 1000)
    from lsst.rsp import get_tap_service, retrieve_query

2.3. Importar paquetes necesarios para acceder a imágenes.

.. 2.3. Import packages needed to access images.

.. code-block::

    import lsst.daf.butler as dafButler
    import lsst.geom
    import lsst.afw.display as afwDisplay



.. _DP0-2-Cmndline-Beginner-ES-Step-3:

Paso 3. Recuperar datos usando TAP para 10 objetos
==================================================

.. Step 3. Retrieve data using TAP for 10 objects
.. ==============================================

El protocolo de acceso a datos tabulados TAP (Table Access Protocol) provee acceso estandarizado a los datos de los catálogos para exploración, búsqueda y recuperación.
`La documentación completa para TAP <https://www.ivoa.net/documents/TAP/20190927/index.html>`_ es provista por la Alianza Internacional del Observatorio Virtual (IVOA - International Virtual Observatory Alliance).
El servicio TAP utiliza un lenguaje de consultas similar a SQL (Structured Query Language - lenguaje de consulta estructurado) denominado ADQL (Astronomical Data Query Language - lenguaje de consulta de datos astronómicos).
La `documentación para ADQL <https://www.ivoa.net/documents/latest/ADQL.html>`_ incluye más información sobre sintaxis y palabras clave.

.. Table Access Procotol (TAP) provides standardized access to the catalog data for !!!discovery!!!, search, and retrieval.
.. `Full documentation for TAP <https://www.ivoa.net/documents/TAP/20190927/index.html>`_ is provided by the International Virtual Observatory Alliance (IVOA).
.. The TAP service uses a query language similar to SQL (Structured Query Langage) called ADQL (Astronomical Data Query Language).
.. The `documentation for ADQL <https://www.ivoa.net/documents/latest/ADQL.html>`_ includes more information about syntax and keywords.

Aviso: No están soportadas por RSP todas las funcionalidades de ADQL para la vista previa de datos 0 (DP0).

.. Notice: Not all ADQL functionality is supported by the RSP for Data Preview 0.


Este ejemplo utiliza el Catálogo de Objetos DP0.2, que contiene fuentes detectadas en las imágenes combinadas (también llamadas imágenes apiladas, combinadas o deepCoadd).

.. This example uses the DP0.2 Object catalog, which contains sources detected in the !!!coadded images!!! (also called stacked, combined, or !!!deepCoadd!!!{se deja sin traducir} images).

3.1. Iniciar el servicio TAP.

.. 3.1. Start the TAP service .

.. code-block::

    service = get_tap_service("tap")
    
3.2. Definir las coordenadas para una búsqueda de cono centrada alrededor de la región cubierta por la simulación DC2 (RA,Dec = 62,-37).

.. 3.2. Define the coordinates for a cone search centered around the region covered by the DC2 simulation (RA,Dec = 62,-37).

.. code-block::

    use_center_coords = "62, -37"

3.3. Crear una consulta llamada my_adql_query para obtener las coordenadas y las magnitudes g, r, i para objetos contenidos dentro de 0.5 grados de las coordenadas centrales.

.. 3.3. Create a query named my_adql_query to retrieve the coordinates and g, r, i magnitudes for objects !!!within!!!{revisar si "contenidos dentro" está bien} 0.5 degrees of the center coordinates.

.. code-block:: 

   my_adql_query = "SELECT TOP 10 coord_ra, coord_dec, detect_isPrimary, " + \
                "r_calibFlux, r_cModelFlux, r_extendedness " + \
                "FROM dp02_dc2_catalogs.Object " + \
                "WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), " + \
                "CIRCLE('ICRS', " + use_center_coords + ", 0.5)) = 1 "

3.4. Recuperar y visualizar los resultados de la consulta para 10 objetos.

.. 3.4. Retrieve and display the results of the query for 10 objects.

.. code-block::

    results = service.search(my_adql_query)
    results_table = results.to_table()
    print(results_table)   

3.5. Convertir flujos en magnitudes.

.. 3.5. Convert fluxes !!!into!!!{"a" o "en"?} magnitudes.

Los catálogos de objetos y fuentes almacenan sólo flujos.
Hay cientos de columnas relacionadas a flujos, y almacenarlas también como magnitudes sería redundante, y un desperdicio de espacio.
Todas las unidades de flujos son nanojanskys (nJy).
Para convertir nJy a magnitudes AB usar: |mab| = -2.5log(|fnJy|) + 31.4. 

.. |mab| replace:: m\ :sub:`AB`\ 
.. |fnJy| replace:: f\ :sub:`nJy`\


.. The object and source catalogs store only fluxes.
.. There are hundreds of flux-related columns, and to store them also as magnitudes would be redundant, and a waste of space.
.. All flux units are nanojanskys (nJy).
.. To convert nJy to AB magnitudes use: |mab| = -2.5log(|fnJy|) + 31.4. 

Agregar columnas de magnitudes después de recuperar columnas de flujo.

.. Add columns of magnitudes after retrieving columns of flux.

.. code-block::
   
     results_table['r_calibMag'] = -2.50 * numpy.log10(results_table['r_calibFlux']) + 31.4
     results_table['r_cModelMag'] = -2.50 * numpy.log10(results_table['r_cModelFlux']) + 31.4
     
Visualizar la tabla de resultados incluyendo las magnitudes.

.. Display the results table including the magnitudes.

.. code-block::

    print(results_table) 



.. _DP0-2-Cmndline-Beginner-ES-Step-4:

Paso 4. Recuperar datos usando TAP para 10,000 objetos
======================================================

.. Step 4. Retrieve data using TAP for 10,000 objects
.. ==================================================


Para obtener las columnas correspondiente a flujos como magnitudes con una consulta ADQL, se puede hacer lo siguiente:
scisql_nanojanskyToAbMag(g_calibFlux) as g_calibMag,
y las columnas de errores de magnitud se pueden obtener haciendo:
scisql_nanojanskyToAbMagSigma(g_calibFlux, g_calibFluxErr) as g_calibMagErr.

.. To retrieve columns of fluxes as magnitudes in an ADQL query, !!!users!!!{omito usar la traducción usuario porque no encuentro una forma inclusiva no rebuscada de palabra equivalente} can do this:
.. scisql_nanojanskyToAbMag(g_calibFlux) as g_calibMag,
.. and columns of !!!magnitude errors!!! can be retrieved with:
.. scisql_nanojanskyToAbMagSigma(g_calibFlux, g_calibFluxErr) as g_calibMagErr.

4.1. Recuperar las magnitudes de las bandas g, r e i para 10000 objetos puntuales.
 
.. 4.1. Retrieve g-, r- and i-band magnitudes for 10000 !!!point-like objects!!!.

A la búsqueda de cono realizada en la consulta, agregarle como restricciones que detect_isPrimary sea True (esto excluirá fuentes "hijas" producto de separación - *deblending*), que el flujo calibrado sea mayor que 360 nJy (aproximadamente magnitud 25), y que los parámetros de extensión sean 0 (fuentes puntuales).

.. In addition to a cone search, impose query restrictions that detect_isPrimary is True (this will not return !!!deblended "child" sources!!), that the !!!calibrated flux!!! is greater than 360 nJy (about 25th mag), and that the !!!extendedness parameters!!! are 0 (!!!point-like sources!!!).

.. code-block::

 results = service.search("SELECT TOP 10000 coord_ra, coord_dec, "
                         "scisql_nanojanskyToAbMag(g_calibFlux) as g_calibMag, "
                         "scisql_nanojanskyToAbMag(r_calibFlux) as r_calibMag, "
                         "scisql_nanojanskyToAbMag(i_calibFlux) as i_calibMag, "
                         "scisql_nanojanskyToAbMagSigma(g_calibFlux, g_calibFluxErr) as g_calibMagErr "
                         "FROM dp02_dc2_catalogs.Object "
                         "WHERE CONTAINS(POINT('ICRS', coord_ra, coord_dec), "
                         "CIRCLE('ICRS', "+use_center_coords+", 1.0)) = 1 "
                         "AND detect_isPrimary = 1 "
                         "AND g_calibFlux > 360 "
                         "AND r_calibFlux > 360 "
                         "AND i_calibFlux > 360 "
                         "AND g_extendedness = 0 "
                         "AND r_extendedness = 0 "
                         "AND i_extendedness = 0")

4.2. Almacenar los datos como un objeto *dataframe* (marco de datos) de Pandas.

.. 4.2. Store the data as a pandas !!!dataframe!!!{elijo aclarar que es un objeto}. 

.. code-block::
    
    results_table = results.to_table()
    data = results_table.to_pandas()



.. _DP0-2-Cmndline-Beginner-ES-Step-5:

Paso 5. Hacer un diagrama color-magnitud
========================================

.. Step 5. Make a color-magnitude diagram
.. ======================================


5.1. Graficar el color (magnitudes r-i) vs magnitud g.

.. 5.1. Plot the color !!!(r-i magnitudes)!!! vs g magnitude.

.. code-block::

    plt.plot(data['r_calibMag'].values - data['i_calibMag'].values,
         data['g_calibMag'].values, 'o', ms=2, alpha=0.2)
	 
5.2. Definir las etiquetas de los ejes y los límites.

.. 5.2. Define the axis labels and limits.

.. code-block::

    plt.xlabel('mag_r - mag_i', fontsize=16)
    plt.ylabel('mag_g', fontsize=16)
    plt.xticks(fontsize=16)
    plt.yticks(fontsize=16)

    plt.xlim([-0.5, 2.0])
    plt.ylim([25.5, 16.5])

5.3.Guardar el gráfico en formato pdf.

.. 5.3. Save the plot as a pdf.

.. code-block::

    plt.savefig('color-magnitude.pdf')

Utilizar el navegador de archivos en el lado izquierdo de la Faceta Notebook para navegar hasta el archivo "color-magnitude.pdf"
Hacer doble clic sobre el nombre de archivo para abrirlo y ver el gráfico.

.. Use the file navigator on the left-hand side of the Notebook Aspect to navigate to the file "color-magnitude.pdf".
.. Double click on the filename to open and view the plot.
    
.. figure:: /_static/cl_color-magnitude.jpg
	:alt: Diagrama color-magnitud que grafica en el eje y la magnitud g y en el eje x el color magnitud r menos magnitud i
		Hay una serie de bandas verticales que representan varios colores magnitud, que van desde 0.6 hasta 1.7. Esta característica es única de este conjunto de datos simulados.

.. alt: Color-magnitude diagram plotting magnitude g on the y-axis and !!!magnitude r minus magnitude i color!!! on the x-axis.  
.. There are a number of vertical bands representing various !!!color magnitudes!!! ranging from 0.6 to 1.7.  This feature is unique to this simulated data set. 

.. _DP0-2-Cmndline-Beginner-ES-Step-6:

Paso 6. Recuperar los datos de imágenes usando Butler
=====================================================

.. Step 6. Retrieve image data using the butler
.. ============================================

Los dos tipos de imágenes más comunes con los que van a interactuar los delegados y delegadas de DP0 son calexps y deepCoadds.

.. !!!The two most common types of images!!! that DP0 !!!delegates!!!{no encontre alternativa sin genero} will interact with are !!!calexps!!!{sin traducción por glosario} and !!!deepCoadds!!!{sin traducción por glosario}.

calexp: Una única imagen con un único filtro.

.. calexp: A single image in a single filter.

deepCoadd: Una combinación de imágenes individuales en pila profunda o coagregada.

.. deepCoadd: A combination of single images into a deep stack or !!!Coadd!!!{no estoy seguro de usar la traducción del glosario pero así lo hice tambien en las notebooks}.

Las pipelines científicas LSST (Science Pipelines) procesan y almacenan imágenes en regiones y parcelas. Para obtener y mostrar una imagen en una coordenada deseada, los usuarios deben especificar su tipo de imagen, región (tract) y parcela (patch).

.. The LSST Science Pipelines processes and stores images in !!!tracts!!!{traduzco} and !!!patches!!!{traduzco}. To retrieve and display an image at a desired coordinate, users have to specify their image type, !!!tract!!!{traduzco}, and !!!patch!!!{traduzco}.

región: Una porción del cielo dentro de la teselación del cielo completo (mapa del cielo) de LSST (LSST all-sky tessellation) ; dividido en parcelas.

.. !!!tract!!!{pensar si conviene no traducir para que respete el código}: A portion of sky within the !!!LSST all-sky tessellation (sky map)!!!{en glosario de tract aparece tal cual}; divided into patches.

parcela: Una subregión cuadrilátera de una región, de un tamaño que se ajusta fácilmente en la memoria de las computadoras de escritorio.

.. !!!patch!!!{pensar si conviene no traducir para que respete el código}: A quadrilateral sub-region of a tract, of a size that fits easily into memory on desktop computers.

Butler - que en inglés significa mayordomo - (`documentación de butler <https://pipelines.lsst.io/modules/lsst.daf.butler/index.html>`_) es un paquete de software de las pipelines científicas de LSST para obtener datos de LSST sin necesidad de conocer su ubicación o formato. Además Butler también puede ser utilizado para explorar y descubrir qué datos existen. Otros tutoriales muestran la funcionalidad completa de Butler.

.. !!!The!!!{saco el artículo} butler (`butler documentation <https://pipelines.lsst.io/modules/lsst.daf.butler/index.html>`_) is an !!!LSST Science Pipelines!!!{glosario} software package to fetch LSST data without having to know its location or format. The butler can also be used to explore and discover what data exists. Other tutorials demonstrate the full butler functionality.

6.1. Definir una configuración y colección de Butler.

.. 6.1. !!!Define a butler configuration and collection!!!.

.. code-block::

    butler = dafButler.Butler('dp02', collections='2.2i/runs/DP0.2')

6.2. Definir las coordenadas de un cúmulo de galaxias conocido en DC2.

.. 6.2. Define the coordinates of a known !!!galaxy cluster!!! in the DC2. 

.. code-block::

    my_ra_deg = 55.745834
    my_dec_deg = -32.269167

6.3. Usar lsst.geom para definir un SpherePoint (punto de esfera) para las coordenadas del cúmulo (`documentación de lsst.geom <https://pipelines.lsst.io/modules/lsst.geom/index.html>`_).

.. 6.3. Use lsst.geom to define a SpherePoint for the cluster's coordinates (`lsst.geom documentation <https://pipelines.lsst.io/modules/lsst.geom/index.html>`_).

.. code-block::

    my_spherePoint = lsst.geom.SpherePoint(my_ra_deg*lsst.geom.degrees, my_dec_deg*lsst.geom.degrees)
    print(my_spherePoint)

6.3. Recuperar el mapa de cielo (skymap) de DC2 (`documentación de skymap <https://pipelines.lsst.io/modules/lsst.skymap/index.html>`_) e identificar el región y parcela (tract y patch).

.. !!!6.3.!!!{SE REPITE EL 6.3} Retrieve the !!!DC2 skymap!!! (`skymap documentation <https://pipelines.lsst.io/modules/lsst.skymap/index.html>`_) and identify the !!!tract!!!{traduzco ya que se menciona anteriormente tambien como tract} and !!!patch!!!{misma situacion que con tract}.

.. code-block::

    skymap = butler.get('skyMap')
    tract = skymap.findTract(my_spherePoint)
    patch = tract.findPatch(my_spherePoint)

    my_tract = tract.tract_id
    my_patch = patch.getSequentialIndex()

    print('my_tract: ', my_tract)
    print('my_patch: ', my_patch)

6.4. Utiliza Butler para recuperar la deepCoadd en la banda i.

.. 6.4. Retrieve the !!!deep i-band Coadd!!!{viendo el código de abajo, entiendo que se refiere a una deepCoadd la cual en el glosario se indca que se deja sin traducción, pero no me queda 100% claro}.

.. code-block::

    dataId = {'band': 'i', 'tract': my_tract, 'patch': my_patch}
    my_deepCoadd = butler.get('deepCoadd', dataId=dataId)


.. _DP0-2-Cmndline-Beginner-ES-Step-7:

Paso 7. Visualizar la imagen
============================

.. Step 7. Display the image
.. =========================

Los datos de imágenes recuperados con Butler se pueden visualizar de muchas formas distintas.

.. Image data retrieved with the butler can be displayed several different ways.

7.1. Visualizar la imagen usando afwDisplay (`documentación de afwDisplay <https://pipelines.lsst.io/modules/lsst.afw.display/index.html>`_).

.. 7.1. Display the image using afwDisplay (`afwDisplay documentation <https://pipelines.lsst.io/modules/lsst.afw.display/index.html>`_).

.. code-block::

    afwDisplay.setDefaultBackend('matplotlib')

.. code-block::
    
    fig = plt.figure(figsize=(10, 8))
    afw_display = afwDisplay.Display(1)
    afw_display.scale('asinh', 'zscale')
    afw_display.mtv(my_deepCoadd.image)
    plt.gca().axis('on')
    plt.savefig('my_deepCoadd.pdf')

Utilizar el navegador de archivos en el lado izquierdo de la Faceta Notebook para navegar hasta el archivo "my_deepCoadd.pdf"
Hacer doble clic sobre el nombre de archivo para abrirlo y ver el gráfico.

    
.. Use the file navigator on the left-hand side of the Notebook Aspect to navigate to the file "my_deepCoadd.pdf".
.. Double click on the filename to open and view the image.
    
.. figure:: /_static/cl_my-deep-Coadd.jpg
	:alt: Una captura de pantalla de cuatro mil por cuatro mil píxeles de una imagen astronómica que ha sido graficada en una Jupyter notebook.
		Una gran concentración de puntos alargados se encuentra en el cuadrante inferior izquierdo y sugiere un cúmulo de galaxias.
  
.. :alt: A !!!four thousand by four thousand pixel screen capture!!!{en realidad no es la captura que tiene 4mil x 4mil sino la imagen astronómica cruda que de todas formas esta comprimida para entrar dentro del gráfico de la notebook} of an astronomical image that has been plotted in a Jupyter notebook.  
..  A large concentration of elongated points is concentrated at the lower-left quadrant and suggests a cluster of galaxies.  
    
7.2. Visualizar la imagen usando Firefly (`documentación de Firefly <https://pipelines.lsst.io/modules/lsst.display.firefly/index.html>`_).

.. 7.2. Display the image using Firefly (`Firefly documentation <https://pipelines.lsst.io/modules/lsst.display.firefly/index.html>`_).

.. code-block::

    afwDisplay.setDefaultBackend('firefly')
    afw_display = afwDisplay.Display(frame=1)
    afw_display.mtv(my_deepCoadd)
   
Opcional: Para una demostración de la interfaz interactiva de Firefly, revisa "03b Visualización de imágenes con Firefly" del :ref:`DP0-2-Tutorials-Notebooks`.

.. Optional: For a demonstration of the Firefly interactive interface, work through !!!"03b Image Display with Firefly" of the :ref:`DP0-2-Tutorials-Notebooks`.!!!{referenciaremos a una futura versión traducida o al que ahora está en ingles?}

7.3. Cuando estés listo, salir de python para regresar a la línea de comando normal.

.. 7.3. When you're done, exit python to return to the regular command line.

.. code-block::

    exit()

