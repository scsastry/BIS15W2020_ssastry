---
title: "Homework 4"
author: "Savita Sastry"
date: "2/4/2020"
output: 
  html_document: 
    keep_md: yes
---




```r
library(tidyverse)
```


```r
getwd()
```

```
## [1] "C:/Users/Savita/Documents/GitHub/BIS15W2020_ssastry/Homeworks"
```


```r
fisheries <- readr::read_csv("C:/Users/Savita/Documents/GitHub/BIS15W2020_ssastry/lab4/data/FAO_1950to2012_111914.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   `ISSCAAP group#` = col_double(),
##   `FAO major fishing area` = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

```r
fisheries
```

```
## # A tibble: 17,692 x 71
##    Country `Common name` `ISSCAAP group#` `ISSCAAP taxono~ `ASFIS species#`
##    <chr>   <chr>                    <dbl> <chr>            <chr>           
##  1 Albania Angelsharks,~               38 Sharks, rays, c~ 10903XXXXX      
##  2 Albania Atlantic bon~               36 Tunas, bonitos,~ 1750100101      
##  3 Albania Barracudas n~               37 Miscellaneous p~ 17710001XX      
##  4 Albania Blue and red~               45 Shrimps, prawns  2280203101      
##  5 Albania Blue whiting~               32 Cods, hakes, ha~ 1480403301      
##  6 Albania Bluefish                    37 Miscellaneous p~ 1702021301      
##  7 Albania Bogue                       33 Miscellaneous c~ 1703926101      
##  8 Albania Caramote pra~               45 Shrimps, prawns  2280100117      
##  9 Albania Catsharks, n~               38 Sharks, rays, c~ 10801003XX      
## 10 Albania Common cuttl~               57 Squids, cuttlef~ 3210200202      
## # ... with 17,682 more rows, and 66 more variables: `ASFIS species
## #   name` <chr>, `FAO major fishing area` <dbl>, Measure <chr>,
## #   `1950` <chr>, `1951` <chr>, `1952` <chr>, `1953` <chr>, `1954` <chr>,
## #   `1955` <chr>, `1956` <chr>, `1957` <chr>, `1958` <chr>, `1959` <chr>,
## #   `1960` <chr>, `1961` <chr>, `1962` <chr>, `1963` <chr>, `1964` <chr>,
## #   `1965` <chr>, `1966` <chr>, `1967` <chr>, `1968` <chr>, `1969` <chr>,
## #   `1970` <chr>, `1971` <chr>, `1972` <chr>, `1973` <chr>, `1974` <chr>,
## #   `1975` <chr>, `1976` <chr>, `1977` <chr>, `1978` <chr>, `1979` <chr>,
## #   `1980` <chr>, `1981` <chr>, `1982` <chr>, `1983` <chr>, `1984` <chr>,
## #   `1985` <chr>, `1986` <chr>, `1987` <chr>, `1988` <chr>, `1989` <chr>,
## #   `1990` <chr>, `1991` <chr>, `1992` <chr>, `1993` <chr>, `1994` <chr>,
## #   `1995` <chr>, `1996` <chr>, `1997` <chr>, `1998` <chr>, `1999` <chr>,
## #   `2000` <chr>, `2001` <chr>, `2002` <chr>, `2003` <chr>, `2004` <chr>,
## #   `2005` <chr>, `2006` <chr>, `2007` <chr>, `2008` <chr>, `2009` <chr>,
## #   `2010` <chr>, `2011` <chr>, `2012` <chr>
```

2. What are the names of the columns? Do you see any potential problems with the column names?

```r
colnames(fisheries)
```

```
##  [1] "Country"                 "Common name"            
##  [3] "ISSCAAP group#"          "ISSCAAP taxonomic group"
##  [5] "ASFIS species#"          "ASFIS species name"     
##  [7] "FAO major fishing area"  "Measure"                
##  [9] "1950"                    "1951"                   
## [11] "1952"                    "1953"                   
## [13] "1954"                    "1955"                   
## [15] "1956"                    "1957"                   
## [17] "1958"                    "1959"                   
## [19] "1960"                    "1961"                   
## [21] "1962"                    "1963"                   
## [23] "1964"                    "1965"                   
## [25] "1966"                    "1967"                   
## [27] "1968"                    "1969"                   
## [29] "1970"                    "1971"                   
## [31] "1972"                    "1973"                   
## [33] "1974"                    "1975"                   
## [35] "1976"                    "1977"                   
## [37] "1978"                    "1979"                   
## [39] "1980"                    "1981"                   
## [41] "1982"                    "1983"                   
## [43] "1984"                    "1985"                   
## [45] "1986"                    "1987"                   
## [47] "1988"                    "1989"                   
## [49] "1990"                    "1991"                   
## [51] "1992"                    "1993"                   
## [53] "1994"                    "1995"                   
## [55] "1996"                    "1997"                   
## [57] "1998"                    "1999"                   
## [59] "2000"                    "2001"                   
## [61] "2002"                    "2003"                   
## [63] "2004"                    "2005"                   
## [65] "2006"                    "2007"                   
## [67] "2008"                    "2009"                   
## [69] "2010"                    "2011"                   
## [71] "2012"
```

```r
#Problems with the current column names include it having all the years as columns as well as other stratifications that are not dates. Looks like untidy data
```

3. What is the structure of the data? Show the classes of each variable.


```r
str(fisheries)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	17692 obs. of  71 variables:
##  $ Country                : chr  "Albania" "Albania" "Albania" "Albania" ...
##  $ Common name            : chr  "Angelsharks, sand devils nei" "Atlantic bonito" "Barracudas nei" "Blue and red shrimp" ...
##  $ ISSCAAP group#         : num  38 36 37 45 32 37 33 45 38 57 ...
##  $ ISSCAAP taxonomic group: chr  "Sharks, rays, chimaeras" "Tunas, bonitos, billfishes" "Miscellaneous pelagic fishes" "Shrimps, prawns" ...
##  $ ASFIS species#         : chr  "10903XXXXX" "1750100101" "17710001XX" "2280203101" ...
##  $ ASFIS species name     : chr  "Squatinidae" "Sarda sarda" "Sphyraena spp" "Aristeus antennatus" ...
##  $ FAO major fishing area : num  37 37 37 37 37 37 37 37 37 37 ...
##  $ Measure                : chr  "Quantity (tonnes)" "Quantity (tonnes)" "Quantity (tonnes)" "Quantity (tonnes)" ...
##  $ 1950                   : chr  NA NA NA NA ...
##  $ 1951                   : chr  NA NA NA NA ...
##  $ 1952                   : chr  NA NA NA NA ...
##  $ 1953                   : chr  NA NA NA NA ...
##  $ 1954                   : chr  NA NA NA NA ...
##  $ 1955                   : chr  NA NA NA NA ...
##  $ 1956                   : chr  NA NA NA NA ...
##  $ 1957                   : chr  NA NA NA NA ...
##  $ 1958                   : chr  NA NA NA NA ...
##  $ 1959                   : chr  NA NA NA NA ...
##  $ 1960                   : chr  NA NA NA NA ...
##  $ 1961                   : chr  NA NA NA NA ...
##  $ 1962                   : chr  NA NA NA NA ...
##  $ 1963                   : chr  NA NA NA NA ...
##  $ 1964                   : chr  NA NA NA NA ...
##  $ 1965                   : chr  NA NA NA NA ...
##  $ 1966                   : chr  NA NA NA NA ...
##  $ 1967                   : chr  NA NA NA NA ...
##  $ 1968                   : chr  NA NA NA NA ...
##  $ 1969                   : chr  NA NA NA NA ...
##  $ 1970                   : chr  NA NA NA NA ...
##  $ 1971                   : chr  NA NA NA NA ...
##  $ 1972                   : chr  NA NA NA NA ...
##  $ 1973                   : chr  NA NA NA NA ...
##  $ 1974                   : chr  NA NA NA NA ...
##  $ 1975                   : chr  NA NA NA NA ...
##  $ 1976                   : chr  NA NA NA NA ...
##  $ 1977                   : chr  NA NA NA NA ...
##  $ 1978                   : chr  NA NA NA NA ...
##  $ 1979                   : chr  NA NA NA NA ...
##  $ 1980                   : chr  NA NA NA NA ...
##  $ 1981                   : chr  NA NA NA NA ...
##  $ 1982                   : chr  NA NA NA NA ...
##  $ 1983                   : chr  NA NA NA NA ...
##  $ 1984                   : chr  NA NA NA NA ...
##  $ 1985                   : chr  NA NA NA NA ...
##  $ 1986                   : chr  NA NA NA NA ...
##  $ 1987                   : chr  NA NA NA NA ...
##  $ 1988                   : chr  NA NA NA NA ...
##  $ 1989                   : chr  NA NA NA NA ...
##  $ 1990                   : chr  NA NA NA NA ...
##  $ 1991                   : chr  NA NA NA NA ...
##  $ 1992                   : chr  NA NA NA NA ...
##  $ 1993                   : chr  NA NA NA NA ...
##  $ 1994                   : chr  NA NA NA NA ...
##  $ 1995                   : chr  "0 0" "1" NA "0 0" ...
##  $ 1996                   : chr  "53" "2" NA "3" ...
##  $ 1997                   : chr  "20" "0 0" NA "0 0" ...
##  $ 1998                   : chr  "31" "12" NA NA ...
##  $ 1999                   : chr  "30" "30" NA NA ...
##  $ 2000                   : chr  "30" "25" "2" NA ...
##  $ 2001                   : chr  "16" "30" NA NA ...
##  $ 2002                   : chr  "79" "24" NA "34" ...
##  $ 2003                   : chr  "1" "4" NA "22" ...
##  $ 2004                   : chr  "4" "2" "2" "15" ...
##  $ 2005                   : chr  "68" "23" "4" "12" ...
##  $ 2006                   : chr  "55" "30" "7" "18" ...
##  $ 2007                   : chr  "12" "19" NA NA ...
##  $ 2008                   : chr  "23" "27" NA NA ...
##  $ 2009                   : chr  "14" "21" NA NA ...
##  $ 2010                   : chr  "78" "23" "7" NA ...
##  $ 2011                   : chr  "12" "12" NA NA ...
##  $ 2012                   : chr  "5" "5" NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   Country = col_character(),
##   ..   `Common name` = col_character(),
##   ..   `ISSCAAP group#` = col_double(),
##   ..   `ISSCAAP taxonomic group` = col_character(),
##   ..   `ASFIS species#` = col_character(),
##   ..   `ASFIS species name` = col_character(),
##   ..   `FAO major fishing area` = col_double(),
##   ..   Measure = col_character(),
##   ..   `1950` = col_character(),
##   ..   `1951` = col_character(),
##   ..   `1952` = col_character(),
##   ..   `1953` = col_character(),
##   ..   `1954` = col_character(),
##   ..   `1955` = col_character(),
##   ..   `1956` = col_character(),
##   ..   `1957` = col_character(),
##   ..   `1958` = col_character(),
##   ..   `1959` = col_character(),
##   ..   `1960` = col_character(),
##   ..   `1961` = col_character(),
##   ..   `1962` = col_character(),
##   ..   `1963` = col_character(),
##   ..   `1964` = col_character(),
##   ..   `1965` = col_character(),
##   ..   `1966` = col_character(),
##   ..   `1967` = col_character(),
##   ..   `1968` = col_character(),
##   ..   `1969` = col_character(),
##   ..   `1970` = col_character(),
##   ..   `1971` = col_character(),
##   ..   `1972` = col_character(),
##   ..   `1973` = col_character(),
##   ..   `1974` = col_character(),
##   ..   `1975` = col_character(),
##   ..   `1976` = col_character(),
##   ..   `1977` = col_character(),
##   ..   `1978` = col_character(),
##   ..   `1979` = col_character(),
##   ..   `1980` = col_character(),
##   ..   `1981` = col_character(),
##   ..   `1982` = col_character(),
##   ..   `1983` = col_character(),
##   ..   `1984` = col_character(),
##   ..   `1985` = col_character(),
##   ..   `1986` = col_character(),
##   ..   `1987` = col_character(),
##   ..   `1988` = col_character(),
##   ..   `1989` = col_character(),
##   ..   `1990` = col_character(),
##   ..   `1991` = col_character(),
##   ..   `1992` = col_character(),
##   ..   `1993` = col_character(),
##   ..   `1994` = col_character(),
##   ..   `1995` = col_character(),
##   ..   `1996` = col_character(),
##   ..   `1997` = col_character(),
##   ..   `1998` = col_character(),
##   ..   `1999` = col_character(),
##   ..   `2000` = col_character(),
##   ..   `2001` = col_character(),
##   ..   `2002` = col_character(),
##   ..   `2003` = col_character(),
##   ..   `2004` = col_character(),
##   ..   `2005` = col_character(),
##   ..   `2006` = col_character(),
##   ..   `2007` = col_character(),
##   ..   `2008` = col_character(),
##   ..   `2009` = col_character(),
##   ..   `2010` = col_character(),
##   ..   `2011` = col_character(),
##   ..   `2012` = col_character()
##   .. )
```


```r
sapply(fisheries, class)
```

```
##                 Country             Common name          ISSCAAP group# 
##             "character"             "character"               "numeric" 
## ISSCAAP taxonomic group          ASFIS species#      ASFIS species name 
##             "character"             "character"             "character" 
##  FAO major fishing area                 Measure                    1950 
##               "numeric"             "character"             "character" 
##                    1951                    1952                    1953 
##             "character"             "character"             "character" 
##                    1954                    1955                    1956 
##             "character"             "character"             "character" 
##                    1957                    1958                    1959 
##             "character"             "character"             "character" 
##                    1960                    1961                    1962 
##             "character"             "character"             "character" 
##                    1963                    1964                    1965 
##             "character"             "character"             "character" 
##                    1966                    1967                    1968 
##             "character"             "character"             "character" 
##                    1969                    1970                    1971 
##             "character"             "character"             "character" 
##                    1972                    1973                    1974 
##             "character"             "character"             "character" 
##                    1975                    1976                    1977 
##             "character"             "character"             "character" 
##                    1978                    1979                    1980 
##             "character"             "character"             "character" 
##                    1981                    1982                    1983 
##             "character"             "character"             "character" 
##                    1984                    1985                    1986 
##             "character"             "character"             "character" 
##                    1987                    1988                    1989 
##             "character"             "character"             "character" 
##                    1990                    1991                    1992 
##             "character"             "character"             "character" 
##                    1993                    1994                    1995 
##             "character"             "character"             "character" 
##                    1996                    1997                    1998 
##             "character"             "character"             "character" 
##                    1999                    2000                    2001 
##             "character"             "character"             "character" 
##                    2002                    2003                    2004 
##             "character"             "character"             "character" 
##                    2005                    2006                    2007 
##             "character"             "character"             "character" 
##                    2008                    2009                    2010 
##             "character"             "character"             "character" 
##                    2011                    2012 
##             "character"             "character"
```

4. Think about the classes. Will any present problems? Make any changes you think are necessary below.


```r
#change values in the dates columns from character to numeric
fisheries[9:71] <- lapply(fisheries[9:71], as.numeric)
```

```
## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion

