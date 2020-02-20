---
title: "Homework3"
output: 
  html_document: 
    keep_md: yes
---




```r
library(tidyverse)
```


```r
homerange <- readr::read_csv("lab3/data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double()
## )
```

```
## See spec(...) for full column specifications.
```


```r
spec(homerange)
```

```
## cols(
##   taxon = col_character(),
##   common.name = col_character(),
##   class = col_character(),
##   order = col_character(),
##   family = col_character(),
##   genus = col_character(),
##   species = col_character(),
##   primarymethod = col_character(),
##   N = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   alternative.mass.reference = col_character(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   hra.reference = col_character(),
##   realm = col_character(),
##   thermoregulation = col_character(),
##   locomotion = col_character(),
##   trophic.guild = col_character(),
##   dimension = col_character(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double(),
##   prey.size.reference = col_character()
## )
```

```r
#Allows us to see the full details of the columns
```


3. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.

```r
dim(homerange)
```

```
## [1] 569  24
```


```r
colnames(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
str(homerange)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	569 obs. of  24 variables:
##  $ taxon                     : chr  "lake fishes" "river fishes" "river fishes" "river fishes" ...
##  $ common.name               : chr  "american eel" "blacktail redhorse" "central stoneroller" "rosyside dace" ...
##  $ class                     : chr  "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii" ...
##  $ order                     : chr  "anguilliformes" "cypriniformes" "cypriniformes" "cypriniformes" ...
##  $ family                    : chr  "anguillidae" "catostomidae" "cyprinidae" "cyprinidae" ...
##  $ genus                     : chr  "anguilla" "moxostoma" "campostoma" "clinostomus" ...
##  $ species                   : chr  "rostrata" "poecilura" "anomalum" "funduloides" ...
##  $ primarymethod             : chr  "telemetry" "mark-recapture" "mark-recapture" "mark-recapture" ...
##  $ N                         : chr  "16" NA "20" "26" ...
##  $ mean.mass.g               : num  887 562 34 4 4 ...
##  $ log10.mass                : num  2.948 2.75 1.531 0.602 0.602 ...
##  $ alternative.mass.reference: chr  NA NA NA NA ...
##  $ mean.hra.m2               : num  282750 282.1 116.1 125.5 87.1 ...
##  $ log10.hra                 : num  5.45 2.45 2.06 2.1 1.94 ...
##  $ hra.reference             : chr  "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aqu"| __truncated__ ...
##  $ realm                     : chr  "aquatic" "aquatic" "aquatic" "aquatic" ...
##  $ thermoregulation          : chr  "ectotherm" "ectotherm" "ectotherm" "ectotherm" ...
##  $ locomotion                : chr  "swimming" "swimming" "swimming" "swimming" ...
##  $ trophic.guild             : chr  "carnivore" "carnivore" "carnivore" "carnivore" ...
##  $ dimension                 : chr  "3D" "2D" "2D" "2D" ...
##  $ preymass                  : num  NA NA NA NA NA NA 1.39 NA NA NA ...
##  $ log10.preymass            : num  NA NA NA NA NA ...
##  $ PPMR                      : num  NA NA NA NA NA NA 530 NA NA NA ...
##  $ prey.size.reference       : chr  NA NA NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   taxon = col_character(),
##   ..   common.name = col_character(),
##   ..   class = col_character(),
##   ..   order = col_character(),
##   ..   family = col_character(),
##   ..   genus = col_character(),
##   ..   species = col_character(),
##   ..   primarymethod = col_character(),
##   ..   N = col_character(),
##   ..   mean.mass.g = col_double(),
##   ..   log10.mass = col_double(),
##   ..   alternative.mass.reference = col_character(),
##   ..   mean.hra.m2 = col_double(),
##   ..   log10.hra = col_double(),
##   ..   hra.reference = col_character(),
##   ..   realm = col_character(),
##   ..   thermoregulation = col_character(),
##   ..   locomotion = col_character(),
##   ..   trophic.guild = col_character(),
##   ..   dimension = col_character(),
##   ..   preymass = col_double(),
##   ..   log10.preymass = col_double(),
##   ..   PPMR = col_double(),
##   ..   prey.size.reference = col_character()
##   .. )
```


