---
title: "Lab 4 Homework"
author: "Yoko Takashima"
date: "2021-01-24"
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

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

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
##  trophic.guild       dimension            preymass         log10.preymass   
##  Length:569         Length:569         Min.   :     0.67   Min.   :-0.1739  
##  Class :character   Class :character   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Mode  :character   Median :    53.75   Median : 1.7304  
##                                        Mean   :  3989.88   Mean   : 2.0188  
##                                        3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                                        Max.   :130233.20   Max.   : 5.1147  
##                                        NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```



```r
glimpse(homerange)
```

```
## Observations: 569
## Variables: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fish…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cen…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actin…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprin…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cl…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fund…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recap…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2",…
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, …
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home rang…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic"…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ec…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimm…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "ca…
## $ dimension                  <chr> "3D", "2D", "2D", "2D", "2D", "2D", "2D", …
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, …
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA,…
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, N…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 2…
```


**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
homerange$taxon<-as.factor(homerange$taxon)
homerange$taxon
```

```
##   [1] lake fishes   river fishes  river fishes  river fishes  river fishes 
##   [6] river fishes  marine fishes marine fishes marine fishes marine fishes
##  [11] marine fishes marine fishes marine fishes lake fishes   lake fishes  
##  [16] lake fishes   river fishes  river fishes  lake fishes   lake fishes  
##  [21] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [26] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [31] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [36] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [41] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [46] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [51] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [56] marine fishes marine fishes marine fishes marine fishes lake fishes  
##  [61] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [66] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [71] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [76] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [81] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [86] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [91] marine fishes marine fishes marine fishes marine fishes marine fishes
##  [96] marine fishes river fishes  river fishes  river fishes  river fishes 
## [101] lake fishes   river fishes  river fishes  river fishes  marine fishes
## [106] marine fishes marine fishes marine fishes marine fishes lake fishes  
## [111] marine fishes marine fishes marine fishes birds         birds        
## [116] birds         birds         birds         birds         birds        
## [121] birds         birds         birds         birds         birds        
## [126] birds         birds         birds         birds         birds        
## [131] birds         birds         birds         birds         birds        
## [136] birds         birds         birds         birds         birds        
## [141] birds         birds         birds         birds         birds        
## [146] birds         birds         birds         birds         birds        
## [151] birds         birds         birds         birds         birds        
## [156] birds         birds         birds         birds         birds        
## [161] birds         birds         birds         birds         birds        
## [166] birds         birds         birds         birds         birds        
## [171] birds         birds         birds         birds         birds        
## [176] birds         birds         birds         birds         birds        
## [181] birds         birds         birds         birds         birds        
## [186] birds         birds         birds         birds         birds        
## [191] birds         birds         birds         birds         birds        
## [196] birds         birds         birds         birds         birds        
## [201] birds         birds         birds         birds         birds        
## [206] birds         birds         birds         birds         birds        
## [211] birds         birds         birds         birds         birds        
## [216] birds         birds         birds         birds         birds        
## [221] birds         birds         birds         birds         birds        
## [226] birds         birds         birds         birds         birds        
## [231] birds         birds         birds         birds         birds        
## [236] birds         birds         birds         birds         birds        
## [241] birds         birds         birds         birds         birds        
## [246] birds         birds         birds         birds         birds        
## [251] birds         birds         birds         mammals       mammals      
## [256] mammals       mammals       mammals       mammals       mammals      
## [261] mammals       mammals       mammals       mammals       mammals      
## [266] mammals       mammals       mammals       mammals       mammals      
## [271] mammals       mammals       mammals       mammals       mammals      
## [276] mammals       mammals       mammals       mammals       mammals      
## [281] mammals       mammals       mammals       mammals       mammals      
## [286] mammals       mammals       mammals       mammals       mammals      
## [291] mammals       mammals       mammals       mammals       mammals      
## [296] mammals       mammals       mammals       mammals       mammals      
## [301] mammals       mammals       mammals       mammals       mammals      
## [306] mammals       mammals       mammals       mammals       mammals      
## [311] mammals       mammals       mammals       mammals       mammals      
## [316] mammals       mammals       mammals       mammals       mammals      
## [321] mammals       mammals       mammals       mammals       mammals      
## [326] mammals       mammals       mammals       mammals       mammals      
## [331] mammals       mammals       mammals       mammals       mammals      
## [336] mammals       mammals       mammals       mammals       mammals      
## [341] mammals       mammals       mammals       mammals       mammals      
## [346] mammals       mammals       mammals       mammals       mammals      
## [351] mammals       mammals       mammals       mammals       mammals      
## [356] mammals       mammals       mammals       mammals       mammals      
## [361] mammals       mammals       mammals       mammals       mammals      
## [366] mammals       mammals       mammals       mammals       mammals      
## [371] mammals       mammals       mammals       mammals       mammals      
## [376] mammals       mammals       mammals       mammals       mammals      
## [381] mammals       mammals       mammals       mammals       mammals      
## [386] mammals       mammals       mammals       mammals       mammals      
## [391] mammals       mammals       mammals       mammals       mammals      
## [396] mammals       mammals       mammals       mammals       mammals      
## [401] mammals       mammals       mammals       mammals       mammals      
## [406] mammals       mammals       mammals       mammals       mammals      
## [411] mammals       mammals       mammals       mammals       mammals      
## [416] mammals       mammals       mammals       mammals       mammals      
## [421] mammals       mammals       mammals       mammals       mammals      
## [426] mammals       mammals       mammals       mammals       mammals      
## [431] mammals       mammals       mammals       mammals       mammals      
## [436] mammals       mammals       mammals       mammals       mammals      
## [441] mammals       mammals       mammals       mammals       mammals      
## [446] mammals       mammals       mammals       mammals       mammals      
## [451] mammals       mammals       mammals       mammals       mammals      
## [456] mammals       mammals       mammals       mammals       mammals      
## [461] mammals       mammals       mammals       mammals       mammals      
## [466] mammals       mammals       mammals       mammals       mammals      
## [471] mammals       mammals       mammals       mammals       mammals      
## [476] mammals       mammals       mammals       mammals       mammals      
## [481] mammals       mammals       mammals       mammals       mammals      
## [486] mammals       mammals       mammals       mammals       mammals      
## [491] mammals       lizards       snakes        snakes        snakes       
## [496] snakes        snakes        snakes        snakes        snakes       
## [501] snakes        snakes        snakes        snakes        snakes       
## [506] snakes        snakes        snakes        snakes        snakes       
## [511] snakes        snakes        snakes        snakes        snakes       
## [516] snakes        snakes        lizards       lizards       lizards      
## [521] lizards       lizards       lizards       lizards       lizards      
## [526] lizards       snakes        lizards       snakes        snakes       
## [531] snakes        snakes        snakes        snakes        snakes       
## [536] snakes        snakes        snakes        snakes        snakes       
## [541] snakes        snakes        snakes        turtles       turtles      
## [546] turtles       turtles       turtles       turtles       turtles      
## [551] turtles       turtles       turtles       turtles       turtles      
## [556] turtles       tortoises     tortoises     tortoises     tortoises    
## [561] tortoises     tortoises     tortoises     tortoises     tortoises    
## [566] tortoises     tortoises     tortoises     turtles      
## 9 Levels: birds lake fishes lizards mammals marine fishes ... turtles
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



