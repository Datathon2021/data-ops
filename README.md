# Challenge campus party 2021

## Descripcion

Automatizar un proceso de ETL de datos utilizando Apache Airflow.

## Introduccion

Desde el espacio de Data Managment de Advanced Analytics nos encargamos de automatizar procesos de Extract, Transform and Load (ETL) de datos para facilitar su disponibilidad a la hora de buscar insights o entrenar modelos de aprendizaje automatizado.

Dada la multiplicidad de fuentes de datos de Telecom, ponemos enfasis en las buenas practicas de automatizacion, documentacion y mantenimiento de procesos a gran escala. Es por eso que te retamos a aplicar tu conocimiento de principio a fin de un proceso de ETL automatizado.

## El desafio

Este proceso automatizado consiste en tomar datos de entrada, procesarlos y escribirlos en un archivo de salida. Los datos de entrada se encuentran en el siguiente link: [Datasets](https://datasets.imdbws.com/).
Estos datos pertenecen al dataset público de IMDB, cuya metadata se encuentra en el siguiente link: [Metadata](https://www.imdb.com/interfaces/).


Utilizando el lenguaje Python te proponemos el siguiente desafio:

> Para cada *año de estreno* y cada *genero unico* necesitamos calcular la **cantidad total de votos**, la **media de la duracion** y la **media del rating** para todos los titulos de tipo peliculas (`titleType==movie`) que se estrenaron durante los años 2015 y 2020 inclusive (`2015 <= startYear <= 2020`). Tene en cuenta que si una pelicula aparece en mas de un genero se debe incluir en el calculo para cada uno de los generos que pertenece. Ademas, redondea todos los decimales a 2 espacios despues de la coma.

De manera optativa podes tambien agregar la siguiente informacion:

> Para cada *año de estreno* y cada *genero unico* agregar ademas **cantidad de directores distintos**, **cantidad de escritores distintos** y **director con mas contenidos**. Para esta ultima columna y en caso de empate entre directores agregar ambos separados por punto y coma seguido de un espacio (A modo de ejemplo, si `DirectorA` y `DirectorB` fuesen ambos los directores con mas contenidos entonces la columna dira: `DirectorA; DirectorB`).

Finalmente, almacenar la salida de este proceso donde sea indicado para poder ser evaluado.

## A tener en cuenta!

A los fines de automatizar este proceso, solicitamos el uso de Docker y Apache Airflow. Esto va a requerir la creación de un Dockerfile y el código en Python asociado que sea ejecutado dentro del container.

### Airflow

Utilizar la imagen `apache/airflow:1.10.10` (en [Dockerhub](https://hub.docker.com/r/apache/airflow)) basada en Apache Airflow v1.10.10. Preparar un container para que cuando se levante, genere la instancia de Airflow con scheduler y webserver y que tenga el dag preparado para ser ejecutado. Colocar el código en la carpeta `dags`. La salida de este proceso debe apuntar a la ruta `/home/airflow` dentro del container y el nombre del archivo sera `resultados.csv`. Consideramos una ejecucion sin errores aquella que finaliza con la creacion del archivo `/home/airflow/resultados.csv`.

### Entorno de desarrollo

Para poder realizar el ejercicio por lo menos vas a necesitar tener installado [docker](https://docs.docker.com/get-docker/) y [python v3+](https://www.python.org/downloads/). Para escribir codigo podes utilizar tu IDE preferido, si no conoces ninguno te sugerimos [VSCode](https://code.visualstudio.com/download). Todas estas aplicaciones estan disponibles para Linux, Windows y Mac.

## Evaluacion

Del entregable se evaluaran diferentes aspectos:

### 1. Ejecucion del proceso sin errores

El proceso debe ejecutarse de principio a fin sin detener por errores. El uso de buenas practicas para el manejo de errores es aconsejable!

### 2. Archivo de salida correcto

Se evaluara que los valores y las columnas de el archivo de salida entregado sean correctos. Para que esto pueda ser evaluado es necesario que el archivo de salida tenga las siguientes columnas:

| Nombre     | Requerimiento | Descripcion |
|------------|---------------|-------------|
| `startYear`      | Obligatorio |Columna de tipo `integer` que representa el año de lanzamiento de la pelicula |
| `genres`         | Obligatorio | Columna de tipo `string` que representa el nombre del género de cine de la pelicula |
| `runtimeMinutes` | Obligatorio | Columna de tipo `float` que representa la media de duracion para todas las peliculas para un dado año-genero. Debe estar redondeada a dos digitos despues de la coma (Ej `0.00`) |
| `averageRating`  | Obligatorio | Columna de tipo `float` que representa la media de votos para todas las peliculas para un dado año-genero. Debe estar redondeada a dos digitos despues de la coma (Ej `0.00`) |
| `numVotes`       | Obligatorio | Columna de tipo `integer` que representa el total de votos para todas las peliculas para un dado año-genero |
| `numDirectors`   | Optativo    | Columna de tipo `integer` que representa la cantidad de directores unicos que dirigieron peliculas para un dado año-genero |
| `numWriters`     | Optativo    | Columna de tipo `integer` que representa la cantidad de escritores unicos que escribieron guiones de peliculas para un dado año-genero |
| `topDirectors`   | Optativo    | Columna de tipo `string` que representa el nombre del director con mas peliculas para un dado año-genero. En caso de que sean multiples, los nombres deben estar separados por un punto y coma seguido de un espacio (`DirectorA; DirectorB`) |

En este punto se tendra en cuenta durante la valoracion del resultado final si se completo la parte optativa del desafio.

### 3. Formato y estilo

Se aplicaran herramientas para evaluar la complacencia del codigo con la guia de estilo conocida como `PEP8`, a su vez se evaluaran errores de sintaxis.


### 4. Tiempo de entrega

Se tomara en cuenta la velocidad en que se resolvio el desafio desde su publicacion, quienes mas rapido envien los resultados mas puntos suman.

### 5. Tiempo de ejecucion

Se obtendra el tiempo medio de ejecucion del codigo suministrado calculado a partir de 10 corridas. Es deseable que el codigo sea eficiente por lo que lo que se considera mejor el menor tiempo de ejecucion.
