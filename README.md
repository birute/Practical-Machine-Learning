Practical-Machine-Learning
==========================

Practical Machine Learning


Background

Using devices such as Jawbone Up, Nike FuelBand, and Fitbit it is now possible to collect a large amount of data about personal activity relatively inexpensively. These type of devices are part of the quantified self movement – a group of enthusiasts who take measurements about themselves regularly to improve their health, to find patterns in their behavior, or because they are tech geeks. One thing that people regularly do is quantify how much of a particular activity they do, but they rarely quantify how well they do it. In this project, your goal will be to use data from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. They were asked to perform barbell lifts correctly and incorrectly in 5 different ways. More information is available from the website here: http://groupware.les.inf.puc-rio.br/har (see the section on the Weight Lifting Exercise Dataset). 



Data 


The training data for this project are available here: 

https://d396qusza40orc.cloudfront.net/predmachlearn/pml-training.csv

The test data are available here: 

https://d396qusza40orc.cloudfront.net/predmachlearn/pml-testing.csv

The data for this project come from this source: http://groupware.les.inf.puc-rio.br/har. If you use the document you create for this class for any purpose please cite them as they have been very generous in allowing their data to be used for this kind of assignment. 


Course Project: Writeup
========================================================

# Reading data into R from source.

```{r}
# training set

tr <- read.table("F:/+Machine learning coursera/Practical_Machine_Learning_Assignment1/pml-training.csv", header=TRUE, sep=",")

# test set

ts <- read.table("F:/+Machine learning coursera/Practical_Machine_Learning_Assignment1/pml-testing.csv", header=TRUE, sep=",")
```





# Pre-procesing

```{r}
library(caret)

# removing outcome and string variables from dataset

trn<-tr[,c(-1,-2,-3,-4,-5,-160)]
nzv <- nearZeroVar(trn, freqCut = 95/5, uniqueCut = 10, saveMetrics = TRUE)

# find a Mean of percentUnique
summary(nzv)

# a list (names_pred) of non zero variance variables that satisfies nzv = FALSE and percentUnique > 3.89

predictors<-nzv[which(nzv$nzv=='FALSE'&nzv$percentUnique>3.89),]

names_pred<-data.frame(rownames(predictors))


```


