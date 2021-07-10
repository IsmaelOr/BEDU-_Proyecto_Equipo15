# Postwork Sesión 5

## :dart: Objetivo

- Continuar con el desarrollo de los postworks; en esta ocasión se utiliza la función `predict` para realizar predicciones de los resultados de partidos para una fecha determinada

## 🔧 Requisitos

- Haber desarrollado los postworks anteriores
- Cubrir los temas del prework
- Replicar los ejemplos de la sesión

## 🤓 Desarrollo

1. A partir del conjunto de datos de soccer de la liga española de las temporadas 2017/2018, 2018/2019 y 2019/2020, crea el data frame `SmallData`, que contenga las columnas `date`, `home.team`, `home.score`, `away.team` y `away.score`; esto lo puede hacer con ayuda de la función `select` del paquete `dplyr`. Luego establece un directorio de trabajo y con ayuda de la función `write.csv` guarda el data frame como un archivo csv con nombre *soccer.csv*. Puedes colocar como argumento `row.names = FALSE` en `write.csv`. 

El conjunto de datos de las temporadas 2017 al 2020 lo tenemos almacenado en `Soccer` por lo que lo mandamos llamar retirando la columna FTR que no será necesaria y asignandolo a `SmallData` para posteriormente ordenar las columnas.
```R
SmallData <- select(Soccer, -FTR)
SmallData <- select(SmallData, Date, HomeTeam, FTHG, AwayTeam ,FTAG)
summary(SmallData)

```
De lo anterior obtenemos el siguiente resumen de `SmallData`
<p align = "center">
  <img src = "https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork5/SmallData_summary.PNG">
</p>



Verificando que la estructura del data frame es la adecuada usamos la función `colnames` para renombrar las columnas a como lo requiere `fbRanks`, con los datos en el orden y con el nombre que requerimos lo guardamos en un nuevo archivo csv. 
```R
colnames(SmallData) <- c("date", "home.team", "home.score", "away.team", "away.score")

write.csv(SmallData, file = "Soccer.csv", row.names = F)
```R

2. Con la función `create.fbRanks.dataframes` del paquete `fbRanks` importe el archivo *soccer.csv* a `R` y al mismo tiempo asignelo a una variable llamada `listasoccer`. Se creará una lista con los elementos `scores` y `teams` que son data frames listos para la función `rank.teams`. Asigna estos data frames a variables llamadas `anotaciones` y `equipos`.

```R
install.packages("fbRanks")
library(fbRanks)

listaSoccer <- create.fbRanks.dataframes(scores.file = "Soccer.csv")

anotaciones <- listaSoccer$scores
equipos <- listaSoccer$teams

```



3. Con ayuda de la función `unique` crea un vector de fechas (`fecha`) que no se repitan y que correspondan a las fechas en las que se jugaron partidos. Crea una variable llamada `n` que contenga el número de fechas diferentes. Posteriormente, con la función `rank.teams` y usando como argumentos los data frames `anotaciones` y `equipos`, crea un ranking de equipos usando únicamente datos desde la fecha inicial y hasta la penúltima fecha en la que se jugaron partidos, estas fechas las deberá especificar en `max.date` y `min.date`. Guarda los resultados con el nombre `ranking`.

4. Finalmente estima las probabilidades de los eventos, el equipo de casa gana, el equipo visitante gana o el resultado es un empate para los partidos que se jugaron en la última fecha del vector de fechas `fecha`. Esto lo puedes hacer con ayuda de la función `predict` y usando como argumentos `ranking` y `fecha[n]` que deberá especificar en `date`.

