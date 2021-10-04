---
title: "HW1"
author: "Haoran Zhang"
date: "2021/9/22"
output=github_document
---




```r
library(data.table)
```

```
## Warning: package 'data.table' was built under R version 4.0.5
```

```r
library(dtplyr)
```

```
## Warning: package 'dtplyr' was built under R version 4.0.5
```

```r
library(dplyr)
```

```
## Warning: package 'dplyr' was built under R version 4.0.5
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:data.table':
## 
##     between, first, last
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(readr)
```

```
## Warning: package 'readr' was built under R version 4.0.5
```

```r
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 4.0.5
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.5     v purrr   0.3.4
## v tibble  3.1.4     v stringr 1.4.0
## v tidyr   1.1.3     v forcats 0.5.1
```

```
## Warning: package 'ggplot2' was built under R version 4.0.5
```

```
## Warning: package 'tibble' was built under R version 4.0.5
```

```
## Warning: package 'tidyr' was built under R version 4.0.5
```

```
## Warning: package 'purrr' was built under R version 4.0.3
```

```
## Warning: package 'stringr' was built under R version 4.0.5
```

```
## Warning: package 'forcats' was built under R version 4.0.5
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::between()   masks data.table::between()
## x dplyr::filter()    masks stats::filter()
## x dplyr::first()     masks data.table::first()
## x dplyr::lag()       masks stats::lag()
## x dplyr::last()      masks data.table::last()
## x purrr::transpose() masks data.table::transpose()
```

```r
library(skimr)
```

```
## Warning: package 'skimr' was built under R version 4.0.5
```

```r
library(lubridate)
```

```
## Warning: package 'lubridate' was built under R version 4.0.5
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:data.table':
## 
##     hour, isoweek, mday, minute, month, quarter, second, wday, week,
##     yday, year
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(leaflet)
```

```
## Warning: package 'leaflet' was built under R version 4.0.5
```
## 1. Import and check the data.

```r
pm04 <- fread("ad_viz_plotval_data_2004.csv")

pm19 <- fread("ad_viz_plotval_data_2019.csv")
```
Check the variables of 2004

```r
dim(pm04)
```

```
## [1] 19233    20
```

```r
names(pm04)
```

```
##  [1] "Date"               "Source"             "Site ID"           
##  [4] "POC"                "DMC"                "UNITS"             
##  [7] "DAILY_AQI_VALUE"    "site"               "DAILY_OBS_COUNT"   
## [10] "PERCENT_COMPLETE"   "AQS_PARAMETER_CODE" "AQS_PARAMETER_DESC"
## [13] "CBSA_CODE"          "CBSA_NAME"          "STATE_CODE"        
## [16] "STATE"              "COUNTY_CODE"        "COUNTY"            
## [19] "lat"                "lon"
```

```r
str(pm04)
```

```
## Classes 'data.table' and 'data.frame':	19233 obs. of  20 variables:
##  $ Date              : chr  "01/01/2004" "01/02/2004" "01/03/2004" "01/04/2004" ...
##  $ Source            : chr  "AQS" "AQS" "AQS" "AQS" ...
##  $ Site ID           : int  60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 ...
##  $ POC               : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ DMC               : num  11 12.2 16.5 18.1 11.5 32.5 14 29.9 21 15.7 ...
##  $ UNITS             : chr  "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" ...
##  $ DAILY_AQI_VALUE   : int  46 51 60 64 48 94 55 88 70 59 ...
##  $ site              : chr  "Livermore" "Livermore" "Livermore" "Livermore" ...
##  $ DAILY_OBS_COUNT   : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ PERCENT_COMPLETE  : int  100 100 100 100 100 100 100 100 100 100 ...
##  $ AQS_PARAMETER_CODE: int  88502 88502 88502 88101 88502 88502 88101 88502 88502 88101 ...
##  $ AQS_PARAMETER_DESC: chr  "Acceptable PM2.5 AQI & Speciation Mass" "Acceptable PM2.5 AQI & Speciation Mass" "Acceptable PM2.5 AQI & Speciation Mass" "PM2.5 - Local Conditions" ...
##  $ CBSA_CODE         : int  41860 41860 41860 41860 41860 41860 41860 41860 41860 41860 ...
##  $ CBSA_NAME         : chr  "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" ...
##  $ STATE_CODE        : int  6 6 6 6 6 6 6 6 6 6 ...
##  $ STATE             : chr  "California" "California" "California" "California" ...
##  $ COUNTY_CODE       : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ COUNTY            : chr  "Alameda" "Alameda" "Alameda" "Alameda" ...
##  $ lat               : num  37.7 37.7 37.7 37.7 37.7 ...
##  $ lon               : num  -122 -122 -122 -122 -122 ...
##  - attr(*, ".internal.selfref")=<externalptr>
```

