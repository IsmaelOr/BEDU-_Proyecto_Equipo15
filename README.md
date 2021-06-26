# Fase 2 - Proyecto - Equipo 15
Repositorio de entrega de Postwork para el Proyecto del Curso de BEDU en Data Science. Equipo 15


## 🚀 Integrantes del Equipo: 
*  Dávila Osorio Javier Ibzan
*  Díaz Lievano Lázaro Raúl
*  García Ruiz Diana Isabel
*  Ortega Estrada Ismael
*  Pizano Ocampo Aranza Nayeli
*  Sánchez Loperena Ruben

## 📂 Postworks
- [Postwork_1](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/tree/main/Postwork1)
- [Postwork_2](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/tree/main/Postwork2)
- [Postwork_3](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/tree/main/Postwork3)
- [Postwork_4](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/tree/main/Postwork4)

## Desarrollo del Proyecto
### Postwork 1
El siguiente postwork, te servirá para ir desarrollando habilidades como si se tratara de un proyecto que evidencie el progreso del aprendizaje durante el módulo, sesión a sesión se irá desarrollando. A continuación aparecen una serie de objetivos que deberás cumplir, es un ejemplo real de aplicación y tiene que ver con datos referentes a equipos de la liga española de fútbol (recuerda que los datos provienen siempre de diversas naturalezas), en este caso se cuenta con muchos datos que se pueden aprovechar, explotarlos y generar análisis interesantes que se pueden aplicar a otras áreas. Siendo así damos paso a las instrucciones:

#### 1. Importa los datos de soccer de la temporada 2019/2020 de la primera división de la liga española a R, los datos los puedes encontrar en el siguiente enlace: https://www.football-data.co.uk/spainm.php

Importamos el archivo que contiene los datos mediante la función read.csv y guardamos el data frame como soccer19_20 :

```R
soccer19_20 <- read.csv("https://www.football-data.co.uk/mmz4281/1920/SP1.csv")
```

A continuación se muestra el data frame obtenido:

```R
head(soccer19_20)
```

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Head%20soccer19_20.PNG)


#### 2. Del data frame que resulta de importar los datos a R, extrae las columnas que contienen los números de goles anotados por los equipos que jugaron en casa (FTHG) y los goles anotados por los equipos que jugaron como visitante (FTAG)

Esto lo hacemos seleccionando las columnas respectivas para:

Goles anotados por equipos de casa

```R
G_Casa <- soccer19_20[, "FTHG"]
```
![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Goles%20casa.PNG)

Y goles anotados por equipos visitantes

```R
G_Visitante <- soccer19_20[, "FTAG"]
```
![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Goles%20visitante.PNG)

#### 3. Consulta cómo funciona la función table en R al ejecutar en la consola ?table

```R
?table
```

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Consulta%20funci%C3%B3n%20table.PNG)

Tal como su nombre lo indica por medio de esta función convertimos los datos seleccionados a una tabla, en este caso utilizamos como argumentos las columnas extraidas y generamos tablas de frecuencias relativas.

Tabla de frecuencias goles de casa

```R
F_GCasa <- table(G_Casa); 
F_GCasa
```

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Tabla%20de%20frecuencias%20goles%20casa.PNG)

Tabla de frecuencias goles de visitante

```R
F_GVisitante <- table(G_Visitante); 
F_GVisitante
``` 

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Tabla%20de%20frecuencias%20goles%20visitante.PNG)

Posteriormente elabora tablas de frecuencias relativas para estimar las siguientes probabilidades:

#### * La probabilidad (marginal) de que el equipo que juega en casa anote X goles (X = 0, 1, 2, ...)

Para obtener la probabilidad marginal utilizamos la funcion prop.table, la cuál nos genera las probabilidades de que los equipos en casa anoten x cantidad de goles de acuerdo a las frecuencias obtenidas anteriormente y la expresamos como porcentaje.                                                                                                     

```R
P_GCasa <- prop.table(F_GCasa)  
paste("La probabilidad (%) de que el equipo de casa anote X goles es: ") 
P_GCasa <- round((P_GCasa * 100), 3); 
P_GCasa
```

La probabilidad (%) de que el equipo de casa anote X goles es:

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Probabilidad%20goles%20casa.PNG)

#### * La probabilidad (marginal) de que el equipo que juega como visitante anote Y goles (Y = 0, 1, 2, ...)

Realizamos la misma función del punto anterior ahora para las probabilidades de que los equipos visitantes anoten Y cantidad de goles.

```R
P_GVisitante <- prop.table(F_GVisitante)                                                                                                                                   
paste("La probabilidad (%) de que el equipo visitante anote Y goles es: ")                                                                                              
P_GVisitante <- round((P_GVisitante * 100), 3); 
P_GVisitante
```

