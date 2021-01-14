---
title: "Lab 3 Homework"
author: "Yoko Takashima"
date: "2021-01-13"
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

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
?msleep
```

```
## starting httpd help server ... done
```

```r
msleep
```

```
## # A tibble: 83 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Chee~ Acin~ carni Carn~ lc                  12.1      NA        NA      11.9
##  2 Owl ~ Aotus omni  Prim~ <NA>                17         1.8      NA       7  
##  3 Moun~ Aplo~ herbi Rode~ nt                  14.4       2.4      NA       9.6
##  4 Grea~ Blar~ omni  Sori~ lc                  14.9       2.3       0.133   9.1
##  5 Cow   Bos   herbi Arti~ domesticated         4         0.7       0.667  20  
##  6 Thre~ Brad~ herbi Pilo~ <NA>                14.4       2.2       0.767   9.6
##  7 Nort~ Call~ carni Carn~ vu                   8.7       1.4       0.383  15.3
##  8 Vesp~ Calo~ <NA>  Rode~ <NA>                 7        NA        NA      17  
##  9 Dog   Canis carni Carn~ domesticated        10.1       2.9       0.333  13.9
## 10 Roe ~ Capr~ herbi Arti~ lc                   3        NA        NA      21  
## # ... with 73 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```

2. Store these data into a new data frame `sleep`.

```r
sleep <-msleep
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(sleep)
```

```
## [1] 83 11
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  

```r
anyNA(sleep)
```

```
## [1] TRUE
```

5. Show a list of the column names is this data frame.

```r
colnames(sleep)
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```


6. How many herbivores are represented in the data?  

```r
table(sleep$vore)
```

```
## 
##   carni   herbi insecti    omni 
##      19      32       5      20
```

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
small <- subset.data.frame(sleep,bodywt <=1)

small
```

```
## # A tibble: 36 x 11
##    name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##    <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
##  1 Owl ~ Aotus omni  Prim~ <NA>                17         1.8      NA       7  
##  2 Grea~ Blar~ omni  Sori~ lc                  14.9       2.3       0.133   9.1
##  3 Vesp~ Calo~ <NA>  Rode~ <NA>                 7        NA        NA      17  
##  4 Guin~ Cavis herbi Rode~ domesticated         9.4       0.8       0.217  14.6
##  5 Chin~ Chin~ herbi Rode~ domesticated        12.5       1.5       0.117  11.5
##  6 Star~ Cond~ omni  Sori~ lc                  10.3       2.2      NA      13.7
##  7 Afri~ Cric~ omni  Rode~ <NA>                 8.3       2        NA      15.7
##  8 Less~ Cryp~ omni  Sori~ lc                   9.1       1.4       0.15   14.9
##  9 Big ~ Epte~ inse~ Chir~ lc                  19.7       3.9       0.117   4.3
## 10 Euro~ Erin~ omni  Erin~ lc                  10.1       3.5       0.283  13.9
## # ... with 26 more rows, and 2 more variables: brainwt <dbl>, bodywt <dbl>
```


```r
large<- subset.data.frame(sleep,bodywt>=200)
large
```

```
## # A tibble: 7 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Cow   Bos   herbi Arti~ domesticated         4         0.7       0.667  20  
## 2 Asia~ Elep~ herbi Prob~ en                   3.9      NA        NA      20.1
## 3 Horse Equus herbi Peri~ domesticated         2.9       0.6       1      21.1
## 4 Gira~ Gira~ herbi Arti~ cd                   1.9       0.4      NA      22.1
## 5 Pilo~ Glob~ carni Ceta~ cd                   2.7       0.1      NA      21.4
## 6 Afri~ Loxo~ herbi Prob~ vu                   3.3      NA        NA      20.7
## 7 Braz~ Tapi~ herbi Peri~ vu                   4.4       1         0.9    19.6
## # ... with 2 more variables: brainwt <dbl>, bodywt <dbl>
```


8. What is the mean weight for both the small and large mammals?

```r
smallwt <- mean(small$bodywt)
smallwt
```

```
## [1] 0.2596667
```


```r
largewt<-mean(large$bodywt)
largewt
```

```
## [1] 1747.071
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  

```r
largesleep <- mean(large$sleep_total)
largesleep
```

```
## [1] 3.3
```


```r
smallsleep <- mean(small$sleep_total)
smallsleep
```

```
## [1] 12.65833
```
On average, smaller animals sleep longer. 

10. Which animal is the sleepiest among the entire dataframe?

```r
summary(sleep)
```

```
##      name              genus               vore              order          
##  Length:83          Length:83          Length:83          Length:83         
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  conservation        sleep_total      sleep_rem      sleep_cycle    
##  Length:83          Min.   : 1.90   Min.   :0.100   Min.   :0.1167  
##  Class :character   1st Qu.: 7.85   1st Qu.:0.900   1st Qu.:0.1833  
##  Mode  :character   Median :10.10   Median :1.500   Median :0.3333  
##                     Mean   :10.43   Mean   :1.875   Mean   :0.4396  
##                     3rd Qu.:13.75   3rd Qu.:2.400   3rd Qu.:0.5792  
##                     Max.   :19.90   Max.   :6.600   Max.   :1.5000  
##                                     NA's   :22      NA's   :51      
##      awake          brainwt            bodywt        
##  Min.   : 4.10   Min.   :0.00014   Min.   :   0.005  
##  1st Qu.:10.25   1st Qu.:0.00290   1st Qu.:   0.174  
##  Median :13.90   Median :0.01240   Median :   1.670  
##  Mean   :13.57   Mean   :0.28158   Mean   : 166.136  
##  3rd Qu.:16.15   3rd Qu.:0.12550   3rd Qu.:  41.750  
##  Max.   :22.10   Max.   :5.71200   Max.   :6654.000  
##                  NA's   :27
```

```r
max(sleep$sleep_total)
```

```
## [1] 19.9
```


```r
sleepiest <- subset(sleep, sleep_total ==19.9)
sleepiest
```

```
## # A tibble: 1 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Litt~ Myot~ inse~ Chir~ <NA>                19.9         2         0.2   4.1
## # ... with 2 more variables: brainwt <dbl>, bodywt <dbl>
```
The animal that is the sleepiest is the little brown bat. 

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