## Warning in lapply(fisheries[9:71], as.numeric): NAs introduced by coercion
```

```r
sapply(fisheries, class)
```

```
##                 Country             Common name          ISSCAAP group# 
##             "character"             "character"               "numeric" 
## ISSCAAP taxonomic group          ASFIS species#      ASFIS species name 
##             "character"             "character"             "character" 
##  FAO major fishing area                 Measure                    1950 
##               "numeric"             "character"               "numeric" 
##                    1951                    1952                    1953 
##               "numeric"               "numeric"               "numeric" 
##                    1954                    1955                    1956 
##               "numeric"               "numeric"               "numeric" 
##                    1957                    1958                    1959 
##               "numeric"               "numeric"               "numeric" 
##                    1960                    1961                    1962 
##               "numeric"               "numeric"               "numeric" 
##                    1963                    1964                    1965 
##               "numeric"               "numeric"               "numeric" 
##                    1966                    1967                    1968 
##               "numeric"               "numeric"               "numeric" 
##                    1969                    1970                    1971 
##               "numeric"               "numeric"               "numeric" 
##                    1972                    1973                    1974 
##               "numeric"               "numeric"               "numeric" 
##                    1975                    1976                    1977 
##               "numeric"               "numeric"               "numeric" 
##                    1978                    1979                    1980 
##               "numeric"               "numeric"               "numeric" 
##                    1981                    1982                    1983 
##               "numeric"               "numeric"               "numeric" 
##                    1984                    1985                    1986 
##               "numeric"               "numeric"               "numeric" 
##                    1987                    1988                    1989 
##               "numeric"               "numeric"               "numeric" 
##                    1990                    1991                    1992 
##               "numeric"               "numeric"               "numeric" 
##                    1993                    1994                    1995 
##               "numeric"               "numeric"               "numeric" 
##                    1996                    1997                    1998 
##               "numeric"               "numeric"               "numeric" 
##                    1999                    2000                    2001 
##               "numeric"               "numeric"               "numeric" 
##                    2002                    2003                    2004 
##               "numeric"               "numeric"               "numeric" 
##                    2005                    2006                    2007 
##               "numeric"               "numeric"               "numeric" 
##                    2008                    2009                    2010 
##               "numeric"               "numeric"               "numeric" 
##                    2011                    2012 
##               "numeric"               "numeric"
```

5. How many countries are represented in the data? Provide a count.


```r
#There are 204 countries represented in this data set
length(unique(fisheries$Country))
```

```
## [1] 204
```

6. What are the names of the countries?


```r
unique(fisheries$Country)
```

```
##   [1] "Albania"                   "Algeria"                  
##   [3] "American Samoa"            "Angola"                   
##   [5] "Anguilla"                  "Antigua and Barbuda"      
##   [7] "Argentina"                 "Aruba"                    
##   [9] "Australia"                 "Bahamas"                  
##  [11] "Bahrain"                   "Bangladesh"               
##  [13] "Barbados"                  "Belgium"                  
##  [15] "Belize"                    "Benin"                    
##  [17] "Bermuda"                   "Bonaire/S.Eustatius/Saba" 
##  [19] "Bosnia and Herzegovina"    "Brazil"                   
##  [21] "British Indian Ocean Ter"  "British Virgin Islands"   
##  [23] "Brunei Darussalam"         "Bulgaria"                 
##  [25] "Cabo Verde"                "Cambodia"                 
##  [27] "Cameroon"                  "Canada"                   
##  [29] "Cayman Islands"            "Channel Islands"          
##  [31] "Chile"                     "China"                    
##  [33] "China, Hong Kong SAR"      "China, Macao SAR"         
##  [35] "Colombia"                  "Comoros"                  
##  [37] "Congo, Dem. Rep. of the"   "Congo, Republic of"       
##  [39] "Cook Islands"              "Costa Rica"               
##  [41] "Croatia"                   "Cuba"                     
##  [43] "Cura<e7>ao"                "Cyprus"                   
##  [45] "C<f4>te d'Ivoire"          "Denmark"                  
##  [47] "Djibouti"                  "Dominica"                 
##  [49] "Dominican Republic"        "Ecuador"                  
##  [51] "Egypt"                     "El Salvador"              
##  [53] "Equatorial Guinea"         "Eritrea"                  
##  [55] "Estonia"                   "Ethiopia"                 
##  [57] "Falkland Is.(Malvinas)"    "Faroe Islands"            
##  [59] "Fiji, Republic of"         "Finland"                  
##  [61] "France"                    "French Guiana"            
##  [63] "French Polynesia"          "French Southern Terr"     
##  [65] "Gabon"                     "Gambia"                   
##  [67] "Georgia"                   "Germany"                  
##  [69] "Ghana"                     "Gibraltar"                
##  [71] "Greece"                    "Greenland"                
##  [73] "Grenada"                   "Guadeloupe"               
##  [75] "Guam"                      "Guatemala"                
##  [77] "Guinea"                    "GuineaBissau"             
##  [79] "Guyana"                    "Haiti"                    
##  [81] "Honduras"                  "Iceland"                  
##  [83] "India"                     "Indonesia"                
##  [85] "Iran (Islamic Rep. of)"    "Iraq"                     
##  [87] "Ireland"                   "Isle of Man"              
##  [89] "Israel"                    "Italy"                    
##  [91] "Jamaica"                   "Japan"                    
##  [93] "Jordan"                    "Kenya"                    
##  [95] "Kiribati"                  "Korea, Dem. People's Rep" 
##  [97] "Korea, Republic of"        "Kuwait"                   
##  [99] "Latvia"                    "Lebanon"                  
## [101] "Liberia"                   "Libya"                    
## [103] "Lithuania"                 "Madagascar"               
## [105] "Malaysia"                  "Maldives"                 
## [107] "Malta"                     "Marshall Islands"         
## [109] "Martinique"                "Mauritania"               
## [111] "Mauritius"                 "Mayotte"                  
## [113] "Mexico"                    "Micronesia, Fed.States of"
## [115] "Monaco"                    "Montenegro"               
## [117] "Montserrat"                "Morocco"                  
## [119] "Mozambique"                "Myanmar"                  
## [121] "Namibia"                   "Nauru"                    
## [123] "Netherlands"               "Netherlands Antilles"     
## [125] "New Caledonia"             "New Zealand"              
## [127] "Nicaragua"                 "Nigeria"                  
## [129] "Niue"                      "Norfolk Island"           
## [131] "Northern Mariana Is."      "Norway"                   
## [133] "Oman"                      "Other nei"                
## [135] "Pakistan"                  "Palau"                    
## [137] "Palestine, Occupied Tr."   "Panama"                   
## [139] "Papua New Guinea"          "Peru"                     
## [141] "Philippines"               "Pitcairn Islands"         
## [143] "Poland"                    "Portugal"                 
## [145] "Puerto Rico"               "Qatar"                    
## [147] "Romania"                   "Russian Federation"       
## [149] "R<e9>union"                "Saint Barth<e9>lemy"      
## [151] "Saint Helena"              "Saint Kitts and Nevis"    
## [153] "Saint Lucia"               "Saint Vincent/Grenadines" 
## [155] "SaintMartin"               "Samoa"                    
## [157] "Sao Tome and Principe"     "Saudi Arabia"             
## [159] "Senegal"                   "Serbia and Montenegro"    
## [161] "Seychelles"                "Sierra Leone"             
## [163] "Singapore"                 "Sint Maarten"             
## [165] "Slovenia"                  "Solomon Islands"          
## [167] "Somalia"                   "South Africa"             
## [169] "Spain"                     "Sri Lanka"                
## [171] "St. Pierre and Miquelon"   "Sudan"                    
## [173] "Sudan (former)"            "Suriname"                 
## [175] "Svalbard and Jan Mayen"    "Sweden"                   
## [177] "Syrian Arab Republic"      "Taiwan Province of China" 
## [179] "Tanzania, United Rep. of"  "Thailand"                 
## [181] "TimorLeste"                "Togo"                     
## [183] "Tokelau"                   "Tonga"                    
## [185] "Trinidad and Tobago"       "Tunisia"                  
## [187] "Turkey"                    "Turks and Caicos Is."     
## [189] "Tuvalu"                    "US Virgin Islands"        
## [191] "Ukraine"                   "Un. Sov. Soc. Rep."       
## [193] "United Arab Emirates"      "United Kingdom"           
## [195] "United States of America"  "Uruguay"                  
## [197] "Vanuatu"                   "Venezuela, Boliv Rep of"  
## [199] "Viet Nam"                  "Wallis and Futuna Is."    
## [201] "Western Sahara"            "Yemen"                    
## [203] "Yugoslavia SFR"            "Zanzibar"
```


7. Use `rename()` to rename the columns and make them easier to use. The new column names should be:  
+ country
+ commname
+ ASFIS_sciname
+ ASFIS_spcode
+ ISSCAAP_spgroup
+ ISSCAAP_spgroupname
+ FAO_area
+ unit


```r
fisheries <- fisheries %>% 
  dplyr::rename(
    country = "Country",
    commname = "Common name", 
    ASFIS_spcode = "ASFIS species#",
    ASFIS_sciname = "ASFIS species name",  
    ISSCAAP_spgroup = "ISSCAAP group#",
    ISSCAAP_spgroupname = "ISSCAAP taxonomic group", 
    FAO_area = "FAO major fishing area", 
    unit = "Measure")
      
