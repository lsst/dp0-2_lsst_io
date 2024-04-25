.. Revisar el README para obtener instrucciones sobre cómo contribuir.
.. Revisar la guía de estilo para mantener un enfoque consistente en la documentación.
.. Los objetos estáticos, como las figuras, deben almacenarse en el directorio _static. Revisar _static/README para obtener instrucciones sobre cómo contribuir.
.. No eliminar los comentarios que describen cada sección. Se incluyen para brindar orientación a los colaboradores.
.. No eliminar otro contenido proporcionado en las plantillas, como por ejemplo una sección. En su lugar, comentar el contenido y agregar comentarios para explicar la situación. Por ejemplo:
  - Si no se necesita una sección dentro de la plantilla, comentar el título de la sección y la referencia de la etiqueta. No eliminar el título de sección esperado, la referencia ni los comentarios relacionados proporcionados por la plantilla.
  - Si un archivo no puede incluir un título (rodeado por numerales (#)), comentar el título desde la plantilla e incluir un comentario explicando por qué se implementa esto (además de aplicar la directiva ``title``).

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

.. Esta sección debería ofrecer una descripción breve y de alto nivel de la página.

**Faceta del RSP:** Portal

**Autoría:** Melissa Graham y Greg Madejski

**Última verificación de ejecución:** 2023-04-07

**Nivel de aprendizaje:** principiante

**Introducción:**
Este tutorial utiliza la interfaz Consulta de Tabla Única (Single-Table Query) para buscar estrellas brillantes en una región pequeña del cielo
y luego utiliza la interfaz de Resultados (Results) para crear un diagrama color-magnitud.
Este es el mismo ejemplo usado para ilustrar el servicio de Protocolo de Acceso de Tablas (Table Access Protocol - TAP) en el primer tutorial de :ref:`DP0-2-Tutorials-Notebooks-ES`.
Principiantes que busquen una visión más general de la Faceta Portal pueden consultar :doc:`/data-access-analysis-tools/portal-intro`.


.. _DP0-2-Portal-Beginner-ES-Step-1:

Paso 1. Establecer las restricciones de la consulta
===================================================

1.1. Iniciar sesión en la Faceta Portal.

1.2. Debajo de "TAP Searches" (búsquedas TAP), dejar la casilla "Use Image Search (ObsTAP)" sin marcar y dejar la configuración de "View" con su valor por defecto "UI assisted".

1.3. A la derecha de "LSST DP0.2 DC2 Tables", elegir en "Table Collection" el conjunto de tablas "dp02_dc2_catalogs" (menú desplegable de la izquierda) y en "Table" la tabla "dp02_dc2_catalogs.Object" (menú desplegable de la derecha).

1.4. En la sección de restricciones, debajo de "Enter Constraints", marcar la casilla de verificación a la izquierda de "Spatial" para usar restricciones espaciales.
Dejar "Shape Type" (el tipo de forma) con su valor por defecto "Cone" (cono), y para las coordenadas/nombre de objeto en "Coords or Obj Name" usar las coordenadas centrales del área de simulación de DC2 "62, -37".
En el menú desplegable al lado de "Radius", elegir "degrees" *y luego* ingresar "1" en el cuadro de texto y presionar la tecla *enter* (*entrar*) para establecer la búsqueda con radio de 1 grado.

1.5. En la tabla de la derecha, debajo de "Output Column Selection and Constraints" (Selección de Columnas de Salida y Restricciones), hacer clic en las casillas de la primera columna a la izquierda para seleccionar "coord_ra", "coord_dec", "detect_isPrimary", "g" "r" e "i_calibFlux", y "g" "r" e "i_extendedness". Se pueden buscar los nombres de columnas. Para evitar recorrer una larga lista de columnas,
ingresar una palabra clave (e.g., "calibFlux") en el cuadro justo debajo de la columna "Name". Se listarán todos los nombres de columnas que contengan la palabra clave ingresada.
Después de seleccionar las columnas que se necesiten (e.g., "g" "r" e "i_calibFlux"), borrar el cuadro de texto y presionar *enter* para continuar seleccionando otras columnas.
Hacer clic en el símbolo de embudo en la parte superior de la columna de casillas de verificación para filtrar la vista de tabla y mostrar sólo las columnas seleccionadas.

1.6. En la columna de restricciones "constraints", ingresar "=1" para "detect_isPrimary", ">360" para los flujos ("g" "r" e "i_calibFlux"), y "=0" para los parámetros de extensión ("extendedness")
Esto va a limitar los objetos obtenidos a aquellos sin hijos (i.e. componentes resultantes de la separación [deblending]), que son más brillantes que aproximadamente 25 magnitudes
en los filtros g, r e i, y que parecen ser puntuales (no extendidos, pero *no necesariamente estelares*) en esos tres filtros también.

En este punto las casillas que seleccionan los parámetros de "extendedness" y "detect_isPrimary" pueden ser desmarcadas ya que
no es necesario para este tutorial recopilar los datos de estas columnas, sino que sólo se busca restringir la consulta basándose en sus valores.

**Aviso:** En este punto, con la consulta configurada en su totalidad, haciendo clic en "Populate and Edit ADQL" (rellenar y editar ADQL) se cambiará el Tipo de Consulta a "Edit ADQL" y se llenará el cuadro "ADQL Query" con la consulta, como se muestra en el Paso 3 más abajo.

1.7. Establecer el límite de filas en "Row Limit" a 10000, para solo obtener 10000 objetos para esta demostración.

.. figure:: /_static/portal_tut01_step01.png
	:name: portal_tut01_step01
	:alt: Una captura de pantalla que muestra cómo ingresar criterios de búsqueda en la Faceta Portal.
		El portal es una forma conveniente de consultar la base de datos de Rubin a través de una interfaz gráfica de usuario sin necesidad de usar Python o *scripts* en la línea de comandos.
		Cada fila representa una categoría separada que caracteriza los criterios de búsqueda TAP a utilizar, incluyendo: el servicio TAP; el tipo de consulta;
		la colección de tablas y la tabla específica a utilizar, así como las restricciones a emplear para la consulta. La búsqueda en el portal se puede realizar presionando el botón de búsqueda en la esquina inferior izquierda.
	
	La captura de pantalla anterior muestra las restricciones antes de hacer clic en "Search".

1.8. Hacer clic en "Search" en la parte más abajo a la izquierda para realizar la búsqueda.


.. _DP0-2-Portal-Beginner-ES-Step-2:

Paso 2. Crear el diagrama color-magnitud
========================================

La disposición predeterminada "Tri-view" muestra un mapa de cobertura del cielo de la simulación DESC DC2 en la parte superior izquierda (debajo de "Coverage"), un gráfico interactivo ("Active Chart") que muestra la distribución espacial de los objetos obtenidos
en la parte superior derecha y una tabla con los resultados de la búsqueda en la parte inferior.

.. figure:: /_static/portal_tut01_step02a.png
	:name: portal_tut01_step02a
	:alt: Una captura de pantalla de los resultados de la consulta realizada anteriormente.
	
	La vista predeterminada de resultados con "Tri-view".

2.1. En la esquina superior derecha, hacer clic en "Bi-view Tables"  para mostrar solo el gráfico interactivo o solo el mapa de cobertura del cielo (alternando entre los dos haciendo clic en la pestaña "Active Chart"/"Coverage") en la parte derecha junto con la tabla en la parte izquierda de la pantalla.

**Aviso:** Los objetos obtenidos *no* llenan el área de búsqueda (con radio de 1 grado) en el gráfico interactivo predeterminado de "coord_ra" versus "coord_dec".
Esto se debe a que se aplicó un límite de filas de 10000 objetos, y los datos están divididos en archivos por coordenadas celestes.
La consulta accedió a estos archivos hasta encontrar 10000 objetos (es decir, la consulta *no* encuentra *todos los objetos* que cumplen con los parámetros de la consulta y luego elige 10000 objetos al azar para devolver).

.. figure:: /_static/portal_tut01_step02b.png
	:name: portal_tut01_step02b
	:alt: Esta es una captura de pantalla del portal después de ejecutar una búsqueda de consulta. La imagen superior muestra la densidad de las fuentes seleccionadas dentro del área de búsqueda.
		En este caso, un círculo con el radio seleccionado previamente centrado en la ascensión recta y declinación elegidas.
		El panel inferior muestra los objetos devueltos por la consulta de búsqueda en forma de tabla.
	
	La vista de resultados (Results) con "Bi-view Tables" seleccionado.

**Aviso:** Para graficar el color (magnitudes r-i) versus la magnitud (g), los flujos (que están en unidades de nanojansky) se convertirán a magnitudes AB en el siguiente paso. La página `Magnitud AB Wikipedia <https://es.wikipedia.org/wiki/Magnitud_AB>`_ ofrece un recurso conciso para quienes no estén familiarizados con las magnitudes AB y los flujos en unidades de jansky.

2.2. Hacer clic en el icono de configuración del gráfico interactivo (en "Active Chart", los dos engranajes en la esquina superior derecha) para modificar la traza (opción "modify trace"), lo que significa cambiar los parámetros del gráfico.
Establecer "X" como "(-2.5 * log10(r_calibFlux)) - (-2.5 * log10(i_calibFlux))" e "Y" como "-2.5 * log10(g_calibFlux) + 31.4".
Dejar las opciones en "Trace Options" como están y hacer clic en "Chart Options" para mostrar las opciones de gráfico.
Para el título del gráfico, en "Chart title" ingresar "Diagrama Color-Magnitud"; establecer "X Label" (la etiqueta del eje X) como "color (r-i)"; establecer "Y Label" (etiqueta del eje Y) como "magnitud (g)" y debajo en "Options" marcar la casilla correspondiente a "reverse".
Establecer los valores "X Min/Max" en "-0.5" y "2.0", y los valores "Y Min/Max" en "16.5" y "25.5".

.. figure:: /_static/portal_tut01_step02c.png
	:name: portal_tut01_step02c
	:alt: Una captura de pantalla de la Faceta Portal que muestra la interfaz que permite crear gráficos a partir de los datos devueltos por la consulta.
		Crear gráficos de esta manera es una forma fácil y funcional de explorar los datos.
		La interfaz permite: ingresar funciones de los datos devueltos para graficar, elegir un esquema de colores, editar la segmentación, crear etiquetas y editar la escala de los ejes.
        :width: 300
	
	Establecer los parámetros del gráfico.

2.3. Aplicar los parámetros haciendo clic en "Apply" y luego hacer clic en el botón "Close" para cerrar la ventana, mirar el gráfico color-magnitud.

.. figure:: /_static/portal_tut01_step02d.png
	:name: portal_tut01_step02d
	:alt: Una captura de pantalla del gráfico creado a partir de los datos devueltos por la consulta utilizando la interfaz xy de la Faceta Portal.
		El gráfico muestra un diagrama color-magnitud de la magnitud AB en la banda g vs. el color de la banda r menos la banda i, para los objetos devueltos por la consulta.
		Este ejemplo demuestra cómo explorar rápidamente los datos devueltos en la consulta de búsqueda.
		El gráfico muestra una gran densidad de estrellas en colores r-i bajos, y segmentos discretos en colores r-i más rojizos debido a que los datos simulados se
		basan en modelos estelares rojos discretos que se utilizaron como entrada en DP0.2. Se espera que los datos reales muestren, en cambio, una distribución suave de colores.
	
	El diagrama color-magnitud.

**Aviso:** El estilo de gráfico predeterminado es un gráfico de dispersión, que es apropiado para nuestro conjunto de datos de tamaño modesto (como los 10000 objetos recuperados aquí).
También es posible crear un histograma bidimensional, apropiado para conjuntos de datos grandes (un "mapa de calor" o "heat map"), que crearemos en el Paso 2.4.

**Aviso:** Los datos simulados están visiblemente estratificados en el gráfico anterior, y esto no ocurrirá con datos reales.
Las secuencias discretas en colores rojos, (g-i) > 0.5, provienen del procedimiento discretizado utilizado para simular estrellas de baja masa en el conjunto de datos DP0.2.

2.4. Hacer clic nuevamente en el icono de configuración del gráfico xy (los dos engranajes en la esquina superior derecha), pero esta vez elegir "Add New Chart" para agregar un nuevo gráfico.
Cambiar el tipo de gráfico en "Plot Type" a mapa de calor con la opción "Heatmap" y luego establecer "X" e "Y" con las mismas ecuaciones que en el Paso 2.2.
Utilizar las mismas opciones de gráfico en "Chart Options", pero elegir un nombre distinto para el título del gráfico en "Chart title", tal como "Diagrama Color-Magnitud - Mapa de Calor".

.. figure:: /_static/portal_tut01_step02e.png
	:name: portal_tut01_step02e
	:alt: Captura de pantalla de la ventana de diálogo donde se pueden establecer los nuevos parámetros del gráfico para el mapa de calor.
        :width: 300
	
	Arriba, establecimos los nuevos parámetros del gráfico mapa de calor.

2.5. Hacer clic en "OK" y "Close", y observar el nuevo gráfico de color-magnitud. Para mayor exhaustividad, es posible que se prefiera actualizar el título del gráfico generado anteriormente a "Diagrama Color-Magnitud - Dispersión" ya que aquel era un gráfico de dispersión.

.. figure:: /_static/portal_tut01_step02f.png
	:name: portal_tut01_step02f
	:alt: Diagramas color-magnitud generados a partir del gráfico de dispersión y el mapa de calor creados anteriormente.
	
	Los diagramas color-magnitud, incluyendo el gráfico de dispersión previamente creado (izquierda) y el mapa de calor (derecha).

2.6. Interactuar con el gráfico.
Pasar el *mouse* sobre los puntos de datos en el mapa de cobertura en "Coverage Map" (se verá cómo cambian las coordenadas en la parte inferior del mapa) o en el gráfico interactivo "Active Chart" (se verá que los valores de x e y aparecen en una ventana emergente).
Al seleccionar una fila en la tabla, ésta aparecerá de un color diferente en el(los) gráfico(s), y viceversa: al seleccionar un punto en un gráfico, se resaltará en la tabla de abajo.


.. _DP0-2-Portal-Beginner-ES-Step-3:

Paso 3. Hacer la misma consulta con ADQL
========================================

3.1. Borrar los resultados de la búsqueda y regresar a la interfaz principal del Portal.
En la esquina superior derecha, seleccionar la vista "Edit ADQL" en "View" e ingresar lo siguiente en el cuadro bajo "ADQL Query" (consulta ADQL).

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

**Aviso:** aunque se aplicó el mismo límite de 10000 filas tanto en el Paso 1.7 como en el Paso 3.2,
las dos búsquedas no devolverán las mismas filas exactamente.
Las consultas que devuelven sólo un subconjunto de todos los resultados posibles, en este caso, 10000 de todas las filas posibles,
devolverán subconjuntos aleatorios.


.. _DP0-2-Portal-Beginner-ES-Step-4:

Paso 4. Transferir consultas ADQL o resultados del Portal a la Faceta Notebook
==============================================================================

4.1. Como se describe en el Paso 1.6, una vez que la consulta está completamente configurada en el Portal utilizando la opción "UI assisted",
hacer clic en "Populate and Edit ADQL" para cambiar el tipo de consulta a "Edit ADQL" y llenar la casilla ADQL de la consulta.
A continuación se muestra la misma consulta que en el Paso 3.1 anterior:

.. figure:: /_static/portal_tut01_step04a.png
	:name: portal_tut01_step04a
	:alt: Captura de pantalla del formulario de consulta del Portal de RSP donde el usuario hará clic en el botón de búsqueda.

Para ejecutar la consulta en el Portal, hacer clic en el botón "Search".

Para ejecutar la consulta en la Faceta Notebook, copiar y pegar el código ADQL en la celda de código de cualquier notebook que
utilice el servicio TAP, como se muestra en la Sección 2.3 del primer tutorial de la Faceta Notebook, "01 Introducción a DP0.2".

4.2. También es posible obtener una URL para acceder directamente a los resultados de la consulta.
Esta URL puede ser utilizada desde la Faceta Notebook; esta es una característica especialmente útil para
consultas que son grandes, complejas o que tardan mucho en ejecutarse (por ejemplo, uniones de múltiples tablas),
o para compartir los resultados de la consulta con colegas.

Como ejemplo, la imagen a continuación muestra la vista de resultados (Results View) para una pequeña consulta utilizando solo un radio de 0.05 grados.

.. figure:: /_static/portal_tut01_step04b.png
	:name: portal_tut01_step04b
	:alt: Captura de pantalla de la vista de resultados de la consulta anterior.

Hacer clic en el botón "info" (letra "i" en un círculo) y aparecerá una ventana emergente:

.. figure:: /_static/portal_tut01_step04c.png
	:name: portal_tut01_step04c
	:alt: Ventana emergente cuando se hace clic en el botón de información.

Al lado de "UWS JOB URL" en la ventana emergente se encuentra la URL de los resultados de la consulta.
Hacer clic en el icono de portapapeles para copiar la URL en tu portapapeles.

Como se mostró en la Sección 5.4 del segundo tutorial de la Faceta Notebook, "02 Consultas de catálogo con TAP",
la URL se puede pegar en una celda de código y los resultados de la consulta se pueden obtener utilizando los siguientes comandos:

.. code-block:: SQL

	retrieved_job = retrieve_query('my_portal_url')
	retrieved_results = retrieved_job.fetch_result().to_table().to_pandas()

De este modo, se tendrá en el notebook los mismos datos que se obtuvieron por primera vez a través de la Faceta Portal.

Se aclara que las URL no serán accesibles indefinidamente, sino que están pensadas para acceso y análisis inmediato.
Para preservar y recrear consultas en una fecha posterior, se recomienda guardar la consulta en formato ADQL, como se describe en el paso 1.6.
