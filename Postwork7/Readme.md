# Postwork 7 - RStudio Cloud - GitHub, conexiones con BDs y lectura de datos externos.
## :dart: Objetivo
- Realizar el alojamiento de un fichero .csv a una base de datos (BDD), en un local host de mongodb a través de R.

## 🔧 Requisitos
* Mongodb Compass
* Librerías mongolite
* Nociones básicas de manejo de BDD

## 🤓 Desarrollo
Utilizando el manejador de BDD Mongodb Compass (previamente instalado), deberás de realizar las siguientes acciones:

#### 1.- Alojar el fichero match.data.csv en una base de datos llamada match_games, nombrando la collection como match.
Se descargo el archivo match.data.csv, para después importarlo en MongoDB. Los pasos para poder importar este archivo, primero fue crear nuestra Base de Datos con nombre "match_games" y una colección con nombre "match":

<p align = "center">
  <img src = "https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork7/Create_Database.JPG">
</p>

Después dentro de nuestra colección "match" importamos nuestro archivo CSV de la siguiente forma:

<p align = "center">
  <img src = "https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork7/Upload_CSV.JPG">
</p>

Antes de cargar los datos hemos configurado el tipo de dato de cada una de nuestras columnas, tomando en consideración nuestro criterio de que lo mejor es manejar el campo "date" como un String ya que en R es más sencillo crear una consulta de una fecha como un String.

#### 2.- Una vez hecho esto, realizar un count para conocer el número de registros que se tiene en la base.
Una vez cargados los documentos de nuestro archivo CSV, procedemos a conectar con código en RStudio nuestra Base de Datos de Mongo. <br/>
Se investigo sobre la libería "mongolite" para poder hacer la conexión y el resultado fue el siguiente:

```R
#install.packages("mongolite")

library(mongolite)  

prueba<- mongo(
  collection = "match",
  db="match_games", 
  url = "mongodb+srv://timmitonx:ismael132@cluster0.dmt93.mongodb.net/test",
  verbose = FALSE,
  options = ssl_options()
  )
```

#### 3.- Realiza una consulta utilizando la sintaxis de Mongodb en la base de datos, para conocer el número de goles que metió el Real Madrid el 20 de Diciembre de 2015 y contra que equipo jugó ¿perdió o fue goleada?

#### 4.- Por último, no olvides cerrar la conexión con la BDD.
