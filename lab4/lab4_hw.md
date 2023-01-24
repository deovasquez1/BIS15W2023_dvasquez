---
title: "Lab 4 Homework"
author: "Deon Vasquez"
date: "2023-01-24"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**


```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
homerange
```

```
## # A tibble: 569 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <chr>  <chr>   <chr> <chr> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 lake … americ… acti… angu… angui… angu… rostra… teleme… 16       887    2.95 
##  2 river… blackt… acti… cypr… catos… moxo… poecil… mark-r… <NA>     562    2.75 
##  3 river… centra… acti… cypr… cypri… camp… anomal… mark-r… 20        34    1.53 
##  4 river… rosysi… acti… cypr… cypri… clin… fundul… mark-r… 26         4    0.602
##  5 river… longno… acti… cypr… cypri… rhin… catara… mark-r… 17         4    0.602
##  6 river… muskel… acti… esoc… esoci… esox  masqui… teleme… 5       3525    3.55 
##  7 marin… pollack acti… gadi… gadid… poll… pollac… teleme… 2        737.   2.87 
##  8 marin… saithe  acti… gadi… gadid… poll… virens  teleme… 2        449.   2.65 
##  9 marin… lined … acti… perc… acant… acan… lineat… direct… <NA>     109.   2.04 
## 10 marin… orange… acti… perc… acant… naso  litura… teleme… 8        772.   2.89 
## # … with 559 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```


**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

Dimensions:

```r
dim(homerange)
```

```
## [1] 569  24
```
Column Names:

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
View class:

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", …
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3…
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car…
## $ dimension                  <dbl> 3, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3…
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N…
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, …
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20…
```
Statistical summary:

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  
For taxon:

```r
class(homerange$taxon)
```

```
## [1] "character"
```


```r
homerange$taxon <- as.factor(homerange$taxon)
```


```r
class(homerange$taxon)
```

```
## [1] "factor"
```

```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```
For order:

```r
class(homerange$order)
```

```
## [1] "character"
```


```r
homerange$order <- as.factor(homerange$order)
```


```r
class(homerange$order)
```

```
## [1] "factor"
```


```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tinamiformes"          "tetraodontiformes\xa0"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  


```r
taxa <- select(homerange, "taxon", "common.name", "class", "order", "family", "genus", "species")
taxa
```

```
## # A tibble: 569 × 7
##    taxon         common.name             class        order family genus species
##    <fct>         <chr>                   <chr>        <fct> <chr>  <chr> <chr>  
##  1 lake fishes   american eel            actinoptery… angu… angui… angu… rostra…
##  2 river fishes  blacktail redhorse      actinoptery… cypr… catos… moxo… poecil…
##  3 river fishes  central stoneroller     actinoptery… cypr… cypri… camp… anomal…
##  4 river fishes  rosyside dace           actinoptery… cypr… cypri… clin… fundul…
##  5 river fishes  longnose dace           actinoptery… cypr… cypri… rhin… catara…
##  6 river fishes  muskellunge             actinoptery… esoc… esoci… esox  masqui…
##  7 marine fishes pollack                 actinoptery… gadi… gadid… poll… pollac…
##  8 marine fishes saithe                  actinoptery… gadi… gadid… poll… virens 
##  9 marine fishes lined surgeonfish       actinoptery… perc… acant… acan… lineat…
## 10 marine fishes orangespine unicornfish actinoptery… perc… acant… naso  litura…
## # … with 559 more rows
```


**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  


```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```


**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  


```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```


**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

For carnivores:

```r
carnivores <- filter(homerange, trophic.guild == "carnivore")
carnivores
```

