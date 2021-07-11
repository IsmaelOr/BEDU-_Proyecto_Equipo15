# Postwork 6 - Series de tiempo
## :dart: Objetivo
Aprender a crear una serie de tiempo en R.

## 🔧 Requisitos
* Tener instalado R y RStudio
* Haber trabajado con el prework y el work

## 🤓 Desarrollo

**Importa el conjunto de datos match.data.csv a R y realiza lo siguiente:**

Definimos el dataframe *match.data* usando el url del archivo csv
```R
match.data <- read.csv("https://raw.githubusercontent.com/beduExpert/Programacion-R-Santander-2021/main/Sesion-06/Postwork/match.data.csv")
```
**Agrega una nueva columna sumagoles que contenga la suma de goles por partido.**

Creamos la columna *sumagoles* como la suma de las columnas 3 y 5, goles como local y goles como visitante, respectivamente.
```R
match.data[,'sumagoles'] <- match.data[, 3] + match.data[,5]
head(match.data)
```
![alt text]()


**Obtén el promedio por mes de la suma de goles.**

Antes de crear la columna de promedio por mes, tenemos que arreglar el formato de las fechas
```R
match.data <- mutate(match.data, date = as.Date(date,'%Y-%m-%d'))
```

Y creamos las columna year y month
```R
match.data[, 'year'] <- year(match.data$date)
match.data[,'month'] <- month(match.data$date)
```

Ya con esto hecho podemos crear el dataframe *datos* que almacena el promedio de la suma de goles por mes de cada año
```R
datos <- match.data %>% group_by(year, month) %>% summarize(promedio_goles = mean(sumagoles))
datos <- as.data.frame(datos);
head(datos)
```

![alt text]()

**Crea la serie de tiempo del promedio por mes de la suma de goles hasta diciembre de 2019.**

Ahora bien, antes de crear la serie de tiempo tenemos que hacer nuestro df regular, dado que los meses junio y julio de nuestros datos no tienen temporada de soccer, por lo tanto no hay goles en esos meses. Para esto crearemos un dataframe...
```R
fech <- paste(toString(datos$year[1]),"/8/1", sep = ""); #fecha inicial de los datos
fechf <- paste(toString(datos$year[length(datos[,1])]),"/12/1", sep = "") #fecha final de los datos
```
Creamos una secuencia de fechas %Y-%m-%d con todos los meses, incluidos junio y julio donde no hay temporadas de soccer, esta secuencia empieza en la fecha inicial *fech* y termina en la fecha final *fechf*. 
```R
Meses <- seq(as.Date(fech), as.Date(fechf), by = "month")
```
y creamos el dataframe *ft*, el cual contiene las columnas year y month desde "2010/8/1" hasta "2020/12/1".
```R
ft <- data.frame('year' = year(Meses), 'month' = month(Meses)); 
head(ft)
 ```
A continuacion uniremos los dataframes *ft* y *datos* en un nuevo df llamado *final*, de modo que para cada mes por año dentro de *ft* le corresponda el promedio de goles por mes dentro de *datos*, note que en los meses donde no hay temporada, junio y julio, devolverá un *NA*. 
Todo este proceso fue hecho para que nuestro dataframe *final* tenga todos los meses por año con su correspondiente promedio de goles por mes y así poder hacer una serie de tiempo regular. 
```R
final <- merge(x = datos, y = ft, by = c("month","year"), all = TRUE)
final
```

Rellenamos estos NA's con 0 y ordenamos el dataframe por año 
```R
final[is.na(final)] <- 0
final <- final[order(final$year),]
```

Por último creamos la serie de tiempo de los goles promedios por mes desde la fecha inicial hasta la final y con frecuencia de 12, por la cantidad de meses por año.
```R
Promedio_goles.ts <- ts(final$promedio_goles, start = c(2010,8), end = c(2019, 12), fr = 12)
Promedio_goles.ts
```

**Grafica la serie de tiempo.**


```R
plot(Promedio_goles.ts, xlab = "Tiempo", ylab = "Promedio de goles por mes", main = "Serie de Goles Promedio",
     sub = "Serie mensual: Agosto de 2010 a Diciembre de 2019")
```

obtenemos la siguiente serie de tiempo:

![alt text]()