fisheries
```

```
## # A tibble: 17,692 x 71
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup~ ASFIS_spcode
##    <chr>   <chr>              <dbl> <chr>            <chr>       
##  1 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  2 Albania Atlanti~              36 Tunas, bonitos,~ 1750100101  
##  3 Albania Barracu~              37 Miscellaneous p~ 17710001XX  
##  4 Albania Blue an~              45 Shrimps, prawns  2280203101  
##  5 Albania Blue wh~              32 Cods, hakes, ha~ 1480403301  
##  6 Albania Bluefish              37 Miscellaneous p~ 1702021301  
##  7 Albania Bogue                 33 Miscellaneous c~ 1703926101  
##  8 Albania Caramot~              45 Shrimps, prawns  2280100117  
##  9 Albania Catshar~              38 Sharks, rays, c~ 10801003XX  
## 10 Albania Common ~              57 Squids, cuttlef~ 3210200202  
## # ... with 17,682 more rows, and 66 more variables: ASFIS_sciname <chr>,
## #   FAO_area <dbl>, unit <chr>, `1950` <dbl>, `1951` <dbl>, `1952` <dbl>,
## #   `1953` <dbl>, `1954` <dbl>, `1955` <dbl>, `1956` <dbl>, `1957` <dbl>,
## #   `1958` <dbl>, `1959` <dbl>, `1960` <dbl>, `1961` <dbl>, `1962` <dbl>,
## #   `1963` <dbl>, `1964` <dbl>, `1965` <dbl>, `1966` <dbl>, `1967` <dbl>,
## #   `1968` <dbl>, `1969` <dbl>, `1970` <dbl>, `1971` <dbl>, `1972` <dbl>,
## #   `1973` <dbl>, `1974` <dbl>, `1975` <dbl>, `1976` <dbl>, `1977` <dbl>,
## #   `1978` <dbl>, `1979` <dbl>, `1980` <dbl>, `1981` <dbl>, `1982` <dbl>,
## #   `1983` <dbl>, `1984` <dbl>, `1985` <dbl>, `1986` <dbl>, `1987` <dbl>,
## #   `1988` <dbl>, `1989` <dbl>, `1990` <dbl>, `1991` <dbl>, `1992` <dbl>,
## #   `1993` <dbl>, `1994` <dbl>, `1995` <dbl>, `1996` <dbl>, `1997` <dbl>,
## #   `1998` <dbl>, `1999` <dbl>, `2000` <dbl>, `2001` <dbl>, `2002` <dbl>,
## #   `2003` <dbl>, `2004` <dbl>, `2005` <dbl>, `2006` <dbl>, `2007` <dbl>,
## #   `2008` <dbl>, `2009` <dbl>, `2010` <dbl>, `2011` <dbl>, `2012` <dbl>
```

8. Are these data tidy? Why or why not, and, how do you know? Use the appropriate pivot function to tidy the data. Remove the NA's. Put the tidy data frame into a new object `fisheries_tidy`.  

Requirements for tidyness: 
(1) each variable has its own column  
(2) each observation has its own row  
(3) each value has its own cell  

The second condition is not met


```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(`1950`:`2012`,
               names_to = "year", 
               values_to = "catch",
               values_drop_na = TRUE
               )