```
## # A tibble: 342 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <fct>  <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 lake … americ… acti… angu… angui… angu… rostra… teleme… 16       887    2.95 
##  2 river… blackt… acti… cypr… catos… moxo… poecil… mark-r… <NA>     562    2.75 
##  3 river… centra… acti… cypr… cypri… camp… anomal… mark-r… 20        34    1.53 
##  4 river… rosysi… acti… cypr… cypri… clin… fundul… mark-r… 26         4    0.602
##  5 river… longno… acti… cypr… cypri… rhin… catara… mark-r… 17         4    0.602
##  6 river… muskel… acti… esoc… esoci… esox  masqui… teleme… 5       3525    3.55 
##  7 marin… pollack acti… gadi… gadid… poll… pollac… teleme… 2        737.   2.87 
##  8 marin… saithe  acti… gadi… gadid… poll… virens  teleme… 2        449.   2.65 
##  9 marin… giant … acti… perc… caran… cara… ignobi… teleme… 4        726.   2.86 
## 10 lake … rock b… acti… perc… centr… ambl… rupest… mark-r… 16       196    2.29 
## # … with 332 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```

For Herbivores:

```r
herbivores <- filter(homerange, trophic.guild == "herbivore")
herbivores
```

```
## # A tibble: 227 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <fct>  <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 marin… lined … acti… perc… acant… acan… lineat… direct… <NA>   109.     2.04 
##  2 marin… orange… acti… perc… acant… naso  litura… teleme… 8      772.     2.89 
##  3 marin… bluesp… acti… perc… acant… naso  unicor… teleme… 7      152.     2.18 
##  4 marin… redlip… acti… perc… blenn… ophi… atlant… direct… 20       6.2    0.792
##  5 marin… bermud… acti… perc… kypho… kyph… sectat… teleme… 11    1087.     3.04 
##  6 marin… cherub… acti… perc… pomac… cent… argi    direct… <NA>     2.5    0.398
##  7 marin… damsel… acti… perc… pomac… chro… chromis direct… <NA>    28.4    1.45 
##  8 marin… twinsp… acti… perc… pomac… chry… biocel… direct… 18       9.19   0.963
##  9 marin… wards … acti… perc… pomac… poma… wardi   direct… <NA>    10.5    1.02 
## 10 marin… austra… acti… perc… pomac… steg… apical… direct… <NA>    45.3    1.66 
## # … with 217 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```


**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  
For herbivores:

```r
anyNA(herbivores$mean.hra.m2)
```

```
## [1] FALSE
```

```r
vect_herbivores <- herbivores$mean.hra.m2
vect_herbivores
```

