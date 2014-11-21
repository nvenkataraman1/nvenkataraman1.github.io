---
layout: post
title: "Logistic Regression Modeling"
author: "Naveen Venkataraman"
output: html_document
comments: True
permalink: logistic-regression-modeling
---

In this example, we will look at fitting models using logistic regression. Logistic regression is a good method of fitting when dealing with binary output variables i.e variables that have only 2 _levels_ and building a model which can predict the outcome based on a variable input. The output can be 0 or 1 if the variables are binary / numeric, but if your variables are categorical, R can treat the variable as a factor (you can use stringsAsFactors=T when reading in the data) and use their ```levels``` to work with, when fitting the model.

In this example, I am fitting a model on a dataset using cancer survival data from this study: https://archive.ics.uci.edu/ml/datasets/Haberman's+Survival.

Attribute Information:

1. Age of patient at time of operation (numerical)
2. Patient's year of operation (year - 1900, numerical)
3. Number of positive axillary nodes detected (numerical)
4. Survival status (class attribute)
    + 1 = the patient survived 5 years or longer
    + 2 = the patient died within 5 year
         
I have modified column 4 to set to 0 when the patient died within 5 years.

My goal is to establish whether there is a relationship between Number of positive axillary nodes detected and survival beyond 5 years.


```r
cancerdata_all <- read.csv("./data/data.csv",stringsAsFactors=F)
dim(cancerdata_all)
```

```
## [1] 306   4
```

Taking training data using first 200 samples and test data using last 106 samples.

```r
cancerdata_train <- cancerdata_all[1:200,]

cancerdata_test <- cancerdata_all[201:306,]

dim(cancerdata_train[cancerdata_train$survival==1,])
```

```
## [1] 144   4
```

```r
dim(cancerdata_train[cancerdata_train$survival==2,])
```

```
## [1] 56  4
```

```r
cancerdata_train[cancerdata_train$survival==2,4] <- 0

dim(cancerdata_train[cancerdata_train$survival==0,])
```

```
## [1] 56  4
```

```r
dim(cancerdata_train[cancerdata_train$survival==1,])
```

```
## [1] 144   4
```

```r
summary(cancerdata_train)
```

```
##       age             yrop          auxnodes         survival   
##  Min.   :30.00   Min.   :58.00   Min.   : 0.000   Min.   :0.00  
##  1st Qu.:41.00   1st Qu.:60.00   1st Qu.: 0.000   1st Qu.:0.00  
##  Median :47.00   Median :63.00   Median : 1.000   Median :1.00  
##  Mean   :46.12   Mean   :62.76   Mean   : 4.465   Mean   :0.72  
##  3rd Qu.:52.00   3rd Qu.:65.00   3rd Qu.: 6.000   3rd Qu.:1.00  
##  Max.   :57.00   Max.   :69.00   Max.   :52.000   Max.   :1.00
```

```r
plot(cancerdata_train[,3],cancerdata_train[,4],type="p",pch=19,xlab="Num of positive aux nodes",ylab="Survival beyond 5 years")
```

![plot of chunk unnamed-chunk-2](../images/unnamed-chunk-2-1.png) 

Calling ```glm``` on the data to estimate the logit model


```r
Survival.model <- glm(survival ~ auxnodes, data=cancerdata_train, family=binomial(link=logit))
summary(Survival.model)
```

```
## 
## Call:
## glm(formula = survival ~ auxnodes, family = binomial(link = logit), 
##     data = cancerdata_train)
## 
## Deviance Residuals: 
##     Min       1Q   Median       3Q      Max  
## -1.7745  -1.0378   0.6813   0.7319   2.2229  
## 
## Coefficients:
##             Estimate Std. Error z value Pr(>|z|)    
## (Intercept)  1.34234    0.20182   6.651 2.91e-11 ***
## auxnodes    -0.08097    0.02381  -3.401 0.000671 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 237.18  on 199  degrees of freedom
## Residual deviance: 223.03  on 198  degrees of freedom
## AIC: 227.03
## 
## Number of Fisher Scoring iterations: 4
```

The model parameters are as follows:
1. Slope = -0.08577 with p-value of 0.000671
2. Intercept = 1.41250 with p-value of 2.91e-11

This indicates that both parameters are statistically significant.

Now, we derive the probabilities of the outcomes using the fitted glm model and using it to predict the probabilities.


```r
probability <- predict(Survival.model, newdata=cancerdata_train,type="response")
combined <- cbind(cancerdata_train,probability)
```

Plotting predicted probabilities and num of aux nodes in the training sample

```r
plot(combined[,3],combined[,5],ylab="Probability of survival",xlab="Num of positive aux nodes")
```

![plot of chunk unnamed-chunk-5](../images/unnamed-chunk-5-1.png) 

Plotting probability of expected outcomes based on the number of positive aux nodes gives us a visual representation of the relationship between the two variables (num of aux nodes and survival beyond 5 years).


We can test our model by using the model fitted on the training samples and run it on the test samples.

#### Step 1: Predicting survival rate in the test sample


```r
test_probs <- cbind(cancerdata_test,predict(Survival.model, newdata=data.frame(auxnodes=cancerdata_test$auxnodes),type="response"))

plot(test_probs[,3],test_probs[,5],ylab="Probability of survival",xlab="Num of positive aux nodes")
```

![plot of chunk unnamed-chunk-6](../images/unnamed-chunk-6-1.png) 

We can see the plot of the predicted values, and based on our analysis, we can see that it matches our expectations.

#### Step 2: Predicting survival rates using random data input

Now, we can predict survival probability for a set of input values i.e What are the chances of survival beyond 5 years if a certain number of Auxillary nodes are detected in my test result.


```r
summary(cancerdata_train$auxnodes)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   0.000   0.000   1.000   4.465   6.000  52.000
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=0),type="response") ## 0 - 1st quartile
```

```
##         1 
## 0.7928742
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=1),type="response") ## median
```

```
##         1 
## 0.7792616
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=4),type="response") ## 3rd quartile
```

```
##         1 
## 0.7346722
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=10),type="response") ## 10
```

```
##         1 
## 0.6300984
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=25),type="response") ## between 3rd quartile to max
```

```
##         1 
## 0.3358352
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=40),type="response")## between 3rd quartile to max
```

```
##         1 
## 0.1305098
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=52),type="response")## max value in sample
```

```
##          1 
## 0.05375335
```

```r
predict(Survival.model, newdata=data.frame(auxnodes=60),type="response")## beyond sample max value
```

```
##          1 
## 0.02886441
```



The various predicted probabilities indicate a clear relationship with the number of aux nodes in the population. The higher the aux nodes, the lower the chances of survival beyond 5 years.
