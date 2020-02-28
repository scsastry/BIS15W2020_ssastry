---
title: "Homework 7"
author: "Savita Sastry"
date: "2/26/2020"
output: 
  html_document: 
    keep_md: yes
---



## Libraries

```r
#install.packages("shiny")
library(shiny)
library(shiny)
library(shinydashboard)
```

```
## 
## Attaching package: 'shinydashboard'
```

```
## The following object is masked from 'package:graphics':
## 
##     box
```

## Data
The data for this assignment come from the [University of California Information Center](https://www.universityofcalifornia.edu/infocenter). Admissions data were collected for the years 2010-2019 for each UC campus. Admissions are broken down into three categories: applications, admits, and enrollees. The number of individuals in each category are presented by demographic.  

```r
UC_admit <- readr::read_csv("data/UC_admit.csv")
```

```
## Parsed with column specification:
## cols(
##   Campus = col_character(),
##   Academic_Yr = col_double(),
##   Category = col_character(),
##   Ethnicity = col_character(),
##   `Perc FR` = col_character(),
##   FilteredCountFR = col_double()
## )
```


```r
UC_admit
```

```
## # A tibble: 2,160 x 6
##    Campus Academic_Yr Category   Ethnicity        `Perc FR` FilteredCountFR
##    <chr>        <dbl> <chr>      <chr>            <chr>               <dbl>
##  1 Davis         2019 Applicants International    21.16%              16522
##  2 Davis         2019 Applicants Unknown          2.51%                1959
##  3 Davis         2019 Applicants White            18.39%              14360
##  4 Davis         2019 Applicants Asian            30.76%              24024
##  5 Davis         2019 Applicants Chicano/Latino   22.44%              17526
##  6 Davis         2019 Applicants American Indian  0.35%                 277
##  7 Davis         2019 Applicants African American 4.39%                3425
##  8 Davis         2019 Applicants All              100.00%             78093
##  9 Davis         2018 Applicants International    19.87%              15507
## 10 Davis         2018 Applicants Unknown          2.83%                2208
## # ... with 2,150 more rows
```



**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine if there are NA's and how they are treated.**  


```r
colnames(UC_admit)
```

```
## [1] "Campus"          "Academic_Yr"     "Category"        "Ethnicity"      
## [5] "Perc FR"         "FilteredCountFR"
```



```r
str(UC_admit)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	2160 obs. of  6 variables:
##  $ Campus         : chr  "Davis" "Davis" "Davis" "Davis" ...
##  $ Academic_Yr    : num  2019 2019 2019 2019 2019 ...
##  $ Category       : chr  "Applicants" "Applicants" "Applicants" "Applicants" ...
##  $ Ethnicity      : chr  "International" "Unknown" "White" "Asian" ...
##  $ Perc FR        : chr  "21.16%" "2.51%" "18.39%" "30.76%" ...
##  $ FilteredCountFR: num  16522 1959 14360 24024 17526 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   Campus = col_character(),
##   ..   Academic_Yr = col_double(),
##   ..   Category = col_character(),
##   ..   Ethnicity = col_character(),
##   ..   `Perc FR` = col_character(),
##   ..   FilteredCountFR = col_double()
##   .. )
```


```r
dim(UC_admit)
```

```
## [1] 2160    6
```



```r
which(is.na(UC_admit$`Perc FR`))
```

```
## [1] 1177
```


```r
which(is.na(UC_admit$FilteredCountFR))
```

```
## [1] 1177
```


```r
UC_admit[1177,]
```

```
## # A tibble: 1 x 6
##   Campus Academic_Yr Category  Ethnicity     `Perc FR` FilteredCountFR
##   <chr>        <dbl> <chr>     <chr>         <chr>               <dbl>
## 1 Merced        2012 Enrollees International <NA>                   NA
```


```r
UC_admit$Campus <- as.factor(UC_admit$Campus)
UC_admit$Category <- as.factor(UC_admit$Category)
UC_admit$Ethnicity <- as.factor(UC_admit$Ethnicity)
```

**2. The president of UC has asked you to build a shiny app that shows admissions by ethnicity across all UC campuses. Your app should allow users to explore year, campus, and admit category as interactive variables. Use shiny dashboard and try to incorporate the aesthetics you have learned in ggplot to make the app neat and clean.**


```r
ui <- dashboardPage(
  dashboardHeader(title = "UC Campus Diversity Dashboard"),
  dashboardSidebar(),
  dashboardBody(
  fluidRow(
  box(title = "Plot Options", width = 10,
  selectInput("x", "Select Variable", choices = c("Campus", "Category"),
              selected = "Campus"),
  sliderInput("Academic_Yr", "Select Academic Year", min = 2010, max = 2019, value = 2019, step = 1)
  ), 
  box(title = "Plot of UC Diversity", width = 10,
  plotOutput("plot", width = "600px", height = "500px")
  ) 
  ) 
  ) 
) 

server <- function(input, output, session) { 
  
  
  output$plot <- renderPlot({
    ggplot(UC_admit, aes_string(x = input$x, y = "FilteredCountFR", fill = "Ethnicity" )) + geom_col(position = "dodge") + theme_light(base_size = 18)+
      coord_flip()
  })
  
  # stop the app when we close it
  session$onSessionEnded(stopApp)

  }

shinyApp(ui, server)
```

<!--html_preserve--><div style="width: 100% ; height: 400px ; text-align: center; box-sizing: border-box; -moz-box-sizing: border-box; -webkit-box-sizing: border-box;" class="muted well">Shiny applications not supported in static R Markdown documents</div><!--/html_preserve-->


**3. Make alternate version of your app above by tracking enrollment at a campus over all of the represented years while allowing users to interact with campus, category, and ethnicity.**


```r
ui <- dashboardPage(
  dashboardHeader(title = "UC Campus Enrollment Dashboard"),
  dashboardSidebar(),
  dashboardBody(
  fluidRow(
  box(title = "Plot Options", width = 10,
  selectInput("x", "Select Variable", choices = c("Ethnicity","Campus", "Category"),
              selected = "Ethnicity"),
  sliderInput("Academic_Yr", "Select Academic Year", min = 2010, max = 2019, value = 2019, step = 1)
  ), 
  box(title = "Plot of UC Enrollment", width = 10,
  plotOutput("plot", width = "600px", height = "500px")
  ) 
  ) 
  ) 
) 

server <- function(input, output, session) { 
  
  
  output$plot <- renderPlot({
    ggplot(UC_admit, aes_string(x = "Academic_Yr", y = "FilteredCountFR", fill = input$x )) + geom_col(position = "dodge") + theme_light(base_size = 18)+
      coord_flip()
  })
  
  # stop the app when we close it
  session$onSessionEnded(stopApp)

  }

shinyApp(ui, server)
```

<!--html_preserve--><div style="width: 100% ; height: 400px ; text-align: center; box-sizing: border-box; -moz-box-sizing: border-box; -webkit-box-sizing: border-box;" class="muted well">Shiny applications not supported in static R Markdown documents</div><!--/html_preserve-->

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