```
##   [1] 1.113000e+01 3.209286e+04 1.790000e+04 5.200000e-01 3.442300e+04
##   [6] 1.130000e+00 1.850000e+01 2.580000e+00 5.400000e-01 2.250000e+00
##  [11] 5.000000e-02 7.400000e+00 7.830000e+03 1.720000e+02 2.444278e+04
##  [16] 2.870000e+02 1.650000e+02 1.750000e+02 7.200000e+01 4.948214e+04
##  [21] 4.591200e+07 2.589980e+03 2.540000e+06 6.358500e+07 1.030000e+05
##  [26] 1.815822e+07 1.699677e+04 2.589984e+04 6.200000e+04 1.975000e+06
##  [31] 5.500000e+06 1.203000e+07 4.300000e+04 1.323320e+05 3.090000e+04
##  [36] 1.618740e+04 2.589984e+04 3.140000e+06 9.500000e+04 1.950000e+05
##  [41] 2.450000e+06 2.388000e+07 8.430000e+07 2.428110e+04 1.012535e+07
##  [46] 3.224482e+06 2.176858e+06 9.050030e+06 2.657786e+08 1.014051e+07
##  [51] 6.452827e+07 7.000032e+05 4.161693e+05 3.570015e+05 1.872837e+06
##  [56] 2.733317e+04 2.328574e+07 5.882474e+06 2.754482e+07 6.199976e+05
##  [61] 3.408003e+06 5.239984e+07 3.710906e+04 1.070040e+09 9.382531e+07
##  [66] 3.647707e+06 6.746368e+05 7.486520e+07 8.514909e+05 9.850086e+05
##  [71] 1.620541e+05 3.507276e+07 2.488342e+06 7.900053e+06 1.976651e+05
##  [76] 3.550831e+09 1.365369e+08 5.899973e+06 1.742007e+06 1.097994e+07
##  [81] 2.486223e+06 1.459990e+07 1.919995e+05 1.024991e+06 4.487040e+03
##  [86] 2.792480e+05 4.135043e+06 1.930012e+04 6.413277e+05 9.149977e+05
##  [91] 3.236533e+06 6.133382e+06 9.709123e+05 1.630009e+05 7.739983e+06
##  [96] 1.190008e+05 4.566674e+05 3.732759e+05 1.545468e+04 4.250010e+05
## [101] 3.566646e+04 1.385639e+05 1.527601e+05 5.013488e+04 2.500000e+05
## [106] 1.079991e+05 4.858810e+03 3.271674e+04 2.900013e+06 1.592759e+06
## [111] 5.300050e+05 2.866157e+05 1.389985e+04 4.532418e+05 6.299992e+04
## [116] 1.829995e+04 2.892011e+04 3.960044e+04 1.376000e+03 1.866340e+03
## [121] 2.229513e+07 1.591256e+07 4.206588e+07 4.499974e+04 1.099993e+08
## [126] 1.753759e+09 1.037410e+03 2.685840e+03 1.299990e+04 1.582010e+03
## [131] 2.720000e+02 1.720000e+02 5.400950e+03 9.769897e+05 1.000000e+04
## [136] 1.596980e+03 7.738910e+03 8.322040e+03 7.004200e+02 8.550000e+01
## [141] 1.516000e+02 6.744700e+02 4.117400e+02 3.667000e+01 4.192000e+02
## [146] 9.821300e+02 4.761678e+04 2.537000e+03 5.330000e+02 5.805500e+02
## [151] 5.995010e+03 2.132900e+03 4.549990e+03 3.127810e+03 5.788150e+03
## [156] 1.038510e+03 1.866680e+05 3.615014e+05 7.114000e+01 1.093000e+05
## [161] 4.369990e+03 4.317000e+02 7.374800e+03 1.769987e+04 3.008500e+03
## [166] 1.480440e+03 1.689779e+06 1.411985e+06 1.511785e+05 7.574950e+03
## [171] 1.305209e+04 1.327000e+02 6.300000e+02 3.500016e+04 9.499920e+03
## [176] 5.000000e+03 4.030000e+01 1.932810e+03 1.799990e+03 7.900053e+04
## [181] 2.919577e+04 5.696394e+04 1.653903e+05 2.749983e+04 1.308881e+05
## [186] 4.900040e+03 1.708205e+05 1.282655e+05 7.490831e+04 5.188400e+02
## [191] 5.355000e+02 1.684380e+05 3.010925e+04 1.504181e+04 1.559983e+04
## [196] 4.250500e+04 8.163190e+03 1.490219e+04 5.325005e+04 3.246011e+04
## [201] 4.753350e+03 1.239995e+05 1.176068e+04 8.594300e+03 7.066000e+04
## [206] 1.280000e+05 3.477778e+04 2.350000e+03 5.656000e+03 5.850000e+02
## [211] 5.750000e+01 1.350000e+02 1.464800e+04 8.727000e+03 3.418000e+04
## [216] 1.384160e+06 1.685000e+05 5.200000e+03 7.200000e+04 1.900000e+04
## [221] 9.640000e+04 3.197000e+05 2.050000e+06 1.710000e+04 3.790000e+04
## [226] 5.700000e+05 1.417000e+05
```

```r
mean(vect_herbivores, na.rm=T)
```

```
## [1] 34137012
```
For Carnivores:

```r
anyNA(carnivores$mean.hra.m2)
```

```
## [1] FALSE
```

```r
vect_carnivores <- carnivores$mean.hra.m2
vect_carnivores
```