fisheries_tidy
```

```
## # A tibble: 342,121 x 10
##    country commname ISSCAAP_spgroup ISSCAAP_spgroup~ ASFIS_spcode
##    <chr>   <chr>              <dbl> <chr>            <chr>       
##  1 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  2 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  3 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  4 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  5 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  6 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  7 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  8 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
##  9 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
## 10 Albania Angelsh~              38 Sharks, rays, c~ 10903XXXXX  
## # ... with 342,111 more rows, and 5 more variables: ASFIS_sciname <chr>,
## #   FAO_area <dbl>, unit <chr>, year <chr>, catch <dbl>
```

9. Refocus the data only to include country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, and catch.


```r
fisheries_tidy2 <- fisheries_tidy %>%
  select(country, ISSCAAP_spgroupname, ASFIS_spcode, ASFIS_sciname, year, catch)

fisheries_tidy2
```

```
## # A tibble: 342,121 x 6
##    country ISSCAAP_spgroupname     ASFIS_spcode ASFIS_sciname year  catch
##    <chr>   <chr>                   <chr>        <chr>         <chr> <dbl>
##  1 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1996     53
##  2 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1997     20
##  3 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1998     31
##  4 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   1999     30
##  5 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2000     30
##  6 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2001     16
##  7 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2002     79
##  8 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2003      1
##  9 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2004      4
## 10 Albania Sharks, rays, chimaeras 10903XXXXX   Squatinidae   2005     68
## # ... with 342,111 more rows
```

10. Re-check the classes of `fisheries_tidy2`. Notice that "catch" is shown as a character! This is a problem because we will want to treat it as a numeric. How will you deal with this? 


```r
sapply(fisheries_tidy2, class)
```

```
##             country ISSCAAP_spgroupname        ASFIS_spcode 
##         "character"         "character"         "character" 
##       ASFIS_sciname                year               catch 
##         "character"         "character"           "numeric"
```


```r
fisheries_tidy2$catch <- as.numeric(fisheries_tidy2$catch)
sapply(fisheries_tidy2, class)
```

```
##             country ISSCAAP_spgroupname        ASFIS_spcode 
##         "character"         "character"         "character" 
##       ASFIS_sciname                year               catch 
##         "character"         "character"           "numeric"
```

11. Based on the ASFIS_spcode, how many distinct taxa were caught as part of these data?


```r
length(unique(fisheries_tidy2$ASFIS_spcode))
```

```
## [1] 1530
```

```r
#1530 distinct taxa
```
 

12. Which country had the largest overall catch in the year 2000?


```r
catch_by_country <- fisheries_tidy %>%
  select(country, catch, year) %>%
  filter(year == 2000) %>%
  group_by(country) %>%
  summarize(catch_total = sum(catch, na.rm = T)) %>%
  arrange(desc(catch_total))