```r
head(pm04)
```

```
##          Date Source  Site ID POC  DMC    UNITS DAILY_AQI_VALUE      site
## 1: 01/01/2004    AQS 60010007   1 11.0 ug/m3 LC              46 Livermore
## 2: 01/02/2004    AQS 60010007   1 12.2 ug/m3 LC              51 Livermore
## 3: 01/03/2004    AQS 60010007   1 16.5 ug/m3 LC              60 Livermore
## 4: 01/04/2004    AQS 60010007   1 18.1 ug/m3 LC              64 Livermore
## 5: 01/05/2004    AQS 60010007   1 11.5 ug/m3 LC              48 Livermore
## 6: 01/06/2004    AQS 60010007   1 32.5 ug/m3 LC              94 Livermore
##    DAILY_OBS_COUNT PERCENT_COMPLETE AQS_PARAMETER_CODE
## 1:               1              100              88502
## 2:               1              100              88502
## 3:               1              100              88502
## 4:               1              100              88101
## 5:               1              100              88502
## 6:               1              100              88502
##                        AQS_PARAMETER_DESC CBSA_CODE
## 1: Acceptable PM2.5 AQI & Speciation Mass     41860
## 2: Acceptable PM2.5 AQI & Speciation Mass     41860
## 3: Acceptable PM2.5 AQI & Speciation Mass     41860
## 4:               PM2.5 - Local Conditions     41860
## 5: Acceptable PM2.5 AQI & Speciation Mass     41860
## 6: Acceptable PM2.5 AQI & Speciation Mass     41860
##                            CBSA_NAME STATE_CODE      STATE COUNTY_CODE  COUNTY
## 1: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 2: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 3: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 4: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 5: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
## 6: San Francisco-Oakland-Hayward, CA          6 California           1 Alameda
##         lat       lon
## 1: 37.68753 -121.7842
## 2: 37.68753 -121.7842
## 3: 37.68753 -121.7842
## 4: 37.68753 -121.7842
## 5: 37.68753 -121.7842
## 6: 37.68753 -121.7842
```

```r
tail(pm04)
```

```
##          Date Source  Site ID POC DMC    UNITS DAILY_AQI_VALUE
## 1: 12/14/2004    AQS 61131003   1  11 ug/m3 LC              46
## 2: 12/17/2004    AQS 61131003   1  16 ug/m3 LC              59
## 3: 12/20/2004    AQS 61131003   1  17 ug/m3 LC              61
## 4: 12/23/2004    AQS 61131003   1   9 ug/m3 LC              38
## 5: 12/26/2004    AQS 61131003   1  24 ug/m3 LC              76
## 6: 12/29/2004    AQS 61131003   1   9 ug/m3 LC              38
##                    site DAILY_OBS_COUNT PERCENT_COMPLETE AQS_PARAMETER_CODE
## 1: Woodland-Gibson Road               1              100              88101
## 2: Woodland-Gibson Road               1              100              88101
## 3: Woodland-Gibson Road               1              100              88101
## 4: Woodland-Gibson Road               1              100              88101
## 5: Woodland-Gibson Road               1              100              88101
## 6: Woodland-Gibson Road               1              100              88101
##          AQS_PARAMETER_DESC CBSA_CODE                               CBSA_NAME
## 1: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 2: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 3: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 4: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 5: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 6: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
##    STATE_CODE      STATE COUNTY_CODE COUNTY      lat       lon
## 1:          6 California         113   Yolo 38.66121 -121.7327
## 2:          6 California         113   Yolo 38.66121 -121.7327
## 3:          6 California         113   Yolo 38.66121 -121.7327
## 4:          6 California         113   Yolo 38.66121 -121.7327
## 5:          6 California         113   Yolo 38.66121 -121.7327
## 6:          6 California         113   Yolo 38.66121 -121.7327
```
Check the variables of 2019