```
##   [1]    282750.00       282.10       116.11       125.50        87.10
##   [6]     39343.50      9056.41     44516.15     52773.00     10406.90
##  [11]      4950.00      4420.00        97.50      1936.50     34403.33
##  [16]    158000.00        63.24        59.50        64.91       220.93
##  [21]       274.94      2046.67         2.54        46.20      3303.11
##  [26]        28.27         0.50         0.03         0.32        61.50
##  [31]       517.80     50000.00       227.60       142.50       128.50
##  [36]       158.40       163.70        33.16      4028.59       856.00
##  [41]     15134.00      1368.11       103.30        11.87      1988.10
##  [46]   7640000.00      6660.00      1340.60     35384.00   4172000.00
##  [51]     35474.00     17712.35      5400.00     19200.00     11400.00
##  [56]        27.00         1.10      1300.00      2120.00        12.00
##  [61]       217.00      1243.40      5312.00   2087500.00     18305.00
##  [66]    299000.00         2.19         6.83   1435000.00      3760.25
##  [71]     10002.71    168000.00     18796.00    761666.67   1107500.00
##  [76]     29754.81       101.25       343.70       174.00        45.00
##  [81]     15288.40        83.90        47.00        48.13      2157.75
##  [86]       815.40      1571.00    250000.00     34692.40      6145.74
##  [91]        19.90        12.60       151.50  27550000.00  50240000.00
##  [96]  78500000.00  19620000.00 117300000.00  63570000.00    463900.00
## [101]    785000.00   2460000.00   1000000.00  12560000.00  12560000.00
## [106]  38460000.00    550000.00    499000.00   2254095.45  40000000.00
## [111]   7100000.00    995525.10   4249192.50    639402.30   2464531.65
## [116]   2521187.55 200980000.00  19625000.00 241000000.00    666000.00
## [121]  50000000.00  25778434.50 153860000.00   1416397.50   3000000.00
## [126]     90000.00     44000.00     30000.00     42000.00     82960.43
## [131]     60702.75     48562.20     47000.00     14400.00  28000000.00
## [136]     10926.50      1052.18     16996.77     30756.06     42000.00
## [141]     10000.00     30351.38     30351.38      1335.46     15782.72
## [146]     75676.10    635800.00     80000.00      4046.85    785000.00
## [151]     10117.13     10000.00     15378.03      4500.00      7300.00
## [156]     14568.66     14973.35     24281.10     22662.36      7689.02
## [161]      5260.91     14973.35     10117.13      5260.91     33993.54
## [166]      7284.33      6070.28      1699.68      1942.49      6474.96
## [171]     10117.13     35000.00     16500.00     19900.00     21000.00
## [176]      3237.48      3300.00      2800.00      4856.22      1214.06
## [181]      4046.85     10117.13     10117.13     44029.73      1780.61
## [186]     15782.72     83769.80     14973.35     11735.87      1335.46
## [191]      7284.33    193000.00     97000.00   3500000.00   1038100.00
## [196]   5306600.00    141500.00    350000.00   4521600.00   1850000.00
## [201]   3140000.00  19620000.00    500000.00  16000000.00   2124596.25
## [206]   1250000.00   4937157.00    356932.17   1500000.00       616.60
## [211]     46299.89  28499024.85   5393739.90   4928672.94   2000000.02
## [216]   8772835.78  30399749.15   5495408.74    891250.94 815060787.90
## [221] 376634414.00   1472448.11   2794988.34  67079528.30   6849360.11
## [226]  10949896.14   2390011.55  82748475.24 181042275.70   9499921.14
## [231]  39877690.65   7126724.98  82735138.83 504940260.80  53583367.03
## [236]   2406855.40 312003883.70  17353217.10   2219984.80    592570.46
## [241]    281838.29   3100000.00    387266.56   3799968.53  14617395.58
## [246]   4150018.19 361917847.30   7066103.59   4356522.89   9093477.57
## [251]  16755600.61   1323244.20    176750.24    899994.80    208929.61
## [256]   1000000.00    648858.50   4073802.78   3808816.06  10000000.00
## [261]   7809981.41     57500.29  11999965.57   2290867.65  11595000.00
## [266]     11410.11     35000.16       467.74       707.94    194236.12
## [271]     40377.55      3393.13     11999.97     29000.13       100.00
## [276]    116834.20     21133.43     25945.38      5011.87       234.42
## [281]      4786.30      5011.87       371.54       275.42        77.62
## [286]      3630.78      7428.65      3004.35      2828.59       700.00
## [291]       253.00    151000.00    114500.00      6476.00   1853000.00
## [296]    150600.00     46000.00    516375.00    110900.00    495000.00
## [301]    240400.00    429300.00     99000.00    131000.00     40000.00
## [306]     15400.00     17400.00    701000.00       600.00    374800.00
## [311]     77400.00     27379.00     38800.00     96000.00    171600.00
## [316]    119288.89     10655.00       200.00     60700.00     54200.00
## [321]     28000.00   2579600.00     34900.00   1178000.00     22900.00
## [326]    316000.00     34800.00      2613.69    245928.57      2400.00
## [331]    142000.00    115500.00     65300.00     31500.00     23800.00
## [336]     33000.00     35160.00     57500.00    186000.00      5180.00
## [341]     28000.00   1800000.00
```