```r
summary(homerange)
```

```
##     taxon           common.name           class          
##  Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##     order              family             genus          
##  Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##    species          primarymethod           N            
##  Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##   mean.mass.g        log10.mass      alternative.mass.reference
##  Min.   :      0   Min.   :-0.6576   Length:569                
##  1st Qu.:     50   1st Qu.: 1.6990   Class :character          
##  Median :    330   Median : 2.5185   Mode  :character          
##  Mean   :  34602   Mean   : 2.5947                             
##  3rd Qu.:   2150   3rd Qu.: 3.3324                             
##  Max.   :4000000   Max.   : 6.6021                             
##                                                                
##   mean.hra.m2          log10.hra      hra.reference     
##  Min.   :0.000e+00   Min.   :-1.523   Length:569        
##  1st Qu.:4.500e+03   1st Qu.: 3.653   Class :character  
##  Median :3.934e+04   Median : 4.595   Mode  :character  
##  Mean   :2.146e+07   Mean   : 4.709                     
##  3rd Qu.:1.038e+06   3rd Qu.: 6.016                     
##  Max.   :3.551e+09   Max.   : 9.550                     
##                                                         
##     realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character  
##                                                          
##                                                          
##                                                          
##                                                          
##  trophic.guild       dimension            preymass        
##  Length:569         Length:569         Min.   :     0.67  
##  Class :character   Class :character   1st Qu.:    20.02  
##  Mode  :character   Mode  :character   Median :    53.75  
##                                        Mean   :  3989.88  
##                                        3rd Qu.:   363.35  
##                                        Max.   :130233.20  
##                                        NA's   :502        
##  log10.preymass         PPMR         prey.size.reference
##  Min.   :-0.1739   Min.   :  0.380   Length:569         
##  1st Qu.: 1.3014   1st Qu.:  3.315   Class :character   
##  Median : 1.7304   Median :  7.190   Mode  :character   
##  Mean   : 2.0188   Mean   : 31.752                      
##  3rd Qu.: 2.5603   3rd Qu.: 15.966                      
##  Max.   : 5.1147   Max.   :530.000                      
##  NA's   :502       NA's   :502
```

4. Are there NA's in your data? Show the code that you would use to verify this, please.  

```r
sum(is.na(homerange)) 
```

```
## [1] 2945
```

```r
#This output tells us that there are 2945 NA's in this dataset
```

5. Change the class of the variables `taxon` and `order` to factors and display their levels.

```r
homerange$taxon <- as.factor(homerange$taxon)
homerange$order <- as.factor(homerange$order)

levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"    "afrosoricida"       "anguilliformes"    
##  [4] "anseriformes"       "apterygiformes"     "artiodactyla"      
##  [7] "caprimulgiformes"   "carnivora"          "charadriiformes"   
## [10] "columbidormes"      "columbiformes"      "coraciiformes"     
## [13] "cuculiformes"       "cypriniformes"      "dasyuromorpha"     
## [16] "dasyuromorpia"      "didelphimorphia"    "diprodontia"       
## [19] "diprotodontia"      "erinaceomorpha"     "esociformes"       
## [22] "falconiformes"      "gadiformes"         "galliformes"       
## [25] "gruiformes"         "lagomorpha"         "macroscelidea"     
## [28] "monotrematae"       "passeriformes"      "pelecaniformes"    
## [31] "peramelemorphia"    "perciformes"        "perissodactyla"    
## [34] "piciformes"         "pilosa"             "proboscidea"       
## [37] "psittaciformes"     "rheiformes"         "roden"             
## [40] "rodentia"           "salmoniformes"      "scorpaeniformes"   
## [43] "siluriformes"       "soricomorpha"       "squamata"          
## [46] "strigiformes"       "struthioniformes"   "syngnathiformes"   
## [49] "testudines"         "tetraodontiformes<U+00A0>" "tinamiformes"
```

6. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer?  


```r
deer <- homerange %>%
  select(mean.mass.g, log10.mass, family, genus, species) %>%
  filter(family == "cervidae") %>%
  arrange(desc(log10.mass))

deer
```

```
## # A tibble: 12 x 5
##    mean.mass.g log10.mass family   genus      species    
##          <dbl>      <dbl> <chr>    <chr>      <chr>      
##  1     307227.       5.49 cervidae alces      alces      
##  2     234758.       5.37 cervidae cervus     elaphus    
##  3     102059.       5.01 cervidae rangifer   tarandus   
##  4      87884.       4.94 cervidae odocoileus virginianus
##  5      71450.       4.85 cervidae dama       dama       
##  6      62823.       4.80 cervidae axis       axis       
##  7      53864.       4.73 cervidae odocoileus hemionus   
##  8      35000.       4.54 cervidae ozotoceros bezoarticus
##  9      29450.       4.47 cervidae cervus     nippon     
## 10      24050.       4.38 cervidae capreolus  capreolus  
## 11      13500.       4.13 cervidae muntiacus  reevesi    
## 12       7500.       3.88 cervidae pudu       puda
```

```r
#From this chunk of code, The largest deer is the species alces
```

7. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it! 


```r
snake <- homerange %>%
  select(mean.hra.m2, taxon, order, family, genus, species) %>%
  filter(taxon == "snakes") %>%
  arrange(mean.hra.m2)

snake
```

```
## # A tibble: 41 x 6
##    mean.hra.m2 taxon  order    family     genus       species     
##          <dbl> <fct>  <fct>    <chr>      <chr>       <chr>       
##  1        200  snakes squamata viperidae  bitis       schneideri  
##  2        253  snakes squamata colubridae carphopis   viridis     
##  3        600  snakes squamata colubridae thamnophis  butleri     
##  4        700  snakes squamata colubridae carphopis   vermis      
##  5       2400  snakes squamata viperidae  vipera      latastei    
##  6       2614. snakes squamata viperidae  gloydius    shedaoensis 
##  7       6476  snakes squamata colubridae diadophis   punctatus   
##  8      10655  snakes squamata viperidae  agkistrodon piscivorous 
##  9      15400  snakes squamata colubridae oocatochus  rufodorsatus
## 10      17400  snakes squamata colubridae pituophis   catenifer   
## # ... with 31 more rows
```

```r
#From this coke chunk schneideri has the smallest homerange and is known as the world's smallest viper located in Namibia and South Africa
```


8. You suspect that homerange and mass are correlated in birds. We need a ratio that facilitates exploration of this prediction. First, build a new dataframe called `hra_ratio` that is limited to genus, species, mean.mass.g, log10.mass, log10.hra. Arrange it in ascending order by mean mass in grams.


```r
hra_ratio <- homerange %>%
  filter(taxon == "birds") %>%
  select(genus, species, mean.mass.g, log10.mass, log10.hra) %>%
  arrange(mean.mass.g)

hra_ratio
```

```
## # A tibble: 140 x 5
##    genus        species      mean.mass.g log10.mass log10.hra
##    <chr>        <chr>              <dbl>      <dbl>     <dbl>
##  1 regulus      regulus             5.15      0.712      4.30
##  2 regulus      ignicapillus        5.3       0.724      4.22
##  3 phylloscopus bonelli             7.5       0.875      4.54
##  4 aegithalos   caudatus            8         0.903      4.62
##  5 vireo        atricapillus        8.5       0.929      4.18
##  6 setophaga    magnolia            8.6       0.934      3.86
##  7 certhia      familiaris          8.77      0.943      4.67
##  8 sylvia       undata              8.8       0.944      3.45
##  9 setophaga    ruticilla           9         0.954      3.29
## 10 setophaga    virens              9         0.954      3.81
## # ... with 130 more rows
```

9. Replace the existing `hra_ratio` dataframe with a new dataframe that adds a column calculating the ratio of log 10 hra to log 10 mass. Call it `hra.mass.ratio`. Arrange it in descending order by mean mass in grams.