```r
dim(pm19)
```

```
## [1] 53086    20
```

```r
names(pm19)
```

```
##  [1] "Date"               "Source"             "Site ID"           
##  [4] "POC"                "DMC"                "UNITS"             
##  [7] "DAILY_AQI_VALUE"    "site"               "DAILY_OBS_COUNT"   
## [10] "PERCENT_COMPLETE"   "AQS_PARAMETER_CODE" "AQS_PARAMETER_DESC"
## [13] "CBSA_CODE"          "CBSA_NAME"          "STATE_CODE"        
## [16] "STATE"              "COUNTY_CODE"        "COUNTY"            
## [19] "lat"                "lon"
```

```r
str(pm19)
```

```
## Classes 'data.table' and 'data.frame':	53086 obs. of  20 variables:
##  $ Date              : chr  "01/01/2019" "01/02/2019" "01/03/2019" "01/04/2019" ...
##  $ Source            : chr  "AQS" "AQS" "AQS" "AQS" ...
##  $ Site ID           : int  60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 ...
##  $ POC               : int  3 3 3 3 3 3 3 3 3 3 ...
##  $ DMC               : num  5.7 11.9 20.1 28.8 11.2 2.7 2.8 7 3.1 7.1 ...
##  $ UNITS             : chr  "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" ...
##  $ DAILY_AQI_VALUE   : int  24 50 68 86 47 11 12 29 13 30 ...
##  $ site              : chr  "Livermore" "Livermore" "Livermore" "Livermore" ...
##  $ DAILY_OBS_COUNT   : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ PERCENT_COMPLETE  : int  100 100 100 100 100 100 100 100 100 100 ...
##  $ AQS_PARAMETER_CODE: int  88101 88101 88101 88101 88101 88101 88101 88101 88101 88101 ...
##  $ AQS_PARAMETER_DESC: chr  "PM2.5 - Local Conditions" "PM2.5 - Local Conditions" "PM2.5 - Local Conditions" "PM2.5 - Local Conditions" ...
##  $ CBSA_CODE         : int  41860 41860 41860 41860 41860 41860 41860 41860 41860 41860 ...
##  $ CBSA_NAME         : chr  "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" ...
##  $ STATE_CODE        : int  6 6 6 6 6 6 6 6 6 6 ...
##  $ STATE             : chr  "California" "California" "California" "California" ...
##  $ COUNTY_CODE       : int  1 1 1 1 1 1 1 1 1 1 ...
##  $ COUNTY            : chr  "Alameda" "Alameda" "Alameda" "Alameda" ...
##  $ lat               : num  37.7 37.7 37.7 37.7 37.7 ...
##  $ lon               : num  -122 -122 -122 -122 -122 ...
##  - attr(*, ".internal.selfref")=<externalptr>
```

```r
head(pm19)
```

