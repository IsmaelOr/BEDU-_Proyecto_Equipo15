# Postwork 3 - Análisis Exploratorio de Datos (AED o EDA) con R
## :dart: Objetivos
- Realizar descarga de archivos desde internet
- Generar nuevos data frames
- Visualizar probabilidades estimadas con la ayuda de gráficas

## 🔧 Requisitos
* R, RStudio
* Haber realizado el prework y seguir el curso de los ejemplos de la sesión
* Curiosidad por investigar nuevos tópicos y funciones de R

## 🤓 Desarrollo
Ahora graficaremos probabilidades (estimadas) marginales y conjuntas para el número de goles que anotan en un partido el equipo de casa o el equipo visitante.

#### 1. Con el último data frame obtenido en el postwork de la sesión 2, elabora tablas de frecuencias relativas para estimar las siguientes probabilidades:
##### * La probabilidad (marginal) de que el equipo que juega en casa anote x goles (x=0,1,2,)
##### * La probabilidad (marginal) de que el equipo que juega como visitante anote y goles (y=0,1,2,)
##### * La probabilidad (conjunta) de que el equipo que juega en casa anote x goles y el equipo que juega como visitante anote y goles (x=0,1,2,, y=0,1,2,)
#### 2. Realiza lo siguiente:
##### * Un gráfico de barras para las probabilidades marginales estimadas del número de goles que anota el equipo de casa.
Para realizar las gráficas de las probabilidades marginales, primero estas se almacenan en un dataframe. Se renombran las columnas para tener: "Goles" y "Probabilidad".
```R
Local <- as.data.frame(P_GCasa)
colnames(Local) <- c("Goles","Probabilidad"); Local
```
<p align = "center">
  <img src = "https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork3/2.1.jpg">
</p>

##### * Un gráfico de barras para las probabilidades marginales estimadas del número de goles que anota el equipo visitante.
De igual manera de como hicimos antes, primero, estas probabilidades se almacenan en un dataframe. Se renombran las columnas para tener: "Goles" y "Probabilidad".
```R
Visit <- as.data.frame(P_GVisitante)
colnames(Visit) <- c("Goles","Probabilidad"); Visit
```
<p align = "center">
  <img src = "https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork3/2.2.jpg">
</p>
##### * Un HeatMap para las probabilidades conjuntas estimadas de los números de goles que anotan el equipo de casa y el equipo visitante en un partido.
Por último, de igual manera se hace un dataframe con las probabilidades conjuntas tanto de los goles del equipo de casa como de los goles del equipo visitante. Se renombran las columnas para tener: "Goles_Local", "Goles_Visit" y "Probabilidad".
```R
Conj <- as.data.frame(P_Conj)
colnames(Conj) <- c("Goles_Local", "Goles_Visit","Probabilidad"); Conj
```
<p align = "center">
  <img src = "https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork3/2.3.jpg">
</p>
