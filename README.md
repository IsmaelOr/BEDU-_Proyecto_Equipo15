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