```
##          Date Source  Site ID POC  DMC    UNITS DAILY_AQI_VALUE      site
## 1: 01/01/2019    AQS 60010007   3  5.7 ug/m3 LC              24 Livermore
## 2: 01/02/2019    AQS 60010007   3 11.9 ug/m3 LC              50 Livermore
## 3: 01/03/2019    AQS 60010007   3 20.1 ug/m3 LC              68 Livermore
## 4: 01/04/2019    AQS 60010007   3 28.8 ug/m3 LC              86 Livermore
## 5: 01/05/2019    AQS 60010007   3 11.2 ug/m3 LC              47 Livermore
## 6: 01/06/2019    AQS 60010007   3  2.7 ug/m3 LC              11 Livermore
##    DAILY_OBS_COUNT PERCENT_COMPLETE AQS_PARAMETER_CODE       AQS_PARAMETER_DESC
## 1:               1              100              88101 PM2.5 - Local Conditions
## 2:               1              100              88101 PM2.5 - Local Conditions
## 3:               1              100              88101 PM2.5 - Local Conditions
## 4:               1              100              88101 PM2.5 - Local Conditions
## 5:               1              100              88101 PM2.5 - Local Conditions
## 6:               1              100              88101 PM2.5 - Local Conditions
##    CBSA_CODE                         CBSA_NAME STATE_CODE      STATE
## 1:     41860 San Francisco-Oakland-Hayward, CA          6 California
## 2:     41860 San Francisco-Oakland-Hayward, CA          6 California
## 3:     41860 San Francisco-Oakland-Hayward, CA          6 California
## 4:     41860 San Francisco-Oakland-Hayward, CA          6 California
## 5:     41860 San Francisco-Oakland-Hayward, CA          6 California
## 6:     41860 San Francisco-Oakland-Hayward, CA          6 California
##    COUNTY_CODE  COUNTY      lat       lon
## 1:           1 Alameda 37.68753 -121.7842
## 2:           1 Alameda 37.68753 -121.7842
## 3:           1 Alameda 37.68753 -121.7842
## 4:           1 Alameda 37.68753 -121.7842
## 5:           1 Alameda 37.68753 -121.7842
## 6:           1 Alameda 37.68753 -121.7842
```

```r
tail(pm19)
```

```
##          Date Source  Site ID POC  DMC    UNITS DAILY_AQI_VALUE
## 1: 11/11/2019    AQS 61131003   1 13.5 ug/m3 LC              54
## 2: 11/17/2019    AQS 61131003   1 18.1 ug/m3 LC              64
## 3: 11/29/2019    AQS 61131003   1 12.5 ug/m3 LC              52
## 4: 12/17/2019    AQS 61131003   1 23.8 ug/m3 LC              76
## 5: 12/23/2019    AQS 61131003   1  1.0 ug/m3 LC               4
## 6: 12/29/2019    AQS 61131003   1  9.1 ug/m3 LC              38
##                    site DAILY_OBS_COUNT PERCENT_COMPLETE AQS_PARAMETER_CODE
## 1: Woodland-Gibson Road               1              100              88101
## 2: Woodland-Gibson Road               1              100              88101
## 3: Woodland-Gibson Road               1              100              88101
## 4: Woodland-Gibson Road               1              100              88101
## 5: Woodland-Gibson Road               1              100              88101
## 6: Woodland-Gibson Road               1              100              88101
##          AQS_PARAMETER_DESC CBSA_CODE                               CBSA_NAME
## 1: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 2: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 3: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 4: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 5: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
## 6: PM2.5 - Local Conditions     40900 Sacramento--Roseville--Arden-Arcade, CA
##    STATE_CODE      STATE COUNTY_CODE COUNTY      lat       lon
## 1:          6 California         113   Yolo 38.66121 -121.7327
## 2:          6 California         113   Yolo 38.66121 -121.7327
## 3:          6 California         113   Yolo 38.66121 -121.7327
## 4:          6 California         113   Yolo 38.66121 -121.7327
## 5:          6 California         113   Yolo 38.66121 -121.7327
## 6:          6 California         113   Yolo 38.66121 -121.7327
```
Check the data of 2004

```r
pm04[,table(is.na(DMC))]
```

```
## 
## FALSE 
## 19233
```

```r
pm04[,table(is.na(`Site ID`))]
```

