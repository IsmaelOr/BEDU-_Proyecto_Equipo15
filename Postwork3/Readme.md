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
Para realizar las gráficas de las probabilidades marginales, primero estas se almacenan en un dataframe.
```R
Local <- as.data.frame(P_GCasa)
colnames(Local) <- c("Goles","Probabilidad"); Local
```
!<center>[alt text](https://github.com/IsmaelOr/BEDU_Proyecto_Equipo15/blob/main/Imagenes/Postwork3/2.1.jpg)</center>
##### * Un gráfico de barras para las probabilidades marginales estimadas del número de goles que anota el equipo visitante.
##### * Un HeatMap para las probabilidades conjuntas estimadas de los números de goles que anotan el equipo de casa y el equipo visitante en un partido.