```r
homerange$order <- as.factor(homerange$order)
class(homerange$order)
```

```
## [1] "factor"
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
## [49] "testudines"         "tetraodontiformes\xa0" "tinamiformes"
```


**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
taxa<- select(homerange,"taxon",common_name="common.name","class","order","family","genus","species")
taxa
```

```
## # A tibble: 569 x 7
##    taxon     common_name       class      order     family    genus    species  
##    <fct>     <chr>             <chr>      <fct>     <chr>     <chr>    <chr>    
##  1 lake fis… american eel      actinopte… anguilli… anguilli… anguilla rostrata 
##  2 river fi… blacktail redhor… actinopte… cyprinif… catostom… moxosto… poecilura
##  3 river fi… central stonerol… actinopte… cyprinif… cyprinid… campost… anomalum 
##  4 river fi… rosyside dace     actinopte… cyprinif… cyprinid… clinost… funduloi…
##  5 river fi… longnose dace     actinopte… cyprinif… cyprinid… rhinich… cataract…
##  6 river fi… muskellunge       actinopte… esocifor… esocidae  esox     masquino…
##  7 marine f… pollack           actinopte… gadiform… gadidae   pollach… pollachi…
##  8 marine f… saithe            actinopte… gadiform… gadidae   pollach… virens   
##  9 marine f… lined surgeonfish actinopte… percifor… acanthur… acanthu… lineatus 
## 10 marine f… orangespine unic… actinopte… percifor… acanthur… naso     lituratus
## # … with 559 more rows
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
taxon_table<-table(homerange$taxon)
taxon_table
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
trophic_guilds<-table(homerange$trophic.guild)
trophic_guilds
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
herbivore<- filter(homerange,trophic.guild== "herbivore")
herbivore
```

```
## # A tibble: 227 x 24
##    taxon common.name class order family genus species primarymethod N    
##    <fct> <chr>       <chr> <fct> <chr>  <chr> <chr>   <chr>         <chr>
##  1 mari… lined surg… acti… perc… acant… acan… lineat… direct obser… <NA> 
##  2 mari… orangespin… acti… perc… acant… naso  litura… telemetry     8    
##  3 mari… bluespine … acti… perc… acant… naso  unicor… telemetry     7    
##  4 mari… redlip ble… acti… perc… blenn… ophi… atlant… direct obser… 20   
##  5 mari… bermuda ch… acti… perc… kypho… kyph… sectat… telemetry     11   
##  6 mari… cherubfish  acti… perc… pomac… cent… argi    direct obser… <NA> 
##  7 mari… damselfish  acti… perc… pomac… chro… chromis direct obser… <NA> 
##  8 mari… twinspot d… acti… perc… pomac… chry… biocel… direct obser… 18   
##  9 mari… wards dams… acti… perc… pomac… poma… wardi   direct obser… <NA> 
## 10 mari… australian… acti… perc… pomac… steg… apical… direct obser… <NA> 
## # … with 217 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```