catch_by_country
```

```
## # A tibble: 173 x 2
##    country                  catch_total
##    <chr>                          <dbl>
##  1 Peru                        10625010
##  2 Japan                        4921013
##  3 United States of America     4692229
##  4 Chile                        4297928
##  5 Indonesia                    3761769
##  6 Russian Federation           3678828
##  7 Thailand                     2795719
##  8 India                        2760632
##  9 Norway                       2698506
## 10 Iceland                      1982369
## # ... with 163 more rows
```

```r
#Peru had the largest number of catches
```
 
13. Which country caught the most sardines (_Sardina_) between the years 1990-2000?


```r
fisheries_tidy2 %>%
  select(country, year, ASFIS_sciname, catch) %>%
  filter(str_detect(ASFIS_sciname, "Sardina")) %>%
  filter(year >= "1990" & year <= "2000") %>%
  group_by(country) %>%
  summarize(catch = sum(catch)) %>%
  arrange(desc(catch))
```

```
## # A tibble: 36 x 2
##    country              catch
##    <chr>                <dbl>
##  1 Morocco            4785190
##  2 Spain              1425317
##  3 Russian Federation 1035139
##  4 Portugal            926318
##  5 Ukraine             784730
##  6 Italy               377907
##  7 Algeria             311733
##  8 Turkey              273565
##  9 France              263871
## 10 Denmark             242017
## # ... with 26 more rows
```

```r
#Morocco caught the most sardines
```

14. Which five countries caught the most cephalopods between 2008-2012?


```r
#cephalopods include Squids, cuttlefishes, octopuses

