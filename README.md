<<<<<<< HEAD
## README

My home work
=======
# MyHW
>>>>>>> c77c84f0bbcda696f40bdaf43597a128c822e73b

---
title: "Home Work 5"
author: "Chukwudi Keke"
date: "2022-11-27"
output: html_document
---

```{r setup, include=FALSE}
library(knitr)
library(ggplot2)
library(tidyverse)
library(lubridate)
library(scales)
knitr::opts_chunk$set(echo = FALSE, message = FALSE, warning = FALSE, fig.width = 12, fig.height = 4, tidy = TRUE)
```
```{r}
homicides<-read_csv("homicide-data.csv")
```
```{r}
homicides<-unite(homicides, col='city_name', c('city', 'state'), sep=',') 
homicides<-unite(homicides, col = 'first_last' , c('victim_first', 'victim_last'), sep = ' ')
```
```{r}
baltimore<-homicides %>%
   filter(city_name=="Baltimore,MD") %>%
mutate(reported_date = ymd(reported_date)) %>%
group_by(date = floor_date(reported_date, 'month')) %>%
summarize(homicides = n())

baltimore$month <- format(as.Date(baltimore$date, format="%Y/%m/%d"),"%m")

baltimore$month<-as.numeric(baltimore$month)

baltimore<-baltimore %>%
  mutate(season = case_when(month >= 5 & month <=10 ~ 'summer',
                            month <5 ~'winter',
                           month >10 ~ 'winter'))
```

```{r}
ggplot(baltimore, aes(x = date, weight = homicides, fill = season)) + geom_histogram (bins = 200, binwidth = 20) + 
  scale_fill_manual(values = c('winter' = 'cadetblue3', 
                            'summer' = 'azure3')) + 
  ggtitle("Homicides in Baltimore, MD") + ylab("monthly homicides") + xlab("Date") + theme_dark() + geom_vline(xintercept = as.numeric(as.Date("2015-04-01")), col="red",linetype = "longdash") +
  annotate("text", x = as.Date("2015-04-01"), y = 45, label="Arrest of \n Freddie Gray", color="azure3", size = 3, hjust = 1) 
  
```
```