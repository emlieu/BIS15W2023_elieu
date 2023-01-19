---
title: "Lab 3 Homework"
author: "Emily Lieu"
date: "2023-01-19"
output:
  html_document:
    theme: spacelab
    toc: no
    keep_md: yes 
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
getwd()
```

```
## [1] "C:/Users/emily/OneDrive/Desktop/BIS15W2023_elieu-main/lab3"
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

```r
?msleep
```

```
## starting httpd help server ... done
```
The data is taken from the National Academy of Sciences.

2. Store these data into a new data frame `sleep`.


```r
sleep <- msleep
sleep
```

```
## # A tibble: 83 × 11
##    name         genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt
##    <chr>        <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>
##  1 Cheetah      Acin… carni Carn… lc         12.1    NA    NA      11.9 NA      
##  2 Owl monkey   Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155 
##  3 Mountain be… Aplo… herbi Rode… nt         14.4     2.4  NA       9.6 NA      
##  4 Greater sho… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029
##  5 Cow          Bos   herbi Arti… domest…     4       0.7   0.667  20    0.423  
##  6 Three-toed … Brad… herbi Pilo… <NA>       14.4     2.2   0.767   9.6 NA      
##  7 Northern fu… Call… carni Carn… vu          8.7     1.4   0.383  15.3 NA      
##  8 Vesper mouse Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA      
##  9 Dog          Canis carni Carn… domest…    10.1     2.9   0.333  13.9  0.07   
## 10 Roe deer     Capr… herbi Arti… lc          3      NA    NA      21    0.0982 
## # … with 73 more rows, 1 more variable: bodywt <dbl>, and abbreviated variable
## #   names ¹​conservation, ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below.  

```r
dim(sleep)
```

```
## [1] 83 11
```
I know there are 83 observations and 11 variables because it's stated in the environment. 

4. Are there any NAs in the data? How did you determine this? Please show your code.  

```r
anyNA(sleep)
```

```
## [1] TRUE
```

There are NAs because after being run, the program said true. 

5. Show a list of the column names is this data frame.

```r
names(sleep)
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
There are 32 herbivores. 

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
large <- filter(sleep, bodywt<=200)
large
```

```
## # A tibble: 76 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Chee… Acin… carni Carn… lc         12.1    NA    NA      11.9 NA       50    
##  2 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  3 Moun… Aplo… herbi Rode… nt         14.4     2.4  NA       9.6 NA        1.35 
##  4 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  5 Thre… Brad… herbi Pilo… <NA>       14.4     2.2   0.767   9.6 NA        3.85 
##  6 Nort… Call… carni Carn… vu          8.7     1.4   0.383  15.3 NA       20.5  
##  7 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  8 Dog   Canis carni Carn… domest…    10.1     2.9   0.333  13.9  0.07    14    
##  9 Roe … Capr… herbi Arti… lc          3      NA    NA      21    0.0982  14.8  
## 10 Goat  Capri herbi Arti… lc          5.3     0.6  NA      18.7  0.115   33.5  
## # … with 66 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```


```r
small <- filter(sleep, bodywt<=1)
small
```

```
## # A tibble: 36 × 11
##    name  genus vore  order conse…¹ sleep…² sleep…³ sleep…⁴ awake  brainwt bodywt
##    <chr> <chr> <chr> <chr> <chr>     <dbl>   <dbl>   <dbl> <dbl>    <dbl>  <dbl>
##  1 Owl … Aotus omni  Prim… <NA>       17       1.8  NA       7    0.0155   0.48 
##  2 Grea… Blar… omni  Sori… lc         14.9     2.3   0.133   9.1  0.00029  0.019
##  3 Vesp… Calo… <NA>  Rode… <NA>        7      NA    NA      17   NA        0.045
##  4 Guin… Cavis herbi Rode… domest…     9.4     0.8   0.217  14.6  0.0055   0.728
##  5 Chin… Chin… herbi Rode… domest…    12.5     1.5   0.117  11.5  0.0064   0.42 
##  6 Star… Cond… omni  Sori… lc         10.3     2.2  NA      13.7  0.001    0.06 
##  7 Afri… Cric… omni  Rode… <NA>        8.3     2    NA      15.7  0.0066   1    
##  8 Less… Cryp… omni  Sori… lc          9.1     1.4   0.15   14.9  0.00014  0.005
##  9 Big … Epte… inse… Chir… lc         19.7     3.9   0.117   4.3  0.0003   0.023
## 10 Euro… Erin… omni  Erin… lc         10.1     3.5   0.283  13.9  0.0035   0.77 
## # … with 26 more rows, and abbreviated variable names ¹​conservation,
## #   ²​sleep_total, ³​sleep_rem, ⁴​sleep_cycle
```

8. What is the mean weight for both the small and large mammals?

```r
mean(small$bodywt)
```

```
## [1] 0.2596667
```


```r
mean(large$bodywt)
```

```
## [1] 20.52396
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  

```r
mean(small$sleep_total)
```

```
## [1] 12.65833
```


```r
mean(large$sleep_total)
```

```
## [1] 11.09079
```
Smaller animals sleep longer on average. 

10. Which animal is the sleepiest among the entire data frame?

```r
max(sleep$sleep_total)
```

```
## [1] 19.9
```
The little brown bat is the sleepiest. 

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