fisheries_tidy2 %>%
  select(country, catch, year, ISSCAAP_spgroupname) %>%
  filter(year >= "2008" & year <= "2012") %>%
  filter(str_detect(ISSCAAP_spgroupname, "Squids, cuttlefishes, octopuses")) %>%
  group_by(country) %>%
  summarize(catch = sum(catch)) %>%
  arrange(desc(catch))
```

```
## # A tibble: 112 x 2
##    country                    catch
##    <chr>                      <dbl>
##  1 China                    4785139
##  2 Peru                     2274232
##  3 Korea, Republic of       1535454
##  4 Japan                    1394041
##  5 Chile                     723186
##  6 Indonesia                 684567
##  7 United States of America  613400
##  8 Thailand                  603529
##  9 Taiwan Province of China  593638
## 10 Argentina                 587238
## # ... with 102 more rows
```

```r
#Top 5 countries: China, Peru, Korea, Japan, Chile
```

15. Given the top five countries from question 12 above, which species was the highest catch total? The lowest?


```r
fisheries_tidy2 %>%
  filter(str_detect(ISSCAAP_spgroupname, "Squids, cuttlefishes, octopuses")) %>% 
  filter(year >= "2008" & year <= "2012") %>%
  group_by(ASFIS_sciname) %>%
  summarize(catch_total = sum(catch, na.rm = T)) %>%
  arrange((catch_total))
