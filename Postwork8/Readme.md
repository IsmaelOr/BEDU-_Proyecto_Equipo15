# Postwork sesión 8. Dashboard 

#### OBJETIVO
 
- Observar el resultado de la toma de desiciones consecutivas, cuando estas se basan en datos históricos 

#### DESARROLLO

Para este postwork se generara un dasboard del modo que solo se genero un solo archivo de codigo `app.R`

- Se ejecuta el código `momios.R`

- Almacena los gráficos resultantes en formato `png` 

- Crea un dashboard donde se muestren los resultados con 4 pestañas:
   
- Una pestaña con gráficas de barras, donde en el eje de las _X_ se muestren los goles de local y visitante, con un menu de selección (en _choices_ deben aparecer éstas variables), utiliza la geometría de tipo _barras_, además de hacer un facet_wrap con la variable de el _equipo visitante_
   
- Realiza una pestaña donde agregues las imágenes de las gráficas del postwork 3
    
- En otra pestaña coloca el data table del fichero `match.data.csv` 
    
- Por último en otra pestaña agrega las imágenes de las gráficas de los factores de ganancia promedio y máximo
















Postwork 8

```R
library(shiny)
library(shinydashboard)
library(shinythemes)
```

```R
data <- read.csv("https://raw.githubusercontent.com/beduExpert/Programacion-R-Santander-2021/main/Sesion-08/Postwork/match.data.csv")
```
```R
# Define UI for application that draws a histogram
ui <- fluidPage(

    dashboardPage(
        
        skin = "red",
```

```R
        dashboardHeader(title = "PostWork8"),
        
        dashboardSidebar(
            sidebarMenu(
                menuItem("Gráfico de Barras", tabName = "graph", icon = icon("dashboard")),
                menuItem("Imagenes PW3", tabName = "img", icon = icon("file-picture-o")),
                menuItem("Data Table", tabName = "data_table", icon = icon("table")),
                menuItem("Imagenes", tabName = "img2", icon = icon("file-picture-o"))
            )
        ),
```

```R
        dashboardBody(        
            tabItems(
```

```R
                tabItem(tabName = "graph",
                        fluidRow(
                            titlePanel(h1("Goles a favor y goles en contra por cada equipo")),
                            selectInput("x", "Seleccione la variable a graficar:",
                                        choices = c("home.score", "away.score")),
                            plotOutput("plot1", height = 500, width = 800))
                        ),
```    
   
```R   
                tabItem(tabName = "img",
                        fluidRow(
                            titlePanel(h1("Imagenes PW3")),
                            h2(" - Probabilidades marginales de goles de equipos Locales"),
                            img(src = "pw3_1.png", height = 616, width = 1021),
                            h2(" - Probabilidades marginales de goles de equipos de Visitantes"),
                            img(src = "pw3_2.png", height = 613, width = 1022),
                            h2(" - Heatmap"),
                            img(src = "pw3_3.png", height = 612, width = 1022)
                        )),
```                
                
```R                
                tabItem(tabName = "data_table",
                        fluidRow(
                            titlePanel(h1("Data Table de 'match.data.csv'")),
                            dataTableOutput("data_table")
                        )),
```

```R
                tabItem(tabName = "img2",
                        fluidRow(
                            titlePanel(h1("Imagenes")),
                            h3(" - Factor de ganancia Máximo"),
                            img(src = "grafico1.png", height = 303 * 1.5),
                            h3(" - Factor de ganancia Promedio"),
                            img(src = "grafico2.png", height = 303 * 1.5)
                        ))
            )
        )
    )
)
```

```R
# Define server logic required to draw a histogram
server <- function(input, output) {
```

```R
    library(ggplot2)
    library(plotly)
```

```R
    output$data_table <- renderDataTable(
        {data},
        options = list(aLengthMenu = c(5, 10, 50, 100), iDisplayLength = 5)
    )
```    
```R    
    output$plot1 <- renderPlot({
        
        ?ifelse
        data <- mutate(data, FTR = ifelse(home.score > away.score, "H", ifelse(home.score < away.score, "A", "E")))
        x <- data[, input$x]
        
        data %>% ggplot(aes(x, fill = FTR)) +
            geom_bar() +
            facet_wrap("away.team") +
            labs(x = input$x, y = "Total Goles") +
            ylim(0, 100) +
            xlim(0, 10)
        
    })
    
}
```
```R
# Run the application 
shinyApp(ui = ui, server = server)
```
