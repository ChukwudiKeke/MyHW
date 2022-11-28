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