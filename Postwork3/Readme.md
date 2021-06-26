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
```R
x <- seq(-4, 4, 0.01)*6 + 175 # Algunos posibles valores que puede tomar la v.a. X (mínimo: mu-4sigma, máximo: mu+4sigma)
y <- dnorm(x, mean = 175, sd = 6) # Valores correspondientes de la función de densidad de probabilidad

plot(x, y, type = "l", xlab = "", ylab = "")
title(main = "Densidad de Probabilidad Normal", sub = expression(paste(mu == 175, " y ", sigma == 6)))
abline(v = 175, lwd = 2, lty = 2) # La media es 175 
```
![alt text](https://raw.githubusercontent.com/IsmaelOr/BEDU_Proyecto_Equipo15/main/Imagenes/Postwork3/Rplot.png)
##### * Un gráfico de barras para las probabilidades marginales estimadas del número de goles que anota el equipo visitante.
##### * Un HeatMap para las probabilidades conjuntas estimadas de los números de goles que anotan el equipo de casa y el equipo visitante en un partido.