```

```
## # A tibble: 31 x 2
##    ASFIS_sciname           catch_total
##    <chr>                         <dbl>
##  1 Todarodes filippovae              1
##  2 Martialia hyadesi                 4
##  3 Moroteuthis ingens              194
##  4 Loligo vulgaris                 398
##  5 Eledone cirrhosa                920
##  6 Loligo duvauceli               1843
##  7 Loligo forbesi                 2567
##  8 Todarodes sagittatus           5073
##  9 Illex coindetii               20209
## 10 Sepioteuthis lessoniana       28547
## # ... with 21 more rows
```


16. In some cases, the taxonomy of the fish being caught is unclear. Make a new data frame called `coastal_fish` that shows the taxonomic composition of "Miscellaneous coastal fishes" within the ISSCAAP_spgroupname column.


```r
coastal_fish <- fisheries_tidy2 %>%
  filter(str_detect(ISSCAAP_spgroupname, "Miscellaneous coastal fishes"))
 
coastal_fish
```

```
## # A tibble: 63,236 x 6
##    country ISSCAAP_spgroupname       ASFIS_spcode ASFIS_sciname year  catch
##    <chr>   <chr>                     <chr>        <chr>         <chr> <dbl>
##  1 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1983    559
##  2 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1984    392
##  3 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1985    406
##  4 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1986    499
##  5 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1987    564
##  6 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1988    724
##  7 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1989    583
##  8 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1990    754
##  9 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1991    283
## 10 Albania Miscellaneous coastal fi~ 1703926101   Boops boops   1992    196
## # ... with 63,226 more rows
```



17. Use the data to do at least one exploratory analysis of your choice. What can you learn?


```r
#investigate which species are the most popular in catch number worldwide.
#Identify the species which is caught the most and look at its distribution per country