```r
mean(vect_carnivores, na.rm=T)
```

```
## [1] 13039918
```
On average, herbivores have a larger 'mean.hra.m2' than carnivores. Herbivores have a value of 34,137,012 while carnivores have 13,039,918.


**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  


```r
not_just_deer <- select(homerange, "family","genus","species","mean.mass.g", "log10.mass")
not_just_deer
```

```
## # A tibble: 569 × 5
##    family       genus       species     mean.mass.g log10.mass
##    <chr>        <chr>       <chr>             <dbl>      <dbl>
##  1 anguillidae  anguilla    rostrata           887       2.95 
##  2 catostomidae moxostoma   poecilura          562       2.75 
##  3 cyprinidae   campostoma  anomalum            34       1.53 
##  4 cyprinidae   clinostomus funduloides          4       0.602
##  5 cyprinidae   rhinichthys cataractae           4       0.602
##  6 esocidae     esox        masquinongy       3525       3.55 
##  7 gadidae      pollachius  pollachius         737.      2.87 
##  8 gadidae      pollachius  virens             449.      2.65 
##  9 acanthuridae acanthurus  lineatus           109.      2.04 
## 10 acanthuridae naso        lituratus          772.      2.89 
## # … with 559 more rows
```


```r
deer <- filter(not_just_deer, family == "cervidae")
deer
```

```
## # A tibble: 12 × 5
##    family   genus      species     mean.mass.g log10.mass
##    <chr>    <chr>      <chr>             <dbl>      <dbl>
##  1 cervidae alces      alces           307227.       5.49
##  2 cervidae axis       axis             62823.       4.80
##  3 cervidae capreolus  capreolus        24050.       4.38
##  4 cervidae cervus     elaphus         234758.       5.37
##  5 cervidae cervus     nippon           29450.       4.47
##  6 cervidae dama       dama             71450.       4.85
##  7 cervidae muntiacus  reevesi          13500.       4.13
##  8 cervidae odocoileus hemionus         53864.       4.73
##  9 cervidae odocoileus virginianus      87884.       4.94
## 10 cervidae ozotoceros bezoarticus      35000.       4.54
## 11 cervidae pudu       puda              7500.       3.88
## 12 cervidae rangifer   tarandus        102059.       5.01
```


```r
arrange(deer, desc(log10.mass))
```

```
## # A tibble: 12 × 5
##    family   genus      species     mean.mass.g log10.mass
##    <chr>    <chr>      <chr>             <dbl>      <dbl>
##  1 cervidae alces      alces           307227.       5.49
##  2 cervidae cervus     elaphus         234758.       5.37
##  3 cervidae rangifer   tarandus        102059.       5.01
##  4 cervidae odocoileus virginianus      87884.       4.94
##  5 cervidae dama       dama             71450.       4.85
##  6 cervidae axis       axis             62823.       4.80
##  7 cervidae odocoileus hemionus         53864.       4.73
##  8 cervidae ozotoceros bezoarticus      35000.       4.54
##  9 cervidae cervus     nippon           29450.       4.47
## 10 cervidae capreolus  capreolus        24050.       4.38
## 11 cervidae muntiacus  reevesi          13500.       4.13
## 12 cervidae pudu       puda              7500.       3.88
```