```
## 
## FALSE 
## 19233
```

```r
pm04[,table(is.na(DAILY_AQI_VALUE))]
```

```
## 
## FALSE 
## 19233
```

```r
pm04[,table(is.na(lat))]
```

```
## 
## FALSE 
## 19233
```

```r
pm04[,table(is.na(lon))]
```

```
## 
## FALSE 
## 19233
```

```r
pm04[,range(lat)]
```

```
## [1] 32.63124 41.71182
```

```r
pm04[,range(lon)]
```

```
## [1] -124.1621 -115.4831
```

```r
pm04[,range(DMC)]
```

```
## [1]  -0.1 251.0
```

```r
pm04 <- pm04[DMC>=0]
```
Check the data of 2019

```r
pm19[,table(is.na(DMC))]
```

```
## 
## FALSE 
## 53086
```

```r
pm19[,table(is.na(`Site ID`))]
```

```
## 
## FALSE 
## 53086
```

```r
pm19[,table(is.na(DAILY_AQI_VALUE))]
```

```
## 
## FALSE 
## 53086
```

```r
pm19[,table(is.na(lat))]
```

```
## 
## FALSE 
## 53086
```

```r
pm19[,table(is.na(lon))]
```

```
## 
## FALSE 
## 53086
```

```r
pm19[,range(lat)]
```

```
## [1] 32.57816 41.75613
```

```r
pm19[,range(lon)]
```

```
## [1] -124.2035 -115.4831
```

```r
pm19[,range(DMC)]
```

```
## [1]  -2.2 120.9
```

```r
pm19 <- pm19[DMC>=0]
```

## 2. Combine the two years of data into one data frame and add an year variable.

```r
pm_all <- rbind(pm04,pm19)
pm_all$Date <- mdy(pm_all$Date)
pm_all$year <- year(pm_all$Date)
```
## 3. Create a basic map in leaflet() that shows the locations of the sites (make sure to use different colors for each year). Summarize the spatial distribution of the monitoring sites.

```r
year.pal <- colorFactor(c('blue','red'), domain=pm_all$year)

OB04<-pm_all[pm_all$year==2004]
OB19<-pm_all[pm_all$year==2019]
library(leaflet)
leaflet(pm_all) %>% 
  addProviderTiles('CartoDB.Positron') %>% 
  addCircles(
    data = OB04,
    lat = ~lat, lng = ~lon, popup = "2004.",
    opacity = 1, fillOpacity = 1, radius = 400, color = "blue"
    ) %>%
  addCircles(
    data = OB19,
    lat = ~lat, lng = ~lon, popup = "2019.",
    opacity=0.5, fillOpacity=0.5, radius = 400, color = "red"
    ) %>%
  addLegend('bottomleft', pal=year.pal, values=pm_all$year,
          title='Sites', opacity=1)
```



It seems that the number of sites in 2019 is much more than that of 2014, or maybe they just  overlap. These sites are distributed mostly around bay area and Southern California, while relatively few sites locate inland.

## 4.Check for any missing or implausible values of PM2.5 in the combined dataset. Explore the proportions of each and provide a summary of any temporal patterns you see in these observations.
We've cleared all negative readings before so we'll focus on high reading values.

```r
pm_all[,DMC_cat:=fifelse(DMC<60,"low-concen",
                       fifelse(DMC<120,"mid-concen",
                               "high-concen"))]
table(pm_all$DMC_cat)
```

```
## 
## high-concen  low-concen  mid-concen 
##           5       71918         113
```

```r
high<-pm_all[DMC>120]
leaflet(pm_all) %>% 
  addProviderTiles('CartoDB.Positron') %>%
    addCircles(
    data = high,
    lat = ~lat, lng = ~lon, popup = ">120",
    opacity = 1, fillOpacity = 1, radius = 400, color = "red"
    ) 
```