```r
  hra_ratio <- hra_ratio %>%
  mutate(hra.mass.ratio = log10.hra/log10.mass) %>%
  select(genus, species, mean.mass.g, log10.mass, log10.hra,hra.mass.ratio) %>%
  arrange(desc(mean.mass.g))

hra_ratio
```

```
## # A tibble: 140 x 6
##    genus      species      mean.mass.g log10.mass log10.hra hra.mass.ratio
##    <chr>      <chr>              <dbl>      <dbl>     <dbl>          <dbl>
##  1 struthio   camelus            88250       4.95      7.93           1.60
##  2 rhea       americana          25000       4.40      6.39           1.45
##  3 rhea       pennata            15000       4.18      7.38           1.77
##  4 aquila     chrysaetos          3000       3.48      7.44           2.14
##  5 tetrao     urogallus           2936       3.47      6.74           1.94
##  6 apteryx    australis           2320       3.37      5.67           1.68
##  7 neophron   percnopterus        2203       3.34      7.80           2.33
##  8 bubo       bubo                2191       3.34      7.20           2.16
##  9 hieraaetus fasciatus           2049       3.31      7.29           2.20
## 10 strigops   habroptilus         1941       3.29      5.29           1.61
## # ... with 130 more rows
```

10. What is the lowest mass for birds with a `hra.mass.ratio` greater than or equal to 4.0?

```r
hra_ratio %>%
  filter(hra.mass.ratio >= 4) %>%
  arrange(mean.mass.g)
```

```
## # A tibble: 17 x 6
##    genus        species     mean.mass.g log10.mass log10.hra hra.mass.ratio
##    <chr>        <chr>             <dbl>      <dbl>     <dbl>          <dbl>
##  1 regulus      regulus            5.15      0.712      4.30           6.04
##  2 regulus      ignicapill~        5.3       0.724      4.22           5.82
##  3 phylloscopus bonelli            7.5       0.875      4.54           5.19
##  4 aegithalos   caudatus           8         0.903      4.62           5.12
##  5 vireo        atricapill~        8.5       0.929      4.18           4.49
##  6 setophaga    magnolia           8.6       0.934      3.86           4.13
##  7 certhia      familiaris         8.77      0.943      4.67           4.95
##  8 wilsonia     canadensis         9.3       0.968      4.01           4.14
##  9 troglodytes  troglodytes        9.5       0.978      4.01           4.10
## 10 cisticola    juncidis           9.8       0.991      4.16           4.20
## 11 vireo        belli             10         1          4.07           4.07
## 12 parus        carolinens~       10.1       1.00       4.18           4.16
## 13 hippolais    polyglotta        11         1.04       4.48           4.30
## 14 parus        palustris         11         1.04       4.36           4.18
## 15 spizella     passerina         12.2       1.09       4.49           4.13
## 16 contopus     virens            13.8       1.14       4.64           4.07
## 17 motacilla    alba              21.2       1.33       5.89           4.44
```

```r
#From the results above, the lowest mass for birds with a`hra.mass.ratio` greater than or equal to 4.0 is 5.15 g
```


11. Do a search online; what is the common name of the bird from #8 above? Place a link in your markdown file that takes us to a webpage with information on its biology.  

Bird species Regulus: Common name is Kinglet

-->[Wikipedia Page of Kinglet](https://en.wikipedia.org/wiki/Kinglet)

12. What is the `hra.mass.ratio` for an ostrich? Show your work, please. 


```r
  ostrich_hra_ratio <- homerange %>%
  filter(taxon == "birds") %>%
  filter(common.name == "ostrich") %>%
  mutate(hra.mass.ratio = log10.hra/log10.mass) %>%
  select(common.name,hra.mass.ratio) 

ostrich_hra_ratio
```

```
## # A tibble: 1 x 2
##   common.name hra.mass.ratio
##   <chr>                <dbl>
## 1 ostrich               1.60
```

```r
#Results from above show that hra.mass.ratio for ostrich is 1.602565	
```

