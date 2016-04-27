# Predicting flight delays - Ruby Meetup
Brigitte  
April 27, 2016  


```r
set.seed(100)
setwd("~/GitHub/Ruby_Talk_Material")
library(caret)
```

```
## Warning: package 'caret' was built under R version 3.2.5
## Loading required package: lattice
## Loading required package: ggplot2
```

```r
trainData <- read.csv('train.csv',sep=',', header=TRUE)
testData <- read.csv('test.csv',sep=',', header=TRUE)

trainData$ARR_DEL15 <- as.factor(trainData$ARR_DEL15)
testData$ARR_DEL15 <- as.factor(testData$ARR_DEL15)
trainData$DAY_OF_WEEK <- as.factor(trainData$DAY_OF_WEEK)
testData$DAY_OF_WEEK <- as.factor(testData$DAY_OF_WEEK)
trainData$X <- NULL
testData$X <- NULL
```



Now we train the model. Use a rather simple algorith first to do the classification. Then if performence not that good, go to ensemble algorithms which are usually better. Even better would be to select more important variables from the data, include additional predictor variables, or do feature-engineering.

Choose Logistic regression to start with. Basically a regression that predicts a binary value. 

```r
library(caret)
logisticRegModel <- train(ARR_DEL15 ~ ., data=trainData, method = 'glm', family = 'binomial') #the dot here stands for 'all available variables, i.e. all columns', glm is generalized linear regression, we want logistic regression, i.e. set family to binomial
```

Now we can use the model and the test data to check how well we predict flight arrival delays.


```r
logRegPrediction <- predict(logisticRegModel, testData)
logRegConfMat <- confusionMatrix(logRegPrediction, testData[,"ARR_DEL15"])
logRegConfMat
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    0    1
##          0 7465 2273
##          1   65   94
##                                           
##                Accuracy : 0.7638          
##                  95% CI : (0.7553, 0.7721)
##     No Information Rate : 0.7608          
##     P-Value [Acc > NIR] : 0.2513          
##                                           
##                   Kappa : 0.0457          
##  Mcnemar's Test P-Value : <2e-16          
##                                           
##             Sensitivity : 0.99137         
##             Specificity : 0.03971         
##          Pos Pred Value : 0.76658         
##          Neg Pred Value : 0.59119         
##              Prevalence : 0.76084         
##          Detection Rate : 0.75427         
##    Detection Prevalence : 0.98393         
##       Balanced Accuracy : 0.51554         
##                                           
##        'Positive' Class : 0               
## 
```

####Specificity is really low! Improve model.

See what s available with names(getModelInfo()) and then try boosted tree model gbm:
see http://topepo.github.io/caret/training.html


```r
fitControl <- trainControl(method = 'repeatedcv', number = 10, repeats = 10)
gbmFit1 <- train(ARR_DEL15 ~ ., data=trainData, method = 'gbm',trControl = fitControl,verbose = FALSE)
```

```
## Loading required package: gbm

```

```r
gbmPrediction <- predict(gbmFit1, testData)
gbmConfMat <- confusionMatrix(gbmPrediction, testData[,"ARR_DEL15"])
gbmConfMat
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction    0    1
##          0 7449 2197
##          1   81  170
##                                           
##                Accuracy : 0.7698          
##                  95% CI : (0.7614, 0.7781)
##     No Information Rate : 0.7608          
##     P-Value [Acc > NIR] : 0.0182          
##                                           
##                   Kappa : 0.088           
##  Mcnemar's Test P-Value : <2e-16          
##                                           
##             Sensitivity : 0.98924         
##             Specificity : 0.07182         
##          Pos Pred Value : 0.77224         
##          Neg Pred Value : 0.67729         
##              Prevalence : 0.76084         
##          Detection Rate : 0.75265         
##    Detection Prevalence : 0.97464         
##       Balanced Accuracy : 0.53053         
##                                           
##        'Positive' Class : 0               
## 
```

The specificity increased a tiny bit. Need to do more! What about weather, would that be a good predictor for flight delays?