```{=html}
<div id="htmlwidget-db8a03af5924bed03e92" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-db8a03af5924bed03e92">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addProviderTiles","args":["CartoDB.Positron",null,null,{"errorTileUrl":"","noWrap":false,"detectRetina":false}]},{"method":"addCircles","args":[[37.748707,37.748707,37.748707,37.748707,34.19925],[-119.587094,-119.587094,-119.587094,-119.587094,-118.53276],400,null,null,{"interactive":true,"className":"","stroke":true,"color":"red","weight":5,"opacity":1,"fill":true,"fillColor":"red","fillOpacity":1},">120",null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null,null]}],"limits":{"lat":[34.19925,37.748707],"lng":[-119.587094,-118.53276]}},"evals":[],"jsHooks":[]}</script>
```
There are five datapoints that are extremely high(>=120), four of them were measured from 07/18/2004 to 07/21/2004. Noticing that the data was observed at Yosemite Visitor Center, I checked the internet and noticed that a meadow fire took place during that time and maybe that was the cause of such extremely high PM2.5 concentration.

## 5. Explore the main question of interest at three different spatial levels. Create exploratory plots (e.g. boxplots, histograms, line plots) and summary statistics that best suit each level of data. Be sure to write up explanations of what you observe in these data.
Violin

```r
pm_all_norm<-pm_all[DMC<120]
ggplot(pm_all_norm ,mapping=aes(y=DMC,x=1))+
  geom_violin()+
  facet_grid(~year)
```

