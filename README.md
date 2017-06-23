---
title: "Automated Content Analysis in R"
output: html_document
---
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Here is an example of using the Readme automated content analysis package in R.  Our goal is to take a set of survey responses to a question and categorize each of them into one of two responses titled 1 and 2.  The first step is to load, install, and library all of the necessary packages.
```{r}
library(devtools)
install_github("iqss-research/VA-package")
install_github("iqss-research/ReadMeV1")
library(ReadMe)
```
Here I am selecting a random subset that will be hand coded.
```{r}
setwd("~/Desktop/QualData")
rbbcsc = read.csv("RBBCSCStaffSurvey.csv", header = TRUE)
rbbcsc = as.data.frame(rbbcsc)
mccsc = read.csv("MCCSCStaffSurvey.csv", header = TRUE)

mccsc2 = mccsc[c("Q2", "Q3")]
mccsc2 = mccsc2[-c(1:2), ]
mccsc2 = as.matrix(mccsc2)


rbbcsc1 = rbbcsc[c("Q2", "Q3")]
rbbcsc2 = rbbcsc1[-c(1:2), ]
rbbcsc2 = as.matrix(rbbcsc2)


both = rbind(mccsc2, rbbcsc2)
dim(both)

both = rbind(mccsc2, rbbcsc2)
write.csv(both, "both.csv")
both = read.csv("both.csv", header= TRUE, na.strings = c("", "NA"))
both = na.omit(both)
id = 1:nrow(both)
both = cbind(id, both)
head(both)
both = both[c(1,3:4)]
set.seed(123)
dim(both)
both$random = rnorm(386)
both = as.data.frame(both)
both$random

library(rlist)
library(pipeR)
people <- list.load("http://renkun.me/rlist-tutorial/data/sample.json")
list.order(both$random)

write.csv(both, "AutoFull.csv", row.names = FALSE)
```
