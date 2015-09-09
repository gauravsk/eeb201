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