popular_fish <- fisheries_tidy2 %>%
 group_by(ASFIS_sciname) %>%
  summarize(catch_total = sum(catch, na.rm = T)) %>%
  filter(catch_total >= 50000000) %>%
  arrange(desc(catch_total))

popular_fish
```

```
## # A tibble: 12 x 2
##    ASFIS_sciname           catch_total
##    <chr>                         <dbl>
##  1 Osteichthyes              373807184
##  2 Engraulis ringens         324718139
##  3 Theragra chalcogramma     194730667
##  4 Clupea harengus           134992872
##  5 Gadus morhua              126371412
##  6 Scomber japonicus          90056951
##  7 Trachurus murphyi          82874285
##  8 Sardinops sagax            74703430
##  9 Sardinops melanostictus    74261311
## 10 Mallotus villosus          71823402
## 11 Katsuwonus pelamis         67519554
## 12 Sardina pilchardus         52979312
```


```r
#The osteichthyes, or bony fish, represent the largest taxonomic class of vertebrates in the modern world.

most_caught <- fisheries_tidy2 %>%
  filter(str_detect(ASFIS_sciname, "Osteichthyes")) %>%
  group_by(country) %>%
  summarize(catch = sum(catch)) %>%
  arrange(desc(catch))
 
most_caught
```

```
## # A tibble: 189 x 2
##    country               catch
##    <chr>                 <dbl>
##  1 China              81794211
##  2 Thailand           43130604
##  3 Myanmar            37368145
##  4 Viet Nam           33142032
##  5 Japan              26355662
##  6 Indonesia          18663279
##  7 India              16469387
##  8 Malaysia           13367312
##  9 Un. Sov. Soc. Rep.  8116661
## 10 Mexico              7694907
## # ... with 179 more rows
```

```r
#Visualize above data

#install.packages("rworldmap")
#library(rworldmap)
```


```r
# matched <- joinCountryData2Map(most_caught, joinCode="NAME", nameJoinColumn="country")
# 
# mapCountryData(matched, nameColumnToPlot="catch", mapTitle="Catch Country Sample", catMethod = "pretty", colourPalette = "heat")
```

