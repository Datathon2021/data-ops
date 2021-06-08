# Challenge campus party 2021


## Descripcion

Automatizar un proceso de ETL de datos utilizando Airflow o cron.

## Introduccion

Desde el espacio de Data Managment de Advanced Analytics nos encargamos de automatizar procesos de Extract, Transform and Load (ETL) de datos para facilitar su disponibilidad a la hora de buscar insights o entrenar modelos de aprendizaje automatizado.

Dada la multiplicidad de fuentes de datos de Telecom, ponemos enfasis en las buenas practicas de automatizacion, documentacion y mantenimiento de procesos a gran escala. Es por eso que te retamos a aplicar tu conocimiento de principio a fin de un proceso de ETL automatizado.

## El challenge

Este proceso automatizado consiste en tomar datos de entrada, procesarlos y escribirlos en un archivo de salida. Los datos de entrada se encuentran en el siguiente link: [Datasets](https://datasets.imdbws.com/).
Estos datos pertenecen al dataset público de IMDB, cuya metadata se encuentra en el siguiente link: [Metadata](https://www.imdb.com/interfaces/).

Sobre estos datos, te solicitamos realizar las transformaciones pertinentes en lenguaje Python con el objetivo de:

Obtener una base solo de películas de los últimos 5 años, agrupada por año de lanzamiento y género, con los siguientes atributos (Obligatorios y Deseados):

Obligatorios
- Promedio de rating
- Cantidad de votaciones
- Tiempo promedio de ejecución (Minutos)

Deseados
- Promedio de rating
- Cantidad de votaciones
- Tiempo promedio de ejecución (Minutos)
  
NOTA: Si una película tiene mas de un género, incluir el cálculo en todos los géneros a los que pertenece.

Finalmente, almacenar la salida de este proceso a nivel de la carpeta que se indica para cada caso en la siguiente seccion.

## A tener en cuenta!

A los fines de automatizar este proceso, solicitamos el uso de Docker y una herramienta a elección: preferentemente Airflow o en su defecto, Cron. Esto va a requerir la creación de un Dockerfile y el código en Python asociado que sea ejecutado dentro del container. Una vez elegida la imagen completar el archivo Dockerfile.

De acuerdo a la herramienta elegida se espera lo siguiente:

### Airflow

Utilizar la imagen `apache/airflow:1.10.10` (en [Dockerhub](https://hub.docker.com/r/apache/airflow)) basada en Apache Airflow v1.10.10. Preparar un container para que cuando se levante, genere la instancia de Airflow con scheduler y webserver y que tenga el dag preparado para ser ejecutado. Colocar el código en la carpeta `dags`. La salida de este proceso debe apuntar a la ruta `/home/airflow` dentro del container.

### Cron

Utilizar la imagen `python:3.7-slim` (en [Dockerhub](https://hub.docker.com/_/python)) basada en Python 3.7 y configurar cron para automatizar un script de Python que ejecute el proceso. En la carpeta `src` colocar el código. La salida de este proceso debe apuntar a la ruta `/app` dentro del container.

## Evaluacion

Del entregable se evaluaran diferentes aspectos:

### Formato y estilo

Se aplicaran herramientas para evaluar la complacencia del codigo con la guia de estilo conocida como `PEP8`, a su vez se evaluaran errores de sintaxis.

### Archivo de salida correcto

Se evaluara que los valores y las columnas de el archivo de salida entregado sean correctos. Para que esto pueda ser evaluado es necesario que el archivo de salida tenga las siguientes columnas:

| Nombre     | Descripcion |
|------------|-------------|
| `año`      | Columna de tipo `integer` que representa el año de lanzamiento de la pelicula |
| `genero`   | Columna de tipo `string` que representa el nombre del género de la pelicula |
| `pelicula` | Columna de tipo `string` que representa el nombre de una pelicula |
| `genero`   | Columan de tipo `string` que representa generos del cine |
| `votos`    | Columnda de tipo `integer` que representa la media de votos obtenida por parte de las peliculas que reportan el genero |

### Tiempo de ejecucion

Se obtendra el tiempo medio de ejecucion del codigo suministrado calculado a partir de 10 corridas. Es deseable que el codigo sea eficiente por lo que lo que se considera mejor el menor tiempo de ejecucion.
