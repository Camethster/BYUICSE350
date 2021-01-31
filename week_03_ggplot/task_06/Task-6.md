---
title: "Exploratory Data Analysis"
author: "Cameron Hansen"
date: "January 30, 2021"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---



# Fix this Chart?

## Orginal  Graph


```r
library(readr) # loading in readr package
library(ggplot2) # loading in ggplot2 package


rcw <- read_csv("https://byuistats.github.io/M335/data/rcw.csv", 
                col_types = cols(Semester_Date = col_date(format = "%m/%d/%y"), 
                                 Semester = col_factor(levels = c("Winter", "Spring", "Fall")))) #takes the data from the github repository and stories it in a vector rwc. 
#Then formates the semester date to a date data type then in month day year order.
# Then takes semester column and turns it into a factor with Winter Spring and Fall as the accepted types 

# displays the first five rows of the vector
head(rcw)
```

```
## # A tibble: 6 x 5
##    Year Semester Semester_Date Count Department
##   <dbl> <fct>    <date>        <dbl> <chr>     
## 1  2016 Spring   2016-04-01        7 Chem      
## 2  2016 Fall     2016-09-01       10 Chem      
## 3  2017 Winter   2017-01-01       21 Chem      
## 4  2017 Spring   2017-04-01        8 Chem      
## 5  2017 Fall     2017-09-01       12 Chem      
## 6  2018 Winter   2018-01-01       16 Chem
```

```r
# Maps the rcw data to the x and y and then groups the data by department shown by color
ggplot(data = rcw, 
       mapping = aes(x = Semester_Date, 
                     y = Count, 
                     color = Department)) +
  geom_line()  + #Creates a line graph
  geom_point() # Creates a point for every observation for each group
```

![](Task-6_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

## My improvements


```r
library(tidyverse)



ggplot(data = rcw) +
  geom_smooth(aes(x = Semester_Date,
                  y = Count))
```

![](Task-6_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
ggplot(data = rcw) +
  geom_bar(mapping = aes(x = Semester,
                         y = Count,
                         fill = Department)
           ,stat="identity")
```

![](Task-6_files/figure-html/unnamed-chunk-3-2.png)<!-- -->

