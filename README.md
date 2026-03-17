# Análisis de Vulnerabilidades(Red Hat & CISA KEV)

## Descripción del Proyecto
Este proyecto consiste en la extracción, procesamiento y análisis de vulnerabilidades de seguridad (CVEs).

## Tecnologías y Herramientas
* **Lenguaje base:** Python
* **Librerías:** `pandas`, `requests`
* **Consumo de APIs:**
    * Red Hat Security Data API (Vulnerabilidades y productos afectados)
    * CISA KEV Catalog (Vulnerabilidades explotadas activamente)
    * FIRST EPSS API (Sistema de puntuación predictiva de explotación)
* **Visualización de Datos:** Tableau Public

## Arquitectura 
1.  **Extracción:** Conexión a las APIs de Red Hat y CISA para recopilar los datos crudos en formato JSON.
2.  **Transformación:** Limpieza de datos (identificación y manejo de valores nulos), extracción de diccionarios, cruce de un CVE con múltiples productos afectados
3.  **Enriquecimiento:** Cruce entre el catálogo KEV y la API de FIRST para añadir métricas de probabilidad matemática (EPSS y Percentiles) a las vulnerabilidades activas.
4.  **Visualización:** Exportación a CSVs y representación en Tableau con un dashboard dinámico.

## Análisis y Visualizaciones del Dashboard

1.- NUMERODE VULNERABILIDADES POR CRITICIDAD:

Esta gráfica muestra la extracción de los identificadores CVE (estandar para la identificaación de vulnerabilidades) más recientes y su impacto. Se utilizó el puntaje CSSV v3 para clasificar la gravedad de cada vulnerabilidad. 
Es importante mencionar que se aplicó una limpieza de datos donde se omitió el 10.2% de los registros debido a que correspondian a vulnerabilidades en fase de análisis y por lo mismo no contaban con un puntaje CVSS asignado.
La gráfica muestra que la mayor cantidad de vulnerabilidades ase concentran en niveles de  gravedad "Medio" y "Alto" lo que significa que requiere atención prioritaria

Con base en la grafica podemos observar que la mayoria de las vulnerabilidades detectadas entran en nivel de gravedad medio y alto.


2.- NÚMERO DE VULNERABILIDADES POR PRODUCTO Y CRITICIDAD

Para esta representación, se tuvo que hacer una relación de cada CVE con los productos encontrados en cada URL de apoyo; es decir una relación uno a muchos.  Se aplico un filtro que muestra unicamente los 10 productos con más vulnerabilidades detectadas, ordenados en forma descendente. Además en cada producto se puede observar un recuento de los CVSS ordenado por el nivel de gravedad. Esto sirve para saber en que productos enfocarce primero.


3.-APROVECHAMIENTO ACTIVO

Finalmente, la tercera tabla mustra el riesgo de explotación en el mundo real. 
Se realizó un cruce de la BD generada contra el KEV de la CISA para identificar amenazas activas al 16 de marzo y hasta ese día solo se encontraron 3 coincidencias, sin embargo no impactan sofware de RedHat, todas son referentes al navegador Chromium y  poseen un puntaje CVSS de 8.8 por lo que se clasifican con gravedad alta y se publicaron el 12 y 13 de marzo.

Para conocer la probabilidad de que la vulnerabilidad sea explotada se uso la API FiRST para obtener el EPSS y el percentil para conocer su probabilidad de riesgo contra otras vulnerabilidades.

Se observaron EPSS menores al 30%, indicando que no es tan probable que sean atacados, pero al tener un percentil superior al 90% su riesgo en comparación con otras vulnerabilidades se vuelve alto; por lo que deben ser prioridad.

## Enlaces
* **Dashboard Interactivo:** [https://public.tableau.com/views/Anlisi_RedHat/Dashboard1?:language=es-ES&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link]
* **Código Fuente:** Archivo `.ipynb`  incluido en este repositorio.