The largest deer species is the Alces. It's common name is 'Moose.'

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    


```r
not_just_snakes <- select(homerange, "taxon","family","genus","species","mean.hra.m2", "log10.hra")
not_just_snakes
```

```
## # A tibble: 569 × 6
##    taxon         family       genus       species     mean.hra.m2 log10.hra
##    <fct>         <chr>        <chr>       <chr>             <dbl>     <dbl>
##  1 lake fishes   anguillidae  anguilla    rostrata       282750        5.45
##  2 river fishes  catostomidae moxostoma   poecilura         282.       2.45
##  3 river fishes  cyprinidae   campostoma  anomalum          116.       2.06
##  4 river fishes  cyprinidae   clinostomus funduloides       126.       2.10
##  5 river fishes  cyprinidae   rhinichthys cataractae         87.1      1.94
##  6 river fishes  esocidae     esox        masquinongy     39344.       4.59
##  7 marine fishes gadidae      pollachius  pollachius       9056.       3.96
##  8 marine fishes gadidae      pollachius  virens          44516.       4.65
##  9 marine fishes acanthuridae acanthurus  lineatus           11.1      1.05
## 10 marine fishes acanthuridae naso        lituratus       32093.       4.51
## # … with 559 more rows
```

```r
snakes <- filter(not_just_snakes, taxon == "snakes")
snakes
```

```
## # A tibble: 41 × 6
##    taxon  family     genus      species                  mean.hra.m2 log10.hra
##    <fct>  <chr>      <chr>      <chr>                          <dbl>     <dbl>
##  1 snakes colubridae carphopis  vermis                           700      2.85
##  2 snakes colubridae carphopis  viridis                          253      2.40
##  3 snakes colubridae coluber    constrictor                   151000      5.18
##  4 snakes colubridae coluber    constrictor flaviventris      114500      5.06
##  5 snakes colubridae diadophis  punctatus                       6476      3.81
##  6 snakes colubridae drymarchon couperi                      1853000      6.27
##  7 snakes colubridae elaphe     guttata emoryi                150600      5.18
##  8 snakes colubridae elaphe     obsoleta                       46000      4.66
##  9 snakes colubridae heterodon  platirhinos                   516375      5.71
## 10 snakes colubridae hierophis  viridiflavus                  110900      5.04
## # … with 31 more rows
```


```r
arrange(snakes, -desc(mean.hra.m2))
```

```
## # A tibble: 41 × 6
##    taxon  family     genus       species      mean.hra.m2 log10.hra
##    <fct>  <chr>      <chr>       <chr>              <dbl>     <dbl>
##  1 snakes viperidae  bitis       schneideri          200       2.30
##  2 snakes colubridae carphopis   viridis             253       2.40
##  3 snakes colubridae thamnophis  butleri             600       2.78
##  4 snakes colubridae carphopis   vermis              700       2.85
##  5 snakes viperidae  vipera      latastei           2400       3.38
##  6 snakes viperidae  gloydius    shedaoensis        2614.      3.42
##  7 snakes colubridae diadophis   punctatus          6476       3.81
##  8 snakes viperidae  agkistrodon piscivorous       10655       4.03
##  9 snakes colubridae oocatochus  rufodorsatus      15400       4.19
## 10 snakes colubridae pituophis   catenifer         17400       4.24
## # … with 31 more rows
```
The Bitis Scheneideri has the smallest homerange out of all the snakes. It's in the 'viperidae' family. On Wikipedia, the species habitat are the coastal sand dunes in Namibia. The snake is venomous, with a report that the venom causes pain, swelling, discoloration, and oozing. But the person who was bit recovered after 2 weeks. Good for them! lol!

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
