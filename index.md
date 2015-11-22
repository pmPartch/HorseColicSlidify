---
title       : Horse Colic Severity Predictor
subtitle    : Help the experienced horse owner with colic diagnosis
author      : Peter Partch
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Overview

Using the Horse Colic data set available from UCI Machine Learning Repository. The traning data set is comprised of:

1. 300 observations
2. 27 features
3. about 30% missing data (including one observation without an output)
4. several of the features that can only be done via medical personnel
5. only 6 observations are complete (therefore we need to deal with missing data in some way)


--- .class #id 

## Data Cleanup

The data was cleaned and modified as follows:

1. removed features that cannot be done by an average horse owner
2. removed features that lack > 50% of the observations
3. fill in missing observations (using nominal values or, in some cases, mean values)

--- .class #id 

## Supervised Learning

Use randomForest as a learning algorithm with a reduced feature set that includes the following:

* age (a binary value of adult or young)
* rectal temperature (you will need a rectal thermometer for this one and  good luck)
* pulse (measured off the neck or jaw)
* respiratory rate
* temperature of extrmities (a judgement, not a measure)
* peripheral pulse
* mucous membranes (look in the mouth)
* capillary refill time (depress a bit of the gum and measure how fast it recovers to pink)
* pain 
* Peristalsis (gut actifity...place your ear on the flank and listen)
* abdominal distension (this is an important measure)

--- .class #id 

## Processing

Here is a bit of the processing done to produce the model (I need some R code for the assignment)

```r
filename <- "horse-colic.data"
if (file.exists(filename)==FALSE)
{
    fileurl <- "https://archive.ics.uci.edu/ml/machine-learning-databases/horse-colic/horse-colic.data"
    download.file(fileurl,filename,method='curl')
}
```
The data is cleaned and then modeled using random forest (too much to show, so I'll hide that code). The confusion matrix follows (using all three output classes: lived, died, euthanized:

```
##     1  2 3 class.error
## 1 153 16 9   0.1404494
## 2  33 36 8   0.5324675
## 3  26 15 3   0.9318182
```

```
## Error in predict(modelFit8, colicMin): object 'modelFit8' not found
```

```
## Error in eval(expr, envir, enclos): object 'pred' not found
```

```
## Error in eval(expr, envir, enclos): object 'colicTestRaw' not found
```

```
## Error in sprintf("V%d", 1:dim(colicTest)[2]): object 'colicTest' not found
```

```
## Error in eval(expr, envir, enclos): object 'colicTest' not found
```

```
## Error in lapply(X = X, FUN = FUN, ...): object 'colicTest' not found
```

```
## Error in names(colicTest) <- newnames: object 'colicTest' not found
```

```
## Error in mean(colicTest$rect_temp, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$pulse, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$resp_rate, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$extm_temp, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$periph_pulse, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$muc_memb, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$cap_refil, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$pain, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$peristalsis, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in mean(colicTest$abd_dist, na.rm = TRUE): object 'colicTest' not found
```

```
## Error in colicTest[is.na(colicTest)] <- 0: object 'colicTest' not found
```

```
## Error in eval(expr, envir, enclos): object 'colicTest' not found
```

--- .class #id 

## Results

Examination of the resulting model and testing with the training and test set shows that the model was over fitted. Due to limitations on time (and this class really was to show Slidify, Kniter, HTML, and Shiny knowledge) I decided to not spend too much time on the modeling issues.


