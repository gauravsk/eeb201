---
title: "Appendix B from Primer of Ecology w/ R"
author: "Gaurav Kandlikar"
date: "September 6, 2015"
output: html_document
---

### Appendix B1
This section focuses on using R's help functions.

```r
### When you know a function name ----
?mean

# Equivalent:
help(mean)
?mean

### When you don't know a function name ----
help.search("mean") # Here, "mean" is just a keyword
apropos("mean") # Here, functions with "mean" in the name are shown
```

```
##  [1] "colMeans"      ".colMeans"     "kmeans"        "mean"         
##  [5] "mean.Date"     "mean.default"  "mean.difftime" "mean.POSIXct" 
##  [9] "mean.POSIXlt"  "rowMeans"      ".rowMeans"     "weighted.mean"
```

```r
### When you want to search in packages that might not yet be on the system
RSiteSearch("violin") # This opens in the browser.
```

```
## A search query has been submitted to http://search.r-project.org
## The results page should open in your browser shortly
```

### Appendix B2

This section works through assigning values to variables.

```r
a <- 2+3
a
```

```
## [1] 5
```

```r
# Use a as input to another variable
b <- a+a

# Use semicolon to make two calls on one line
a+b; b+b
```

```
## [1] 15
```

```
## [1] 20
```

### Appendix B3

#### Appendix B3.1
Vectors 


```r
# Creating a vector Y with some known values
Y <- c(8.3, 8.6, 10.7, 10.8, 11, 11, 11.1, 11.2,11.3, 11.4)

# Creating sequences of numbers
1:4
```

```
## [1] 1 2 3 4
```

```r
4:1
```

```
## [1] 4 3 2 1
```

```r
-1:3
```

```
## [1] -1  0  1  2  3
```

```r
-(1:3) # minus sign outside acts as a function
```

```
## [1] -1 -2 -3
```

```r
# Sequencing by non-integer increments
seq(from = 1, to = 3, by = 0.2)
```

```
##  [1] 1.0 1.2 1.4 1.6 1.8 2.0 2.2 2.4 2.6 2.8 3.0
```

```r
seq(1, 3, by = 0.2) # We can skip argument names
```

```
##  [1] 1.0 1.2 1.4 1.6 1.8 2.0 2.2 2.4 2.6 2.8 3.0
```

```r
seq(1, 3, length = 7) # If we just know how long a vector we need
```

```
## [1] 1.000000 1.333333 1.666667 2.000000 2.333333 2.666667 3.000000
```

```r
# Repeating sequences
rep(1, 3) # Repeat 1 three times
```

```
## [1] 1 1 1
```

```r
rep(1:3, 2) # Repeat 1:3 three times
```

```
## [1] 1 2 3 1 2 3
```

```r
rep(1:3, each = 2) # Repeat each number in 1:3 twice
```

```
## [1] 1 1 2 2 3 3
```


#### Appendix B3.2
Info about vectors

```r
# Recall Y:
Y
```

```
##  [1]  8.3  8.6 10.7 10.8 11.0 11.0 11.1 11.2 11.3 11.4
```

```r
sum(Y)
```

```
## [1] 105.4
```

```r
mean(Y)
```

```
## [1] 10.54
```

```r
max(Y)
```

```
## [1] 11.4
```

```r
length(Y)
```

```
## [1] 10
```

```r
summary(Y)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##    8.30   10.72   11.00   10.54   11.18   11.40
```

Vectors aren't always numeric

```r
Names <- c("Sarah", "Yunluan")
Names
```

```
## [1] "Sarah"   "Yunluan"
```

```r
b <- c(TRUE, FALSE)

# Find out what kind of a vector it is!
class(Y); class(b)
```

```
## [1] "numeric"
```

```
## [1] "logical"
```

Tests are vectorized:

```r
Y>10
```

```
##  [1] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
```

```r
Y > mean(Y)
```

```
##  [1] FALSE FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE
```

```r
Y == 11
```

```
##  [1] FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE
```

```r
Y != 11
```

```
##  [1]  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
```

```r
# We can use this to extract the data:
# Get all values of Y that are bigger than the mean of Y:
Y[Y > mean(Y)]
```

```
## [1] 10.7 10.8 11.0 11.0 11.1 11.2 11.3 11.4
```

Vector algebra

```r
a <- 1:3
b <- 4:6

# Play with two vectors of equal lengths
a + b
```

```
## [1] 5 7 9
```

```r
a * b
```

```
## [1]  4 10 18
```

```r
a/b
```

```
## [1] 0.25 0.40 0.50
```

```r
# Play with a vector and a scalar
a + 1
```

```
## [1] 2 3 4
```

```r
a * 2
```

```
## [1] 2 4 6
```

```r
1/a
```

```
## [1] 1.0000000 0.5000000 0.3333333
```

```r
# Play with two vectors of unequal lengths
a * 1:2 # Note the warning.... This is equivalent to `a * c(1, 2, 1)`
```

```
## Warning in a * 1:2: longer object length is not a multiple of shorter
## object length
```

```
## [1] 1 4 3
```

```r
1:4 * 1:2 # Note no warning here, even though it's 4 * 2.
```

```
## [1] 1 4 3 8
```