![](HW1_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

summary

```r
pm_all_norm[!is.na(site)] %>%
  ggplot() + 
    stat_summary(mapping = aes(x = year, y = DMC),
    fun.min = min,
    fun.max = max,
    fun = median)
```

![](HW1_files/figure-html/unnamed-chunk-12-1.png)<!-- -->
Histogram

```r
ggplot(pm_all_norm, aes(x = DMC)) +
  geom_histogram() +
  facet_wrap(. ~ year)
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](HW1_files/figure-html/unnamed-chunk-13-1.png)<!-- -->
From these graphs we can see there is a slight decrease of daily mean PM2.5 concentration over the last 15 years.


```r
ggplot( 
  pm_all[!is.na(DMC)], 
  mapping = aes( y = DMC, x = COUNTY, color = year)) +
  geom_point() +
  theme(axis.text.x = element_text(angle=90, hjust=1, vjust=1))
```

![](HW1_files/figure-html/unnamed-chunk-14-1.png)<!-- -->
In this point graph, black dots represent readings in 2004 while blue dots represent readings in 2019. We can see that there is an significantly decrease of daily mean PM2.5 concentration over the 15 years.





```r
ggplot( 
  pm_all[!is.na(DMC)],
  mapping = aes( y = DMC, x = COUNTY)) +
  geom_point() +
  facet_wrap(. ~ year)+
  theme(axis.text.x = element_text(angle=90, hjust=1, vjust=1,size = 5))
```

![](HW1_files/figure-html/unnamed-chunk-15-1.png)<!-- -->
Sites in Los Angeles

```r
LAsites<-pm_all[COUNTY=="Los Angeles"]
LAsites[!is.na(site)]
```

```
##             Date Source  Site ID POC  DMC    UNITS DAILY_AQI_VALUE  site
##    1: 2004-01-01    AQS 60370002   1 18.0 ug/m3 LC              63 Azusa
##    2: 2004-01-02    AQS 60370002   1 20.4 ug/m3 LC              68 Azusa
##    3: 2004-01-03    AQS 60370002   1  8.0 ug/m3 LC              33 Azusa
##    4: 2004-01-07    AQS 60370002   1 23.6 ug/m3 LC              75 Azusa
##    5: 2004-01-08    AQS 60370002   1 28.3 ug/m3 LC              85 Azusa
##   ---                                                                   
## 7127: 2019-12-14    AQS 60379034   1  2.8 ug/m3 LC              12 Lebec
## 7128: 2019-12-17    AQS 60379034   1  1.4 ug/m3 LC               6 Lebec
## 7129: 2019-12-20    AQS 60379034   1  1.1 ug/m3 LC               5 Lebec
## 7130: 2019-12-23    AQS 60379034   1  0.5 ug/m3 LC               2 Lebec
## 7131: 2019-12-26    AQS 60379034   1  0.3 ug/m3 LC               1 Lebec
##       DAILY_OBS_COUNT PERCENT_COMPLETE AQS_PARAMETER_CODE
##    1:               1              100              88101
##    2:               1              100              88101
##    3:               1              100              88101
##    4:               1              100              88101
##    5:               1              100              88101
##   ---                                                    
## 7127:               1              100              88502
## 7128:               1              100              88502
## 7129:               1              100              88502
## 7130:               1              100              88502
## 7131:               1              100              88502
##                           AQS_PARAMETER_DESC CBSA_CODE
##    1:               PM2.5 - Local Conditions     31080
##    2:               PM2.5 - Local Conditions     31080
##    3:               PM2.5 - Local Conditions     31080
##    4:               PM2.5 - Local Conditions     31080
##    5:               PM2.5 - Local Conditions     31080
##   ---                                                 
## 7127: Acceptable PM2.5 AQI & Speciation Mass     31080
## 7128: Acceptable PM2.5 AQI & Speciation Mass     31080
## 7129: Acceptable PM2.5 AQI & Speciation Mass     31080
## 7130: Acceptable PM2.5 AQI & Speciation Mass     31080
## 7131: Acceptable PM2.5 AQI & Speciation Mass     31080
##                                CBSA_NAME STATE_CODE      STATE COUNTY_CODE
##    1: Los Angeles-Long Beach-Anaheim, CA          6 California          37
##    2: Los Angeles-Long Beach-Anaheim, CA          6 California          37
##    3: Los Angeles-Long Beach-Anaheim, CA          6 California          37
##    4: Los Angeles-Long Beach-Anaheim, CA          6 California          37
##    5: Los Angeles-Long Beach-Anaheim, CA          6 California          37
##   ---                                                                     
## 7127: Los Angeles-Long Beach-Anaheim, CA          6 California          37
## 7128: Los Angeles-Long Beach-Anaheim, CA          6 California          37
## 7129: Los Angeles-Long Beach-Anaheim, CA          6 California          37
## 7130: Los Angeles-Long Beach-Anaheim, CA          6 California          37
## 7131: Los Angeles-Long Beach-Anaheim, CA          6 California          37
##            COUNTY      lat       lon year    DMC_cat
##    1: Los Angeles 34.13650 -117.9239 2004 low-concen
##    2: Los Angeles 34.13650 -117.9239 2004 low-concen
##    3: Los Angeles 34.13650 -117.9239 2004 low-concen
##    4: Los Angeles 34.13650 -117.9239 2004 low-concen
##    5: Los Angeles 34.13650 -117.9239 2004 low-concen
##   ---                                               
## 7127: Los Angeles 34.81303 -118.8848 2019 low-concen
## 7128: Los Angeles 34.81303 -118.8848 2019 low-concen
## 7129: Los Angeles 34.81303 -118.8848 2019 low-concen
## 7130: Los Angeles 34.81303 -118.8848 2019 low-concen
## 7131: Los Angeles 34.81303 -118.8848 2019 low-concen
```

```r
ggplot( 
  LAsites[!is.na(site)], 
  mapping = aes( y = DMC, x = site)) +
  geom_boxplot() +
   facet_wrap(. ~ year)+
 theme(axis.text.x = element_text(angle=90, hjust=1, vjust=0.1))
```

![](HW1_files/figure-html/unnamed-chunk-16-1.png)<!-- -->
The first boxplot represents those data with missing sites thus should be ignored. For those with applicable sites, we can see that Los Angeles main street which had the highest daily mean PM2.5 concentration in 2004 has decreased during the 15-year period.

## 6. Conclusion
From those plots above, we can see that the daily mean PM2.5 concentration did decrease during the 15-year period.
