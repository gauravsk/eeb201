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
# RSiteSearch("violin") # This opens in the browser -- commented for now...
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

#### Appendix B3.3
Extracting data and handling missing values
Two ways to extract data from vectors: 1) provide numeric index; 2) provide logical vector


```r
# Using numeric index
Y[1]
```

```
## [1] 8.3
```

```r
Y[1:3]
```

```
## [1]  8.3  8.6 10.7
```

```r
# Using logical vector
Y[Y > mean(Y)] # Recall that the inside is just a T/F vector
```

```
## [1] 10.7 10.8 11.0 11.0 11.1 11.2 11.3 11.4
```

Missing data is SRS BSNS!

```r
a <- c(5, 3, 6, NA)
a
```

```
## [1]  5  3  6 NA
```

```r
is.na(a)
```

```
## [1] FALSE FALSE FALSE  TRUE
```

```r
sum(a) # Throws an error since R doesn't know how to add NA
```

```
## [1] NA
```

```r
# Multiple ways to eliminate the NAs from vectors (if that's the goal)
a[!is.na(a)]
```

```
## [1] 5 3 6
```

```r
na.exclude(a)
```

```
## [1] 5 3 6
## attr(,"na.action")
## [1] 4
## attr(,"class")
## [1] "exclude"
```

```r
# Some functions can remove NAs on the fly...
mean(a) # Fail
```

```
## [1] NA
```

```r
mean(a, na.rm = T) # Success
```

```
## [1] 4.666667
```

#### Appendix B.3.4
Matrices! Two dimensions, all data are of the same type


```r
matrix(letters[1:4], ncol = 2)
```

```
##      [,1] [,2]
## [1,] "a"  "c" 
## [2,] "b"  "d"
```

```r
M <- matrix(1:4, nrow = 2); M # Notice that the numbers are filled in by column
```

```
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
```

```r
matrix(1:4, nrow = T, byrow = T) # To fill in by row
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    2    3    4
```

```r
# Making an identity matrix
I <- diag(1, nrow = 2)

# We can make inverse matrices of known matrices easily:

M_inv <- solve(M)
M %*% M_inv 
```

```
##      [,1] [,2]
## [1,]    1    0
## [2,]    0    1
```

Extracting data from matrices is the same... matrix[row, column]

```r
M [1, 2] # First row; second col
```

```
## [1] 3
```

```r
M [1, ]; M[1, 1:2] # Both are equivalent
```

```
## [1] 1 3
```

```
## [1] 1 3
```

Skipping "Simple Matrix Algebra" for now. 

#### Appendix B3.5
Data frames: two dimensionsal, like matrices, but can store multiple types of data, unlike matrices...


```r
dat <- data.frame(species = c("S.altissima", "S.rugosa", "E.graminifolia", "A. pilosus"), 
                  treatment = factor(c("Control","Water", "Control", "Water")),
                  height = c(1.1,0.8, 0.9, 1), 
                  width = c(1, 1.7, 0.6, 0.2))
dat
```

```
##          species treatment height width
## 1    S.altissima   Control    1.1   1.0
## 2       S.rugosa     Water    0.8   1.7
## 3 E.graminifolia   Control    0.9   0.6
## 4     A. pilosus     Water    1.0   0.2
```

```r
# Extracting data 
dat[2, ]
```

```
##    species treatment height width
## 2 S.rugosa     Water    0.8   1.7
```

```r
dat[, 2]
```

```
## [1] Control Water   Control Water  
## Levels: Control Water
```

```r
dat[3, 4]
```

```
## [1] 0.6
```

```r
# We can treat these as vectors...
dat[, 2] == "Water"
```

```
## [1] FALSE  TRUE FALSE  TRUE
```

```r
# Use this to subset dat to only water
dat[dat[,2] == "Water", ] # Or just use the subset()
```

```
##      species treatment height width
## 2   S.rugosa     Water    0.8   1.7
## 4 A. pilosus     Water    1.0   0.2
```

```r
# Data frames often have factors.
c("Control", "Medium", "High")
```

```
## [1] "Control" "Medium"  "High"
```

```r
rep(c("Control", "Medium", "High"), each = 3)
```

```
## [1] "Control" "Control" "Control" "Medium"  "Medium"  "Medium"  "High"   
## [8] "High"    "High"
```

```r
Treatment <- factor(rep(c("Control", "Medium", "High"), each = 3))
Treatment
```

```
## [1] Control Control Control Medium  Medium  Medium  High    High    High   
## Levels: Control High Medium
```

```r
# The levels are stored alphabetically (i.e 1 will be control):
levels(Treatment)
```

```
## [1] "Control" "High"    "Medium"
```

```r
stripchart(1:9 ~ Treatment)
```

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12-1.png) 

```r
# We can force levels to be different:
Treatment <- factor(rep(c("Control", "Medium", "High"), each = 3), 
                    levels = c("Control", "Medium", "High"))
stripchart(1:9 ~ Treatment)
```

![plot of chunk unnamed-chunk-12](figure/unnamed-chunk-12-2.png) 

#### Appendix B3.6
Lists are just globs of objects...


```r
my.list <- list(My.Y = Y, b = b, 
                Names, 
                Weed.data = dat,
                My.matrix = M, 
                my.no = 4)
my.list
```

```
## $My.Y
##  [1]  8.3  8.6 10.7 10.8 11.0 11.0 11.1 11.2 11.3 11.4
## 
## $b
## [1] 4 5 6
## 
## [[3]]
## [1] "Sarah"   "Yunluan"
## 
## $Weed.data
##          species treatment height width
## 1    S.altissima   Control    1.1   1.0
## 2       S.rugosa     Water    0.8   1.7
## 3 E.graminifolia   Control    0.9   0.6
## 4     A. pilosus     Water    1.0   0.2
## 
## $My.matrix
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
## 
## $my.no
## [1] 4
```

```r
# Multiple ways of getting objects out of lists:
my.list[["b"]]; my.list[[2]]; my.list$b
```

```
## [1] 4 5 6
```

```
## [1] 4 5 6
```

```
## [1] 4 5 6
```

```r
# We can extract specific components from the objects
my.list[["b"]][1]
```

```
## [1] 4
```

```r
# We can think of data frames as a list of vectors;
# This is what allows us to use the $ operator to extract data from dfs!
```