La probabilidad (%) de que el equipo visitante anote Y goles es:

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Probabilidad%20goles%20visitante.PNG)
  
#### * La probabilidad (conjunta) de que el equipo que juega en casa anote X goles y el equipo que juega como visitante anote Y goles (x = 0, 1, 2, ..., y = 0, 1, 2, ...)

En este punto generamos una tabla de frecuencias conjunta, que nos muestra los diferentes casos utilizando como X los goles de los equipos en casa y como Y los goles de los equipos visitantes.

```R
F_GConj <- table(G_Casa,G_Visitante); 
F_GConj
```

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Tabla%20de%20frecuencias%20conjunta.PNG)

Finalmente utilizando la función prop.table generamos la probabilidad conjunta.

```R
P_Conj <- prop.table(table(G_Casa, G_Visitante))                                                                                                                       
paste("La probabilidad conjunta (%) de que el equipo de casa anote X goles y el equpo visitante anote Y goles: ")                                                             
P_Conj <- round((P_Conj * 100), 3); 
P_Conj
```

La probabilidad conjunta (%) de que el equipo de casa anote X goles y el equpo visitante anote Y goles:

![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork1/Probabilidad%20conjunta.PNG)

Al obtener esta tabla de probabilidades conjunta podemos posteriormente graficar los datos y analizarlos, siendo de utilidad para con base en ellos determinar cuales son los escenarios más probables y hacer proyecciones a futuro; por ejemplo apuestas, entre otras.

### Postwork 2
Ahora vamos a generar un cúmulo de datos mayor al que se tenía, esta es una situación habitual que se puede presentar para complementar un análisis, siempre es importante estar revisando las características o tipos de datos que tenemos, por si es necesario realizar alguna transformación en las variables y poder hacer operaciones aritméticas si es el caso, además de sólo tener presente algunas de las variables, no siempre se requiere el uso de todas para ciertos procesamientos.

#### 1. Importa los datos de soccer de las temporadas 2017/2018, 2018/2019 y 2019/2020 de la primera división de la liga española a R, los datos los puedes encontrar en el siguiente enlace: https://www.football-data.co.uk/spainm.php

##### Importamos la libreria `dplyr`
```R
  library(dplyr)
```
##### Almacenamos los `URL` de los dataset de las temporadas de soccer de primera division del 2017 al 2020.
```R
  URL_17_18 <- "https://www.football-data.co.uk/mmz4281/1718/SP1.csv"
  URL_18_19 <- "https://www.football-data.co.uk/mmz4281/1819/SP1.csv"
  URL_19_20 <- "https://www.football-data.co.uk/mmz4281/1920/SP1.csv"
```
##### Escogemos la carpeta donde se guardan los archivos `csv`.
```R
  setwd(choose.dir(caption = "Select folder"))
```
##### Descargamos los dataset de las temporadas de soccer y les asiganmos un nombre con extencion `csv`.
```R
  download.file(url = URL_17_18, destfile = "soccer17_18.csv", mode = "wb")
  download.file(url = URL_18_19, destfile = "soccer18_19.csv", mode = "wb")
  download.file(url = URL_19_20, destfile = "soccer19_20.csv", mode = "wb")
```
##### Leemos cojuntamente todos los archivos `csv` mediante la funcion `lapply()` y los guardamos en una lista.
```R
  SoccerList <- lapply(dir(), read.csv)
```