```r
carnivores <- filter(homerange, trophic.guild=="carnivore")
carnivores
```

```
## # A tibble: 342 x 24
##    taxon common.name class order family genus species primarymethod N    
##    <fct> <chr>       <chr> <fct> <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake… american e… acti… angu… angui… angu… rostra… telemetry     16   
##  2 rive… blacktail … acti… cypr… catos… moxo… poecil… mark-recaptu… <NA> 
##  3 rive… central st… acti… cypr… cypri… camp… anomal… mark-recaptu… 20   
##  4 rive… rosyside d… acti… cypr… cypri… clin… fundul… mark-recaptu… 26   
##  5 rive… longnose d… acti… cypr… cypri… rhin… catara… mark-recaptu… 17   
##  6 rive… muskellunge acti… esoc… esoci… esox  masqui… telemetry     5    
##  7 mari… pollack     acti… gadi… gadid… poll… pollac… telemetry     2    
##  8 mari… saithe      acti… gadi… gadid… poll… virens  telemetry     2    
##  9 mari… giant trev… acti… perc… caran… cara… ignobi… telemetry     4    
## 10 lake… rock bass   acti… perc… centr… ambl… rupest… mark-recaptu… 16   
## # … with 332 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
anyNA(herbivore)
```

```
## [1] TRUE
```



```r
herbi_mean <- herbivore$mean.hra.m2
mean(herbi_mean, na.rm = T)
```

```
## [1] 34137012
```


