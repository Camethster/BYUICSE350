---
title: "Task 11"
author: "Cameron Hansen"
date: "February 09, 2021"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---



## Covid



```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.0.4     v dplyr   1.0.2
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.0
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(scales)
```

```
## 
## Attaching package: 'scales'
```

```
## The following object is masked from 'package:purrr':
## 
##     discard
```

```
## The following object is masked from 'package:readr':
## 
##     col_factor
```

```r
covid <- read_csv("https://github.com/ktoutloud/classslides/raw/master/math335/data/M335_excess-mortality-p-scores.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   date = col_date(format = "")
## )
## i Use `spec()` for the full column specifications.
```

```r
pivot_covid  <- transform(covid, date = as.Date(date)) %>% 
  mutate(Spain = Spain*100) %>% 
  pivot_longer(cols = -date,
               names_to = "country",
               values_to = "percents") %>% 
  as_tibble()

x_labs <- c("Jan 5, 2020","Mar 11","Apr 30","Jun 19","Aug 8","Sep 27","Nov 16","
Jan 24, 2021")
x_breaks <- as.Date(c("2020-01-05","2020-03-11","2020-04-30","2020-06-19","2020-08-08","2020-09-27","2020-11-16","2021-01-2"))


tidy_covid  <- pivot_covid %>% 
  filter(country %in% c("England...Wales","Germany", "Spain","Norway"), na.rm =TRUE) 
graph <- ggplot(tidy_covid,aes(x=date,y=percents/100, color=country))  +
  theme_bw() +
  scale_x_continuous(breaks = x_breaks, labels = x_labs) +
  scale_y_continuous(breaks = seq(0.00,1.40,.20), labels = percent) +
  theme(panel.grid = element_blank(),
        panel.grid.major.y = element_line("grey90",linetype = 2),
        panel.border = element_blank(),
        axis.title = element_blank(),
        legend.position = "none") 
  
graph
```

![](Task-11_files/figure-html/unnamed-chunk-1-1.png)<!-- -->


## Highlight Plots

### Text

```r
graph + 
  geom_line() +
  geom_point() +
  geom_line(mapping= aes(y=1.00),color="grey") +
  geom_text(x=as.Date("2020-06-19"),y = 1.20, label = "Over 100%", color="grey")
```

```
## Warning: Removed 9 row(s) containing missing values (geom_path).
```

```
## Warning: Removed 9 rows containing missing values (geom_point).
```

![](Task-11_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

### Fill

```r
graph + 
  geom_line() +
  geom_point() +
  geom_rect(xmin=as.Date("2020-01-05"),
            xmax=as.Date("2021-01-24"),
            ymin=1,
            ymax=1.60,
            color = "firebrick",
            fill = NA,
            alpha = 0.2,
            linetype = 1)
```

```
## Warning: Removed 9 row(s) containing missing values (geom_path).
```

```
## Warning: Removed 9 rows containing missing values (geom_point).
```

![](Task-11_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

### Line

```r
graph + 
  geom_point(mapping = aes(x = date, y = percents/100,group = country, color = percents > 100),size = 1)
```

```
## Warning: Removed 9 rows containing missing values (geom_point).
```

![](Task-11_files/figure-html/unnamed-chunk-4-1.png)<!-- -->


### US plots


```r
US_Covid <- filter(pivot_covid, country %in% c("England...Wales","Germany", "Spain","Norway", "United.States"),na.rm = TRUE) 
View(US_Covid)

US_graph <- ggplot(US_Covid,aes(x = date,y = percents / 100, color = country))  +
  theme_bw() +
  scale_x_continuous(breaks = x_breaks, labels = x_labs) +
  scale_y_continuous(breaks = seq(0.00,1.40,.20), labels = percent) +
  theme(panel.grid = element_blank(),
        panel.grid.major.y = element_line("grey90",linetype = 2),
        panel.border = element_blank(),
        axis.title = element_blank(),
        legend.position = "none") +
  geom_line()
  
US_graph
```

```
## Warning: Removed 15 row(s) containing missing values (geom_path).
```

![](Task-11_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