#### 2. Revisa la estructura de de los data frames al usar las funciones: `str`, `head`, `View` ó `summary`.
```R
  str(SoccerList[[1]]); head(SoccerList[[1]]); View(SoccerList[[1]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList1.PNG?raw=true)
```R
  str(SoccerList[[2]]); head(SoccerList[[2]]); View(SoccerList[[2]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList2.PNG?raw=true)
```R
  str(SoccerList[[3]]); head(SoccerList[[3]]); View(SoccerList[[3]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList3.PNG?raw=true)
##### Como se pudo checar en la revision de los dataset cada uno posee casi la misma cantidad de variables y hay algunas que se deben modificar. Hay que convertir la variable Date en una variable de tipo fecha (`as.Date`), mediante la funcion `mutate()` de la libreria de `dplyr`.
##### Se asigna la codificacion con la que se muestra en el data set por ejemplo si la fecha aparece como 20/03/17 la codificacion debe ser `%d/%m/%y` y para una fecha de este modo 20/03/2017 corresponde la codificacion `%d/%m/%Y`.
```R
  SoccerList[[1]] <- mutate(SoccerList[[1]], Date = as.Date(Date, "%d/%m/%y")) 
  SoccerList[[2]] <- mutate(SoccerList[[2]], Date = as.Date(Date, "%d/%m/%Y"))
  SoccerList[[3]] <- mutate(SoccerList[[3]], Date = as.Date(Date, "%d/%m/%Y"))
```
##### Al verificar de nuevo los datos se confirma que la codificacion y tipo de variable para `Date` son la misma para todos los componentes de la lista.
```R
  str(SoccerList[[1]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList1-1.PNG?raw=true)
```R
  str(SoccerList[[2]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList2-1.PNG?raw=true)
```R
  str(SoccerList[[3]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList3-1.PNG?raw=true)
#### 3. Con la función `select()` del paquete dplyr selecciona únicamente las columnas `Date`, `HomeTeam`, `AwayTeam`, `FTHG`, `FTAG` y `FTR`; esto para cada uno de los data frames. Mediante la funcion `lapply()` para poder aplicar el selec a todos los componentes de la lista.
```R
  SoccerList <- lapply(SoccerList, select, Date, HomeTeam, AwayTeam, FTHG, FTAG, FTR)
```
##### Al momento de hacer la verificacion nuevamente se puede observar que los dataframe de la lista ahora solo cuenta con 6 variables.
```R
  str(SoccerList[[1]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList1-2.PNG?raw=true)
```R
  str(SoccerList[[2]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList2-2.PNG?raw=true)
```R
  str(SoccerList[[3]])
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/SoccerList3-2.PNG?raw=true)
#### 4. Asegúrate de que los elementos de las columnas correspondientes de los nuevos data frames sean del mismo tipo. Con ayuda de la función `rbind` forma un único data frame que contenga las seis columnas mencionadas en el punto 3, la función `do.call()` podría ser utilizada
```R
  Soccer <- do.call(rbind, SoccerList)
```
##### Comprobamos que se hallan juntado todos datos de la lista en un dataframe. Debe aparecer un dataframe con 1140 observaciones y 6 variables.
```R
  str(Soccer); View(Soccer)
```
![alt_text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork2/total.PNG?raw=true)
##### Por ultimo se exporta el dataFrame a un archivo csv
```R
  write.csv(Soccer, "Soccer_2017-2020.csv", row.names = FALSE)
```

### Postwork 3

### Postwork 4
Ahora investigarás la dependencia o independencia del número de goles anotados por el equipo de casa y el número de goles anotados por el equipo visitante mediante un procedimiento denominado bootstrap, revisa bibliografía en internet para que tengas nociones de este desarrollo.

#### 1. Ya hemos estimado las probabilidades conjuntas de que el equipo de casa anote X=x goles (x=0,1,... ,8), y el equipo visitante anote Y=y goles (y=0,1,... ,6), en un partido. Obtén una tabla de cocientes al dividir estas probabilidades conjuntas por el producto de las probabilidades marginales correspondientes.

Del postwork 3 

Primero creamos una nueva columna de ceros con la misma longitud que el dataframe Conj, el cual contiene la informacion de goles como local, goles como visitante y la probabilidad conjunta.
```R
Conj[, 4] = rep(0, length(Conj[,1]))
```
Luego llenamos esta columna con el producto de las probabilidades marginales de obtener X goles como local y Y goles como visitante. Por ejemplo, los productos de las probabilidades marginales de obtener 0 goles como visitante y 0, 1, 2, 3, 4, 5 o 6 goles como local.
Para esto empleamos un ciclo anidado tal que para cada elemento de Conj (conjunto de goles local y visitante) cheque si el numero de goles en la columna local y visit de Conj coincide con los que hay en la tabla visit y local, y si lo satisface, que multiplique sus probabilidades marginales y los guarde en su lugar correspondiente dentro de la columna 4 de Conj. 
```R
for(i in 1:length(Conj[,1])){
    for (j in 1:length(Local$Goles)) {
      for (k in 1:length(Visit$Goles)) {
        if((Conj[i,1] == Local[j,1]) & (Conj[i,2] == Visit[k,1])){
          Conj[i,4] = Local[j,2] * Visit[k,2]
        }
      }
    }
  }
```

```R
head(Conj)
```
![alt_text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork4/tabla_conj_prod_marg.png)


Renombramos esta columna llamada V4 como "Prod_Marg" y dividimos entre 100 dado que nosotros mostramos las probabilidades marginales individuales como porcentajes, de esta forma el producto de las probabilidades nos quedaría como porcentaje también.
```R
  Conj <- rename(Conj, Prod_Marg = V4)
  Conj[,"Prod_Marg"] <- Conj[,"Prod_Marg"] / 100
```
y por ultimo definimos la columna cociente como la division entre la probabilidad conjunta y el producto de las probabilidades marginales  
```R
  Conj[, "Cociente"] <- Conj$Probabilidad/Conj$Prod_Marg; head(Conj)
```


![alt_text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork4/tabla_conj_cociente.png)



#### 2. Mediante un procedimiento de bootstrap, obtén más cocientes similares a los obtenidos en la tabla del punto anterior. Esto para tener una idea de las distribuciones de la cual vienen los cocientes en la tabla anterior. Menciona en cuáles casos le parece razonable suponer que los cocientes de la tabla en el punto 1, son iguales a 1 (en tal caso tendríamos independencia de las variables aleatorias X y Y).
##### ¿Qué es Bootstrap?
En lugar de tomar muchas muestras de una población, podemos obtener réplicas (muestras con reemplazamiento) de la muestra original. Todas las réplicas deben tener el mismo tamaño que la muestra original: n.

La distribución bootstrap del estadístico se obtiene a partir de estas muestras y sirve para estimar la distribución del estadístico.

Dado que se nos pide utilizar un procedimiento de bootstrap, investigamos la forma en que este se podía implementar y optamos por utilizar la siguiente libreria llamada "rsample" la cuál contine un función bootstraps( ) que nos regresa un arreglo cuadrangular que incluye una columna con las muestras bootstrap y un identificador del número y tipo de muestra.

Empecemos por cargar nuestra libreria con library(rsample); NOTA: Recuerda que tenemos que instalar previamente la libreria.
Y creando una semilla aleatoria para que obtengamos los mismo resultados después, y declarando una constante n que representará el número de muestras que generaremos.

```R
library(rsample)
  set.seed(1111)
  n = 10000
```

Ahora guardemos en una variable "muestras" nuestras muestras generadas por la función bootstrap que como podremos ver se le pasan como parámetros nuestro dataframe que representa nuestra muestra original y el parámetro n que representa nuestr número de muestras que queremos generar.

```R
muestras <- bootstraps(Conj, times = n)
```

En la variable muestras como bien mencionamos en la explicación de arriba estará compuestá por dos columnas la primera con las muestras y la segunda por un identificador, las muestras se guardan en splits de la siguiente forma:
Ejecutemos un head(muestras) para observar como se estan guardando:
```R
head(muestras)
```
![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork4/muestras.PNG) <br/>
Ahora bien tenemos que sacar la media de cada una de nuestras muestras e irlas almacenando para después gráficarlas por lo que generaremos un vector para ahí irlas guardando, nosotros utilizamos un ciclo para ir recorriendo cada una de nuestras muestras e ir obteniendo la media de cada una de ellas, por lo que para sacar del split cada una de las muestras utilizamos as.data.frame como solución.

```R
  Medias <- c()
  for (i in 1:n) {
    Muest_Prueba <- as.data.frame(muestras$splits[[i]])
    Medias[i] <- mean(Muest_Prueba$Cociente)
  }
```
De igual forma realicemos un head a medias para ver cuales son nuestros resultados y un summary para ver nuestro max y min.
```R
head(Medias)
summary(Medias)
```
![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork4/medias.PNG) <br/>
Como podemos ver todo va a la perfección, ya solo nos queda ver gráficamente como se ven nuestras medias en un histograma, así que gráficando nuestro vector de Medias.

```R
Graph <- ggplot() + 
          geom_histogram(aes(Medias), bins = 50, col="black", fill = "yellow") + 
          geom_vline(aes(xintercept = mean(Medias)), linetype = "dashed", color = "red") +
          ggtitle('Histograma de la distribución de las medias muestrales.')+
          ylab("Frecuencias")
Graph
ggplotly(Graph)
```
![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork4/Graph.png)

Podemos observar que tenemos una distribución normal para nuestro gráfico con el vector de Medias, dado que se puede apreciar la forma de una Camapana de Gauss. 

Para la parte de nuestra hipótesis dada sobre decidir si nuestras Medias obtenidas son independientes o dependientes se propuso de la siguiente forma: <br/>
H<sub>0</sub>: μ = 1 (Las variables son Independientes) vs H<sub>a</sub>: μ ≠  1  (Las variables son Dependientes) <br/>
Empleamos la función t.test para comprobar la hipótesis y estos fueron los resultados
```R
t.test(Medias, alternative = "two.sided", mu = 1)
```
![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork4/test.PNG)

Dado que nos resulto el p-value= 2.2e-16 y esto es menor a 1 podemos rechazar nuestra Hipótesis nula sobre que nuestras variables son independientes y aceptar la Hipótesis alternativa sobre que nuestras variables Goles de Local y Goles de Visita son <strong>Dependientes.</strong>
### Postwork 5

### Postwork 6

### Postwork 7

### Postwork 8