```r
anyNA(carnivores)
```

```
## [1] TRUE
```

```r
carni_mean <- carnivores$mean.hra.m2
mean(carni_mean, na.rm = T)
```

```
## [1] 13039918
```
Herbivores have a larger `mean.hra.m2`

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  

```r
deer_old<- select(homerange, "mean.mass.g","log10.mass","family","genus",'species')
deer_new <- rename(deer_old, mean_mass_g="mean.mass.g", log10_mass="log10.mass")
deer_new
```

```
## # A tibble: 569 x 5
##    mean_mass_g log10_mass family       genus       species    
##          <dbl>      <dbl> <chr>        <chr>       <chr>      
##  1        887       2.95  anguillidae  anguilla    rostrata   
##  2        562       2.75  catostomidae moxostoma   poecilura  
##  3         34       1.53  cyprinidae   campostoma  anomalum   
##  4          4       0.602 cyprinidae   clinostomus funduloides
##  5          4       0.602 cyprinidae   rhinichthys cataractae 
##  6       3525       3.55  esocidae     esox        masquinongy
##  7        737.      2.87  gadidae      pollachius  pollachius 
##  8        449.      2.65  gadidae      pollachius  virens     
##  9        109.      2.04  acanthuridae acanthurus  lineatus   
## 10        772.      2.89  acanthuridae naso        lituratus  
## # … with 559 more rows
```



```r
deers<- filter(deer_new, family =="cervidae")
deer <- arrange(deers, desc(log10_mass))
deer
```

```
## # A tibble: 12 x 5
##    mean_mass_g log10_mass family   genus      species    
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

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column** 

```r
snakess<-filter(homerange,taxa=="snakes")
snakess
```

```
## # A tibble: 41 x 24
##    taxon common.name class order family genus species primarymethod N    
##    <fct> <chr>       <chr> <fct> <chr>  <chr> <chr>   <chr>         <chr>
##  1 snak… western wo… rept… squa… colub… carp… vermis  radiotag      1    
##  2 snak… eastern wo… rept… squa… colub… carp… viridis radiotag      10   
##  3 snak… racer       rept… squa… colub… colu… constr… telemetry     15   
##  4 snak… yellow bel… rept… squa… colub… colu… constr… telemetry     12   
##  5 snak… ringneck s… rept… squa… colub… diad… puncta… mark-recaptu… <NA> 
##  6 snak… eastern in… rept… squa… colub… drym… couperi telemetry     1    
##  7 snak… great plai… rept… squa… colub… elap… guttat… telemetry     12   
##  8 snak… western ra… rept… squa… colub… elap… obsole… telemetry     18   
##  9 snak… hognose sn… rept… squa… colub… hete… platir… telemetry     8    
## 10 snak… European w… rept… squa… colub… hier… viridi… telemetry     32   
## # … with 31 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

```r
min(snakess$mean.hra.m2)
```

```
## [1] 200
```



```r
smallest_homerange <-filter(snakess,mean.hra.m2==200)
smallest_homerange
```

```
## # A tibble: 1 x 24
##   taxon common.name class order family genus species primarymethod N    
##   <fct> <chr>       <chr> <fct> <chr>  <chr> <chr>   <chr>         <chr>
## 1 snak… namaqua dw… rept… squa… viper… bitis schnei… telemetry     11   
## # … with 15 more variables: mean.mass.g <dbl>, log10.mass <dbl>,
## #   alternative.mass.reference <chr>, mean.hra.m2 <dbl>, log10.hra <dbl>,
## #   hra.reference <chr>, realm <chr>, thermoregulation <chr>, locomotion <chr>,
## #   trophic.guild <chr>, dimension <chr>, preymass <dbl>, log10.preymass <dbl>,
## #   PPMR <dbl>, prey.size.reference <chr>
```
According to wikipedia, this is a snake that is native to a coastal region that straddles Nambia and South Africa. It is the smallest snake, has a higher mortality rate, and is considered a venomous snake. 


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
