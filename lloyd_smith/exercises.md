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
generations <- 100
RR <- -0.9 # R is a parameter
N_init <- 100 # N is a state variable

# create and populate pop size vector
pop_sizes <- numeric(generations)
pop_sizes[1] <- N_init
for (time in 2:generations){
  pop_sizes[time] <- RR*pop_sizes[time-1]
}

head(pop_sizes)
```

```
## [1] 100.000 -90.000  81.000 -72.900  65.610 -59.049
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
  pop_sizes[1] <- N
  for (time in 2:generations){
    pop_sizes[time] <- pop_sizes[time-1]*(1+rr*(1-pop_sizes[time-1]/K))
  }
  
  plot(y = pop_sizes, x = 1:generations, type = "l", lwd = 2)
  return(pop_sizes)
}

# Run the function
logistic_pop_growth(N = 10, rr = 0.1, K = 100)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png) 

```
##  [1] 10.00000 10.90000 11.87119 12.91738 14.04226 15.24930 16.54169
##  [8] 17.92224 19.39325 20.95648 22.61295 24.36290 26.20564 28.13947
## [15] 30.16159 32.26803 34.45360 36.71191 39.03534 41.41512
```

### Exercises 3.3.2

Do a systematic exploration of parameter space


```r
rrs <- c(-0.3, 0.3, 1.3, 1.9, 2.2, 2.7)

par(mfrow = c(2,3))
for(rr in rrs) {
  logistic_pop_growth(N = 10, rr = rr, generations = 20, K = 100)
}
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png) 


### Exercise 3.3.3

Bifurcation plot


```r
rrs <- seq(from = -1, to = 3, length.out = 100)
generations <- 100
trajectories <- sapply(rrs, function(x) logistic_pop_growth(N = 10, K = 100, rr = x, generations = generations))
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-2.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-3.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-4.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-5.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-6.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-7.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-8.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-9.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-10.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-11.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-12.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-13.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-14.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-15.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-16.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-17.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-18.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-19.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-20.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-21.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-22.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-23.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-24.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-25.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-26.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-27.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-28.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-29.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-30.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-31.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-32.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-33.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-34.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-35.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-36.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-37.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-38.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-39.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-40.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-41.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-42.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-43.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-44.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-45.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-46.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-47.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-48.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-49.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-50.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-51.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-52.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-53.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-54.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-55.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-56.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-57.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-58.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-59.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-60.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-61.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-62.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-63.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-64.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-65.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-66.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-67.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-68.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-69.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-70.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-71.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-72.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-73.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-74.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-75.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-76.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-77.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-78.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-79.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-80.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-81.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-82.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-83.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-84.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-85.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-86.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-87.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-88.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-89.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-90.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-91.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-92.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-93.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-94.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-95.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-96.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-97.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-98.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-99.png) ![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-100.png) 

```r
# I think this is what a bifurcation plot is!
par(mfrow = c(1,1))
matplot(y = trajectories[generations, ], x = rrs, type = "l", lwd = 2,
        main = "Bifurcation plot?")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-101.png) 

```r
# Or maybe it's this, but so messy!
matplot(y = trajectories, x = rrs, type = "l", lwd = 0.5)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-102.png) 
