.. Revisar el README para obtener instrucciones sobre cómo contribuir.
.. Revisar la guía de estilo para mantener un enfoque consistente en la documentación.
.. Los objetos estáticos, como las figuras, deben almacenarse en el directorio _static. Revisar _static/README para obtener instrucciones sobre cómo contribuir.
.. No eliminar los comentarios que describen cada sección. Se incluyen para brindar orientación a los colaboradores.
.. No eliminar otro contenido proporcionado en las plantillas, como por ejemplo una sección. En su lugar, comentar el contenido y agregar comentarios para explicar la situación. Por ejemplo:
  - Si no se necesita una sección dentro de la plantilla, comentar el título de la sección y la referencia de la etiqueta. No eliminar el título de sección esperado, la referencia ni los comentarios relacionados proporcionados por la plantilla.
  - Si un archivo no puede incluir un título (rodeado por ampersands (#)), comentar el título desde la plantilla e incluir un comentario explicando por qué se implementa esto (además de aplicar la directiva ``title``).

.. Esta es la etiqueta que se puede utilizar para hacer referencia cruzada a este archivo.
.. El formato recomendado para todas las etiquetas es "Nombre del Directorio"-"Nombre del Título" -- Los espacios deben reemplazarse por guiones.
.. _Tutorials-Examples-DP0-2-Portal-Beginner-ES:
.. Cada sección debe incluir una etiqueta para hacer referencia cruzada a una área específica.
.. El formato recomendado para todas las etiquetas es "Nombre del Título"-"Nombre de la Sección" -- Los espacios deben reemplazarse por guiones.
.. Para hacer referencia a una etiqueta que no está asociada con un objeto reST, como un título o una figura, se debe incluir el enlace y el título explícito utilizando la sintaxis :ref:`texto del enlace <nombre-de-la-etiqueta>`.
.. Una advertencia alertará sobre etiquetas idénticas durante el proceso de verificación de enlaces.

#######################################################################
01 (ES). Diagrama color-magnitud de estrellas brillantes (principiante)
#######################################################################

.. 01. Bright Stars !!!Color-Magnitude!!!{Melissa tradujo magnitud-color y no color-magnitud} Diagram (beginner)

.. Esta sección debería ofrecer una descripción breve y de alto nivel de la página.
.. This section should provide a brief, top-level description of the page.

**Faceta del RSP:** Portal

.. **RSP Aspect:** Portal

**Autoría:** Melissa Graham y Greg Madejski

.. **Contact authors:** Melissa Graham and Greg Madejski

**Última verificación de ejecución:** 2023-04-07

.. **Last verified to run:** 2023-04-07

**Nivel de aprendizaje:** principiante

.. **!!!Targeted!!! learning level:** beginner

**Introducción:**
Este tutorial utiliza la interfaz Consulta de Tabla Única (Single-Table Query) para buscar estrellas brillantes en una región pequeña del cielo
y luego utiliza la interfaz de Resultados (Results) para crear un diagrama color-magnitud.
Este es el mismo ejemplo usado para ilustrar el servicio de Protocolo de Acceso de Tablas (Table Access Protocol - TAP) en el primer tutorial de :ref:`DP0-2-Tutorials-Notebooks-ES`.
Principiantes que busquen una visión más general de la Faceta Portal pueden consultar :doc:`/data-access-analysis-tools/portal-intro`.

.. **Introduction:**

.. This tutorial uses the !!!Single-Table Query interface!!! to search for bright stars in a small region of sky,
   and then uses the !!!Results interface!!! to create a color-magnitude diagram.
   This is the same demonstration used to illustrate the Table Access Protocol (TAP) service in the first of the !!!:ref:`DP0-2-Tutorials-Notebooks`!!!{debería referenciar a versión español}
   Beginner-level !!!users!!!{suprimo por genero} looking for a more general overview of the Portal Aspect should refer to this !!!:doc:`/data-access-analysis-tools/portal-intro`!!!
 
.. _DP0-2-Portal-Beginner-ES-Step-1:

Paso 1. Establecer las restricciones de la consulta
===================================================

.. Step 1. Set the !!!query constraints!!!
.. =================================


1.1. Iniciar sesión en la Faceta Portal.

.. 1.1. Log in to the !!!Portal Aspect!!!{glosario}.

1.2. Debajo de "TAP Searches" (búsquedas TAP), dejar la casilla "Use Image Search (ObsTAP)" sin marcar y dejar la configuración de "View" con su valor por defecto "UI assisted".

.. 1.2. Under "TAP Searches", leave the "Use Image Search (ObsTAP)" box unchecked, and leave "View" at its default "UI assisted".

1.3. A la derecha de "LSST DP0.2 DC2 Tables", elegir en "Table Collection" el conjunto de tablas "dp02_dc2_catalogs" (menú desplegable de la izquierda) y en "Table" la tabla "dp02_dc2_catalogs.Object" (menú desplegable de la derecha).

.. 1.3. Next to "LSST DP0.2 DC2 Tables", choose the !!!Table Collection!!! to be "dp02_dc2_catalogs" (left drop-down menu) and the Table to be "dp02_dc2_catalogs.Object" (right drop-down menu).
.. Acá se usa "Table Colection" para identificar el menu desplegable pero también indicando que se está eligiendo dentro de la colección de tablas, por eso agrego "el conjunto de tablas" a la traducción

1.4. En la sección de restricciones, debajo de "Enter Constraints", marcar la casilla de verificación a la izquierda de "Spatial" para usar restricciones espaciales.
Dejar "Shape Type" (el tipo de forma) con su valor por defecto "Cone" (cono), y para las coordenadas/nombre de objeto en "Coords or Obj Name" usar las coordenadas centrales del área de simulación de DC2 "62, -37".
En el menú desplegable al lado de "Radius", elegir "degrees" *y luego* ingresar "1" en el cuadro de texto y presionar la tecla *enter* para establecer la búsqueda con radio de 1 grado.

.. 1.4. Under "Enter Constraints", select the box to the left of "Spatial".
   Leave the "Shape Type" as the default "Cone", and for "Coords or Obj Name" use the central coordinates of the DC2 simulation area "62, -37".
   Next to "Radius", from the drop down menu choose "degrees" *and then* enter "1" in the box and press !!!enter!!!{quizás traducir como <tecla "entrar">?} to set the search radius to 1 degree.

1.5. En la tabla de la derecha, debajo de "Output Column Selection and Constraints" (Selección de Columnas de Salida y Restricciones), hacer clic en las casillas de la primera columna a la izquierda para seleccionar "coord_ra", "coord_dec", "detect_isPrimary", "g" "r" e "i_calibFlux", y "g" "r" e "i_extendedness". Se pueden buscar los nombres de columnas. Para evitar recorrer una larga lista de columnas,
ingresar una palabra clave (e.g., "calibFlux") en el cuadro justo debajo de la columna "Name". Se listarán todos los nombres de columnas que contengan la palabra clave ingresada.
Después de seleccionar las columnas que se necesiten (e.g., "g" "r" e "i_calibFlux"), borrar el cuadro de texto y presionar *enter* para continuar seleccionando otras columnas.
Hacer clic en el símbolo de embudo en la parte superior de la columna de casillas de verificación para filtrar la vista de tabla y mostrar sólo las columnas seleccionadas.

.. 1.5. In the table at right, under "Output Column Selection and Constraints", click the box in the left-most column to select "coord_ra", "coord_dec", "detect_isPrimary", "g" "r" and "i_calibFlux", and "g" "r" and "i_extendedness". Column names are searchable. To avoid !!!scrolling!!! a long column list,
   enter a keyword (e.g., "calibFlux") in the box right below the "Name" column. It will list all the column names containing the given keyword.
   After selecting the needed columns (e.g., "g" "r" and "i_calibFlux"), clear the box and hit the return key to continue selecting other columns.
   Click on the funnel symbol at the top of the checkbox column to filter the table view to show selected columns only.

1.6. En la columna de restricciones "constraints", ingresar "=1" para "detect_isPrimary", ">360" para los flujos ("g" "r" e "i_calibFlux"), y "=0" para los parámetros de extensión (extendedness)
Esto va a limitar los objetos obtenidos a aquellos sin hijos (i.e. componentes resultantes de la separación [deblending]), que son más brillantes que aproximadamente 25 magnitudes
en los filtros g, r e i, y que parecen ser puntuales (no extendidos, pero *no necesariamente estelares*) en esos tres filtros también.

.. 1.6. In the "constraints" column, enter "=1" for the "detect_isPrimary", ">360" for the fluxes, and "=0" for the !!!extendedness!!! parameters.
   This will limit the objects returned to those !!!with no children!!! (i.e., the products of !!!deblending!!!), which are brighter than about 25th magnitude
   in the g, r, and i filters, and which appear to be !!!point-like!!! (not extended, but *not necessarily stellar*) in those three filters as well.
.. No sé cómo se traduce "extendedness" en el contexto de astronomía
.. No estoy seguro en "... limitar los objetos obtenidos a aquellos sin hijos..." si es correcta la traducción de "with no children" en contexto de astronomía
.. No estoy seguro de cómo se traduce "deblending"
.. No estoy seguro de "point-like" lo traduzco como puntual

En este punto las casillas que seleccionan los parámetros de "extendedness" y "detect_isPrimary" pueden ser desmarcadas ya que
no es necesario para este tutorial recopilar los datos de estas columnas, sino que sólo se busca restringir la consulta basándose en sus valores.

.. At this point the boxes selecting the "extendedness" and "detect_isPrimary" parameters can be unchecked, because
   it is not necessary for this tutorial to actually retrieve the data in those columns, only to constrain the query based on their values.

**Aviso:** En este punto, con la consulta configurada en su totalidad, haciendo clic en "Populate and Edit ADQL" (rellenar y editar ADQL) se cambiará el Tipo de Consulta a "Edit ADQL" y se llenará el cuadro "ADQL Query" con la consulta, como se muestra en el Paso 3 más abajo.

.. **Notice:** At this point, with the query all set up, clicking !!!"Populate and Edit ADQL"!!! will switch the Query Type to "Edit ADQL" and populate the ADQL query box, as shown in Step 3 below.

1.7. Establecer el límite de filas en "Row Limit" a 10000, para solo obtener 10000 objetos para esta demostración.

.. 1.7. Set the !!!"Row Limit"!!! to 10000, to only retrieve 10000 objects for this demonstration.

.. figure:: /_static/portal_tut01_step01.png
	:name: portal_tut01_step01
	:alt: Una captura de pantalla que muestra cómo ingresar criterios de búsqueda en la Faceta Portal.
		El portal es una forma conveniente de consultar la base de datos de Rubin a través de una interfaz gráfica de usuario sin necesidad de usar Python o *scripts* en la línea de comandos.
		Cada fila representa una categoría separada que caracteriza los criterios de búsqueda TAP a utilizar, incluyendo: el servicio TAP; el tipo de consulta;
		la colección de tablas y la tabla específica a utilizar, así como las restricciones a emplear para la consulta. La búsqueda en el portal se puede realizar presionando el botón de búsqueda en la esquina inferior izquierda.
	
	La captura de pantalla anterior muestra las restricciones antes de hacer clic en "Search".
	

.. alt: A screenshot of how to input search criteria in the !!!portal aspect!!!.
        The portal is a convenient way to query the Rubin database through a graphical user interface without any python or command line scripting.
    		Each row is a separate category characterizing the tap search criteria to be used, including: the tap service; the query type;
        the table collection and specific table to be used and the constraints to be used for the query. The portal search can be performed by hitting the search button on the bottom left.

   The above screenshot shows the constraints before clicking "Search".

1.8. Hacer clic en "Search" en la parte más abajo a la izquierda para realizar la búsqueda.

.. 1.8. Clic "Search" at lower left.


.. _DP0-2-Portal-Beginner-ES-Step-2:

Paso 2. Crear el diagrama color-magnitud
========================================

.. Step 2. Create the color-magnitude diagram
.. ==========================================

La disposición predeterminada "Tri-view" muestra un mapa de cobertura del cielo de la simulación DESC DC2 en la parte superior izquierda (debajo de "Coverage"), un gráfico activo ("Active Chart") que muestra la distribución espacial de los objetos obtenidos
en la parte superior derecha y una tabla con los resultados de la búsqueda en la parte inferior.

.. The default "Tri-view" layout shows a sky !!!coverage map!!! from DESC DC2 simulation at upper left, an !!!active chart!!! showing the spatial distribution of returned
   objects at upper right, and a table of the search results along the bottom.
.. No estoy seguro cómo se traduce "active map" en este contexto, diría interactivo pero en ese caso sería interactive chart...

.. figure:: /_static/portal_tut01_step02a.png
	:name: portal_tut01_step02a
	:alt: Una captura de pantalla de los resultados de la consulta realizada anteriormente.
	
	La vista predeterminada de resultados con "Tri-view".

.. alt: A screenshot of the previous query's results.
..
.. The default Results view with "Tri-view".

2.1. En la esquina superior derecha, hacer clic en "Bi-view Tables"  para mostrar solo el gráfico activo o solo el mapa de cobertura del cielo (alternando entre los dos haciendo clic en la pestaña "Active Chart"/"Coverage") en la parte derecha junto con la tabla en la parte izquierda de la pantalla.

.. 2.1. In the upper right corner, click "Bi-view Tables" to show only either the !!!active chart!!! or the !!!sky coverage map!!! (switching between the two by clicking the tap "Active Chart"/"Coverage") in the right along with the table in the left of the screen.
.. No estoy seguro cómo se traduce "sky coverage map"


**Aviso:** Los objetos obtenidos *no* llenan el área de búsqueda (con radio de 1 grado) en el gráfico activo predeterminado de "coord_ra" versus "coord_dec".
Esto se debe a que se aplicó un límite de filas de 10000 objetos, y los datos están divididos en archivos por coordenadas celestes.
La consulta accedió a estos archivos hasta encontrar 10000 objetos (es decir, la consulta *no* encuentra *todos los objetos* que cumplen con los parámetros de la consulta y luego elige 10000 objetos al azar para devolver).

.. **Notice:** The objects retrieved *do not* fill in the search area (a 1 degree radius) in the default !!!active chart!! of "coord_ra" versus "coord_dec".
    This is because a row limit of 10000 objects was applied, and the data is partitioned into files by !!!sky coordinate!!!.
    The query accessed these files until 10000 objects were found (i.e., the query *does not* find *all objects* that satisfy the query parameters and then choose 10000 random objects to return).
.. No estoy seguro de la traducción de "sky coordinate" como coordenadas celestes

.. figure:: /_static/portal_tut01_step02b.png
	:name: portal_tut01_step02b
	:alt: Esta es una captura de pantalla del portal después de ejecutar una búsqueda de consulta. La imagen superior muestra la densidad de las fuentes seleccionadas dentro del área de búsqueda.
		En este caso, un círculo de radio seleccionado por el usuario centrado en la ascensión recta y declinación elegidas por el usuario.
		El panel inferior muestra los objetos devueltos por la consulta de búsqueda en forma de tabla.
	
	La vista de resultados (Results) con "Bi-view Tables" seleccionado.
	

.. alt: This screenshot of the portal after a search query is run.  The top image shows the density of selected sources within the search area.
       In this case, a circle of radius that is selected by the user centered at the !!!right ascension!!! and declination !!!location!!! selected by the user.
       The bottom panel displays the returned objects from the search query as a table.
..
.. The !!!Results!!!{es el sistema de interfaz de resultados} view with "Bi-view Tables" selected.
.. No estoy seguro de la traducción "right ascension" como "ascensión recta"
.. No estoy seguro del significado de la oración


**Aviso:** Para graficar el color (magnitudes r-i) versus la magnitud (g), los flujos (que están en unidades de nanojansky) se convertirán a magnitudes AB en el siguiente paso. La página `Magnitud AB Wikipedia <https://es.wikipedia.org/wiki/Magnitud_AB>`_ ofrece un recurso conciso para quienes no estén familiarizados con las magnitudes AB y los flujos en unidades de jansky.

.. **Notice:** In order to plot color (r-i magnitude) versus magnitude (g), the fluxes (which are in units of nanojansky) are being converted to AB magnitudes in the next step. The `AB Magnitudes Wikipedia <https://en.wikipedia.org/wiki/AB_magnitude>`_ page provides a concise resource for !!!users who are unfamiliar!!!{alternativa sin género} with AB magnitudes and fluxes in units of janskys.

2.2. Hacer clic en el icono de configuración del gráfico activo (en "Active Chart", los dos engranajes en la esquina superior derecha) para modificar la traza (opción "modify trace"), lo que significa cambiar los parámetros del gráfico.
Establecer "X" como "(-2.5 * log10(r_calibFlux)) - (-2.5 * log10(i_calibFlux))" e "Y" como "-2.5 * log10(g_calibFlux) + 31.4".
Dejar las opciones en "Trace Options" como están y hacer clic en "Chart Options" para mostrar las opciones de gráfico.
Para el título del gráfico, en "Chart title" ingresar "Diagrama Color-Magnitud"; establecer "X Label" (la etiqueta del eje X) como "color (r-i)"; establecer "Y Label" (etiqueta del eje Y) como "magnitud (g)" y debajo en "Options" marcar la casilla correspondiente a "reverse".
Establecer los valores "X Min/Max" en "-0.5" y "2.0", y los valores "Y Min/Max" en "16.5" y "25.5".

.. 2.2. Click on the Active Chart settings icon (two gears, upper right) in order to "modify trace", which means to change the plot parameters.
   Set "X" to be "(-2.5 * log10(r_calibFlux)) - (-2.5 * log10(i_calibFlux))", and "Y" to be "-2.5 * log10(g_calibFlux) + 31.4".
   Leave the options on "Trace Options" as they are, and click on "Chart Options" to show the options.
   For "Chart title" enter !!!"Color-Magnitude Diagram"!!!; set "X Label" to "color (r-i)"; set "Y Label" to "magnitude (g)", and underneath check the "Options" box for "reverse".
   Set the "X Min/Max" values to "-0.5" and "2.0", and the "Y Min/Max" values to "16.5" and "25.5".
.. Dejo como título "Color-Magnitude Diagram" para que coincida con la captura de pantalla.

.. figure:: /_static/portal_tut01_step02c.png
	:name: portal_tut01_step02c
	:alt: Una captura de pantalla de la Faceta Portal que muestra la interfaz que permite crear gráficos a partir de los datos devueltos por la consulta.
		Crear gráficos de esta manera es una forma fácil y funcional de explorar los datos.
		La interfaz permite: ingresar funciones de los datos devueltos para graficar, elegir un esquema de colores, editar la segmentación, crear etiquetas y editar la escala de los ejes.
        :width: 300
	
	Establecer los parámetros del gráfico

.. alt: A screenshot of the portal aspect showing the interface that allows the user to create charts from the data returned by the query.
   		Creating plots from the data in this way is an easy and functional way to explore the data.
      The interface allows !!!the user to!!!{elimino genero}: input functions of the returned data to plot, choose a color scheme, edit the binning, create labels and edit the axis scaling.
.. Set the plot parameters.

2.3. Aplicar los parámetros haciendo clic en "Apply" y luego hacer clic en el botón "Close" para cerrar la ventana, mirar el gráfico color-magnitud.

.. 2.3. Click "Apply" and then "Close" the pop-up window, and look at the color-magnitude plot.

.. figure:: /_static/portal_tut01_step02d.png
	:name: portal_tut01_step02d
	:alt: Una captura de pantalla del gráfico creado a partir de los datos devueltos por la consulta utilizando la interfaz xy de la Faceta Portal.
		El gráfico muestra un diagrama color-magnitud de la magnitud AB en la banda g vs. el color de la banda r menos la banda i, para los objetos devueltos por la consulta.
		Este ejemplo demuestra cómo explorar rápidamente los datos devueltos en la consulta de búsqueda.
		El gráfico muestra una gran densidad de estrellas en colores r-i bajos, y segmentos discretos en colores r-i más rojizos debido a que los datos simulados se
		basan en modelos estelares rojos discretos que se utilizaron como entrada en DP0.2. Se espera que los datos reales muestren, en cambio, una distribución suave de colores.
	
	El diagrama color-magnitud.

.. alt: A screenshot of the chart created from the data returned by the query using the xy interface of the portal aspect.
   The chart shows a color magnitude diagram, !!!g-band AB magnitude vs r-band minus i-band color!!!{REVISAR CARO}, for the objects returned by the search query.
   This example demonstrates how to quickly explore the data returned in the search query.
   The plot shows a large density of stars at low r-i color, and discrete bins at redder r-i color because the simulated data is
   based on discrete red stellar models that were used as input into DP0.2. Real data is expected to instead show a smooth distribution of colors.
.. The color-magnitude diagram.

**Aviso:** El estilo de gráfico predeterminado es un gráfico de dispersión, que es apropiado para nuestro conjunto de datos de tamaño modesto (como los 10000 objetos recuperados aquí).
También es posible crear un histograma bidimensional, apropiado para conjuntos de datos grandes (un "mapa de calor" o "heat map"), que crearemos en el Paso 2.4.

.. **Notice:** The default plot style is a scatter plot, which is appropriate for our data set of a modest size (such as 10000 objects retrieved here).
   It is also possible to create a two-dimensional histogram, appropriate for large data sets (a "heat map") which we will make in Step 2.4.

**Aviso:** Los datos simulados están visiblemente estratificados en el gráfico anterior, y esto no ocurrirá con datos reales.
Las secuencias discretas en colores rojos, (g-i) > 0.5, provienen del procedimiento discretizado utilizado para simular estrellas de baja masa en el conjunto de datos DP0.2.

.. **Notice:** The simulated data is visibly quantized in the above plot, and this will not be the case with real data.
   The discrete sequences at red colors, (g-i) > 0.5, come from the discretized procedure used to simulate low-mass stars in the DP0.2 data set.
.. Reemplacé "cuantizados" por "irregulares" porque la verdad es que no se me ocurre otra, y creo que el sentido de la oración va en ese tono. Sino, pondría "están discretizados" pero usamos la misma palabra dos veces en la siguiente línea.
.. Probamos con la palabra "estratificados" para tratar de describir mejor lo que sucede con los valores que se agrupan fuertemente en valores puntuales sin que haya una transición entre ellos.

2.4. Hacer clic nuevamente en el icono de configuración del gráfico xy (los dos engranajes en la esquina superior derecha), pero esta vez elegir "Add New Chart" para agregar un nuevo gráfico.
Cambiar el tipo de gráfico en "Plot Type" a mapa de calor con la opción "Heatmap" y luego establecer "X" e "Y" con las mismas ecuaciones que en el Paso 2.2.
Utilizar las mismas opciones de gráfico en "Chart Options", pero elegir un nombre distinto para el título del gráfico en "Chart title", tal como "Diagrama Color-Magnitud - Mapa de Calor".

.. 2.4. Click on the !!!xy plot!!!{es la primera vez que llama así a este gráfico en el texto principal del tutorial, anteriormente era el Active Chart} settings icon (two gears, upper right) again, but this time choose "Add New Chart."
   Change the "Plot Type" to "Heatmap", and then set the "X" and "Y" to the same equation as in Step 2.2.
   Use the same "Chart Options" except give it a different "Chart title", such as "Heatmap Color-Magnitude Diagram."
.. !!!Acá para obtener el mismo gráfico que se muestra en la captura en el tutorial se omitieron detalles como elegir GreySeq y 100 en los bins!!!

.. figure:: /_static/portal_tut01_step02e.png
	:name: portal_tut01_step02e
	:alt: Captura de pantalla de la ventana de diálogo donde se pueden establecer los nuevos parámetros del gráfico para el mapa de calor.
        :width: 300
	
	Arriba, establecimos los nuevos parámetros del gráfico mapa de calor.

.. alt: Screenshot of dialog box where !!!the user!!!{omito por genero} can set new chart parameters for the heat map.
..
.. Above, we set the new chart parameters for a heatmap plot.

2.5. Hacer clic en "OK" y "Close", y observar el nuevo gráfico de color-magnitud. Para mayor exhaustividad, es posible que se prefiera actualizar el título del gráfico generado anteriormente a "Diagrama Color-Magnitud - Dispersión" ya que aquel era un gráfico de dispersión.

.. 2.5. Click "OK" and !!!"Close"!!!{al clickear en OK ya se cierra}, and look at the new color-magnitude plot.  For completeness, you might wish to update the title of the plot you generated previously to "Scatter Color-Magnitude Diagram."

.. figure:: /_static/portal_tut01_step02f.png
	:name: portal_tut01_step02f
	:alt: Diagramas color-magnitud generados a partir del gráfico de dispersión y el mapa de calor creados anteriormente.
	
	Los diagramas color-magnitud, incluyendo el gráfico de dispersión previamente creado (izquierda) y el mapa de calor (derecha).

.. alt: Color magnitude diagrams generated from the previously made scatter plot and heatmap.
..
.. The color-magnitude diagrams, including the previously made scatter plot (left) and the heatmap (right).

2.6. Interactuar con el gráfico.
Pasar el *mouse* sobre los puntos de datos en el mapa de cobertura en "Coverage Map" (se verá cómo cambian las coordenadas en la parte inferior del mapa) o en el gráfico activo "Active Chart" (se verá que los valores de x e y aparecen en una ventana emergente).
Al seleccionar una fila en la tabla, ésta aparecerá de un color diferente en el(los) gráfico(s), y viceversa: al seleccionar un punto en un gráfico, se resaltará en la tabla de abajo.

.. 2.6. Interact with the plot.
.. Hover over the data points with a mouse either on the Coverage map (see the coordinates change in the bottom of the map{no veo que eso pase}) or the Active Chart (see the x and y values appear in a pop-up window).
.. Select a row in the table and it appears as a different color in the plot(s), and vice-versa: select a point in a plot and it is highlighted in the table below.

.. _DP0-2-Portal-Beginner-ES-Step-3:

Paso 3. Hacer la misma consulta con ADQL
========================================

.. Step 3. Do the same query with ADQL
.. ===================================

3.1. Borrar los resultados de la búsqueda y regresar a la interfaz principal del Portal.
En la esquina superior derecha, seleccionar la vista "Edit ADQL" en "View" e ingresar lo siguiente en el cuadro bajo "ADQL Query" (consulta ADQL).

.. 3.1. Clear the search results and return to the main Portal interface.
.. In the upper right, select "Edit ADQL" for "View", and enter the following in the box under "ADQL Query".

.. code-block:: SQL

   SELECT coord_dec,coord_ra,g_calibFlux,i_calibFlux,r_calibFlux
   FROM dp02_dc2_catalogs.Object
   WHERE CONTAINS (POINT('ICRS', coord_ra, coord_dec), CIRCLE('ICRS', 62.0, -37.0, 1)) = 1
   AND detect_isPrimary =1
   AND g_calibFlux >360 AND g_extendedness =0
   AND i_calibFlux >360 AND i_extendedness =0
   AND r_calibFlux >360 AND r_extendedness =0

3.2. En la parte inferior de la página, establecer el límite de filas en "Row Limit" a 10000 y luego en la esquina inferior izquierda hacer clic en "Search" para realizar la búsqueda.
El Portal cambiará a la vista de resultados (Results View) como en el Paso 2, arriba.

.. 3.2. At the bottom of that page, set the "Row Limit" to 10000 and then click "Search" at lower left.
   The Portal will transition to the !!!"Results View"!!! as in Step 2, above.

**Aviso:** aunque se aplicó el mismo límite de 10000 filas tanto en el Paso 1.7 como en el Paso 3.2,
las dos búsquedas no devolverán las mismas filas exactamente.
Las consultas que devuelven solo un subconjunto de todos los resultados posibles, en este caso, 10000 de todas las filas posibles,
devolverán subconjuntos aleatorios.

.. **Notice:** although the same "Row Limit" of 10000 was applied both in Step 1.7 and Step 3.2,
   the two searches will not return the exact same rows.
   Queries which return only a subset of all possible results, in this case 10000 out of all possible rows,
   !!!will return random subsets!!!{parece enredado ya que antes decía que no tomaba aleatoriamente los objetos sino que iba archivo por archivo hasta llegar a 10000... pero claro creo que es exactamente lo que se advierte, que con las consultas si hay random}.



.. _DP0-2-Portal-Beginner-ES-Step-4:

Paso 4. Transferir consultas ADQL o resultados del Portal a la Faceta Notebook
==============================================================================

.. Step 4. Transfer ADQL queries or results from the Portal to the Notebook Aspect
.. ===============================================================================

4.1. Como se describe en el Paso 1.6, una vez que la consulta está completamente configurada en el Portal utilizando la opción "UI assisted",
hacer clic en "Populate and Edit ADQL" para cambiar el tipo de consulta a "Edit ADQL" y llenar la casilla ADQL de la consulta.
A continuación se muestra la misma consulta que en el Paso 3.1 anterior:

.. 4.1. As described under Step 1.6, once a query is all set up in the Portal using the "UI assisted",
.. click "Populate and Edit ADQL" to switch the Query Type to "Edit ADQL" and populate the ADQL query box.
.. Shown below is the same query as in Step 3.1 above:

.. figure:: /_static/portal_tut01_step04a.png
	:name: portal_tut01_step04a
	:alt: Captura de pantalla del formulario de consulta del Portal de RSP donde el usuario hará clic en el botón de búsqueda.
	

.. alt: Screenshot of the RSP portal query where the user will click the search button.

Para ejecutar la consulta en el Portal, hacer clic en el botón "Search".

.. To execute the query in the Portal, click the "Search" button.

Para ejecutar la consulta en la Faceta Notebook, copiar y pegar el código ADQL en la celda de código de cualquier notebook que
utilice el servicio TAP, como se muestra en la Sección 2.3 de la primera notebook del tutorial, "01 Introducción a DP0.2".

.. To execute the query in the Notebook Aspect, copy-paste the ADQL statement into the code cell of any notebook that
.. which uses the TAP service, as demonstrated in Section 2.3 of the first tutorial notebook, !!!01 Introduction to DP0.2.!!! {revisar si esto se traduce en el proyecto actual: SI DP02_01_Introduccion_a_DP02_ES.ipynb}

4.2. También es posible obtener una URL para acceder directamente a los resultados de la consulta.
Esta URL puede ser utilizada desde la Faceta Notebook; esta es una característica especialmente útil para
consultas que son grandes, complejas o que tardan mucho en ejecutarse (por ejemplo, uniones de múltiples tablas),
o para compartir los resultados de la consulta con colegas.

.. 4.2. It is also possible to obtain a URL for direct access to the query results.
.. This URL can be used from the Notebook Aspect; this is an especially useful feature for
.. queries that are large, complex, or time-consuming to execute (for instance, multiple table joins),
.. or for sharing query results with colleagues.

Como ejemplo, la imagen a continuación muestra la vista de resultados (Results View) para una pequeña consulta utilizando solo un radio de 0.05 grados.

.. As an example, the image below displays the !!!Results View!!! for a small query using just a 0.05 degree radius.

.. figure:: /_static/portal_tut01_step04b.png
	:name: portal_tut01_step04b
	:alt: Captura de pantalla de la vista de resultados de la consulta anterior.

.. alt: Screenshot of the results view from the above query.

Hacer clic en el botón "info" (letra "i" en un círculo) y aparecerá una ventana emergente:

.. Click on the "info" button (letter "i" in a circle), and a pop-up window will appear:

.. figure:: /_static/portal_tut01_step04c.png
	:name: portal_tut01_step04c
	:alt: Ventana emergente cuando se hace clic en el botón de información.

.. alt: Pop-up window when the info button is clicked.

Al lado de "UWS JOB URL" en la ventana emergente se encuentra la URL de los resultados de la consulta.
Hacer clic en el icono de portapapeles para copiar la URL en tu portapapeles.

.. The "UWS JOB URL" in the pop-up is the URL to the query results.
.. Click on the clipboard icon to copy the URL to your clipboard.

Como se mostró en la Sección 5.4 de la segunda notebook del tutorial, "02 Consultas de catálogo con TAP",
la URL se puede pegar en una celda de código y los resultados de la consulta se pueden recuperar utilizando los siguientes comandos:

.. As demonstrated in Section 5.4 of the second tutorial notebook, !!!02 Catalog Queries with TAP!!!{esta notebook parece que no se traduce en esta etapa, no se si conviene referenciarla con su nombre en inglés...},
.. the URL can be pasted into a code cell and the query results retrieved using the following commands:

.. code-block:: SQL

	retrieved_job = retrieve_query('my_portal_url')
	retrieved_results = retrieved_job.fetch_result().to_table().to_pandas()

De este modo, se tendrá en la notebook los mismos datos que se obtuvieron por primera vez a través de la Faceta Portal.

.. This results in having the same data in your notebook which you first obtained via the Portal Aspect.

Se aclara que las URL no serán accesibles indefinidamente, sino que están pensadas para acceso y análisis inmediato.
Para preservar y recrear consultas en una fecha posterior, se recomienda guardar la consulta en formato ADQL, como se describe en el paso 1.6.

.. We note that URLs will not be accessible indefinitely, !!!but rather are intended to serve the use case of immediate access and analysis!!!{revisar}.
.. To preserve and recreate queries at a later date, it is recommended to save the ADQL-formatted query as described in step 1.6.
