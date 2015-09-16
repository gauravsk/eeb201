---
title: "Lloyd Smith exercises"
author: "Gaurav Kandlikar"
date: "September 16, 2015"
output: html_document
---

### Mini exercise 3.2.1

Tweaking parameters of discrete growth model


```r
# conditions & parameters (these are new!)
generations <- 200
RR <- 1.001 # R is a parameter
N_init <- 100 # N is a state variable

# create and populate pop size vector
pop_sizes <- numeric(generations)
pop_sizes[1] <- N_init
for (time in 2:generations){
  pop_sizes[time] <- RR*pop_sizes[time-1]
}

pop_sizes
```

```
##   [1] 100.0000 100.1000 100.2001 100.3003 100.4006 100.5010 100.6015
##   [8] 100.7021 100.8028 100.9036 101.0045 101.1055 101.2066 101.3078
##  [15] 101.4091 101.5105 101.6121 101.7137 101.8154 101.9172 102.0191
##  [22] 102.1211 102.2233 102.3255 102.4278 102.5302 102.6328 102.7354
##  [29] 102.8381 102.9410 103.0439 103.1470 103.2501 103.3533 103.4567
##  [36] 103.5602 103.6637 103.7674 103.8712 103.9750 104.0790 104.1831
##  [43] 104.2873 104.3915 104.4959 104.6004 104.7050 104.8097 104.9145
##  [50] 105.0195 105.1245 105.2296 105.3348 105.4402 105.5456 105.6512
##  [57] 105.7568 105.8626 105.9684 106.0744 106.1805 106.2867 106.3929
##  [64] 106.4993 106.6058 106.7124 106.8191 106.9260 107.0329 107.1399
##  [71] 107.2471 107.3543 107.4617 107.5691 107.6767 107.7844 107.8922
##  [78] 108.0001 108.1081 108.2162 108.3244 108.4327 108.5411 108.6497
##  [85] 108.7583 108.8671 108.9759 109.0849 109.1940 109.3032 109.4125
##  [92] 109.5219 109.6314 109.7411 109.8508 109.9607 110.0706 110.1807
##  [99] 110.2909 110.4012 110.5116 110.6221 110.7327 110.8434 110.9543
## [106] 111.0652 111.1763 111.2875 111.3988 111.5102 111.6217 111.7333
## [113] 111.8450 111.9569 112.0688 112.1809 112.2931 112.4054 112.5178
## [120] 112.6303 112.7429 112.8557 112.9685 113.0815 113.1946 113.3078
## [127] 113.4211 113.5345 113.6480 113.7617 113.8754 113.9893 114.1033
## [134] 114.2174 114.3316 114.4460 114.5604 114.6750 114.7896 114.9044
## [141] 115.0193 115.1344 115.2495 115.3647 115.4801 115.5956 115.7112
## [148] 115.8269 115.9427 116.0587 116.1747 116.2909 116.4072 116.5236
## [155] 116.6401 116.7568 116.8735 116.9904 117.1074 117.2245 117.3417
## [162] 117.4590 117.5765 117.6941 117.8118 117.9296 118.0475 118.1656
## [169] 118.2837 118.4020 118.5204 118.6389 118.7576 118.8763 118.9952
## [176] 119.1142 119.2333 119.3526 119.4719 119.5914 119.7110 119.8307
## [183] 119.9505 120.0705 120.1905 120.3107 120.4310 120.5515 120.6720
## [190] 120.7927 120.9135 121.0344 121.1554 121.2766 121.3979 121.5193
## [197] 121.6408 121.7624 121.8842 122.0061
```

```r
# My favourite plot:
plot(x = 1:generations, y = pop_sizes, type = "l", lwd = 2,
     xlab = "generations", main = paste("R = ", RR))
```

![plot of chunk unnamed-chunk-1](figure/unnamed-chunk-1-1.png) 

### Exercise 3.2.2
Convert the model to a function


```r
# The function
geom_pop_growth <- function(N, RR, generations = 20) {
  pop_sizes <- numeric(generations)
  pop_sizes[1] <- N_init
  for (time in 2:generations){
    pop_sizes[time] <- RR*pop_sizes[time-1]
  }
  plot(y = pop_sizes, x = 1:generations, type = "l", lwd = 2)
  return(pop_sizes)
}

# Run the function 
geom_pop_growth(N = 100, RR = 1.1)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png) 

```
##  [1] 100.0000 110.0000 121.0000 133.1000 146.4100 161.0510 177.1561
##  [8] 194.8717 214.3589 235.7948 259.3742 285.3117 313.8428 345.2271
## [15] 379.7498 417.7248 459.4973 505.4470 555.9917 611.5909
```


### Exercise 3.3
Logistic growth (includes carrying capacity)


```r
# parameters
# conditions & parameters (these are new!)
generations <- 200
rr <- .1 # R is a parameter
N_init <- 100 # N is a state variable
K <- 1000 # Carrying capacity - a parameter

# create and populate pop size vector
pop_sizes <- numeric(generations)
pop_sizes[1] <- N_init
for (time in 2:generations){
  pop_sizes[time] <- pop_sizes[time-1]*(1+rr*(1-pop_sizes[time-1]/K))
}
plot(y = pop_sizes, x = 1:generations, type = "l", lwd = 2)
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png) 

### 3.3.1
Convert above logistic growth to a function


```r
# The function

logistic_pop_growth <- function(N, rr, generations = 20, K) {
  pop_sizes <- numeric(generations)
  pop_sizes[1] <- N_init
  for (time in 2:generations){
    pop_sizes[time] <- pop_sizes[time-1]*(1+rr*(1-pop_sizes[time-1]/K))
  }
  plot(y = pop_sizes, x = 1:generations, type = "l", lwd = 2)
  
}

# Run the function
logistic_pop_growth(N = 100, rr = 0.1, K = 1000)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png) 

### Exercises 3.3.3

Do a systematic exploration of parameter space


```r
rrs <- c(-0.3, 0.3, 1.3, 1.9, 2.2, 2.7)
```
