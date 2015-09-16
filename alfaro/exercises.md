---
title: "Script from Alfaro's section of R bootcamp"
author: "Gaurav Kandlikar"
output: html_document
---

Date of last knit: Wed Sep 16 12:05:43 2015

Tinkering around:

```r
source("../source.example.R")

# Run the function
all.I.know.about.life.I.learned.in.grad.school()
```

```
## Don't turn away free food.
```

```r
# Rename the function

some_name() <- all.I.know.about.life.I.learned.in.grad.school()
```

```
## Why would I want to go to med school when I can have all this stress with less career certainty?
```

```
## Error in some_name() <- all.I.know.about.life.I.learned.in.grad.school(): invalid (NULL) left side of assignment
```

### Playing with phylo trees

```r
library(ape)
tt <- read.tree("../tree.tre")

# explore what is in tt
head(tt$tip.label); attributes(tt); str(tt)
```

```
## [1] "Polyodon_spathula"           "Psephurus_gladius"          
## [3] "Scaphirhynchus_albus"        "Scaphirhynchus_platorynchus"
## [5] "Scaphirhynchus_suttkusi"     "Huso_huso"
```

```
## $names
## [1] "edge"        "Nnode"       "tip.label"   "edge.length" "node.label" 
## [6] "root.edge"  
## 
## $class
## [1] "phylo"
## 
## $order
## [1] "cladewise"
```

```
## List of 6
##  $ edge       : int [1:15924, 1:2] 7964 7965 7966 7966 7965 7967 7968 7969 7970 7970 ...
##  $ Nnode      : int 7962
##  $ tip.label  : chr [1:7963] "Polyodon_spathula" "Psephurus_gladius" "Scaphirhynchus_albus" "Scaphirhynchus_platorynchus" ...
##  $ edge.length: num [1:15924] 325.95 12.01 7.04 7.04 8.08 ...
##  $ node.label : chr [1:7962] "Actinopteri" "" "" "" ...
##  $ root.edge  : num 0
##  - attr(*, "class")= chr "phylo"
##  - attr(*, "order")= chr "cladewise"
```

```r
# import in a table with some data about tips
dd <- read.table("../data.txt", as.is = T, sep = "\t", header = T)
str(dd); head(dd) # Apparently there's NAs
```

```
## 'data.frame':	92 obs. of  2 variables:
##  $ species: chr  "Naso_brevirostris" "glass_fish" "Zebrasoma_scopas" "Apogon_nigrofasciatus" ...
##  $ mode   : chr  "BCF" NA "BCF" "BCF" ...
```

```
##                          species mode
## 1              Naso_brevirostris  BCF
## 2                     glass_fish <NA>
## 3               Zebrasoma_scopas  BCF
## 4          Apogon_nigrofasciatus  BCF
## 5        Cheilodipterus_macrodon  BCF
## 6 Cheilodipterus_quinquelineatus  BCF
```

```r
unique(dd$mode)
```

```
## [1] "BCF" NA    "MPF"
```

```r
# generate some random data and add it into a new col
dd$size <- runif(n = nrow(dd))
# if we just want it temporarily, just call cbind()

# Using which() to select certain rows

which(dd$mode == "MPF") # returns row numbers - which() just gives cells for which a value is TRUE
```

```
##  [1] 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56
## [24] 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71 72 73 74 75 76 77 78 79
## [47] 80 81 82 83 84 85 86 87 88 89 90 91 92
```

```r
# Make a vector of species with MPF
head(dd$species[which(dd$mode == "MPF")])
```

```
## [1] "Acanthurus_blochii"     "Acanthurus_dussumieri" 
## [3] "Acanthurus_lineatus"    "Acanthurus_nigrofuscus"
## [5] "Acanthurus_olivaceus"   "Acanthurus_triostegus"
```

```r
# Make a df with just the MPF swimmers
head(dd[which(dd$mode == "MPF"), ])
```

```
##                   species mode       size
## 34     Acanthurus_blochii  MPF 0.91934125
## 35  Acanthurus_dussumieri  MPF 0.27029540
## 36    Acanthurus_lineatus  MPF 0.21489278
## 37 Acanthurus_nigrofuscus  MPF 0.09605554
## 38   Acanthurus_olivaceus  MPF 0.09203567
## 39  Acanthurus_triostegus  MPF 0.49511141
```


```r
# fun for loop
notfish <- c("bat", "dolphin")
for (animal in notfish){
  cat(animal, "fish\n", sep = "") # default sep is " "
}
```

```
## batfish
## dolphinfish
```

```r
# while loop
i <- 1
while(i < 5) {
  cat("The value of i right now is", i, "\n")
   i <- i+1
}
```

```
## The value of i right now is 1 
## The value of i right now is 2 
## The value of i right now is 3 
## The value of i right now is 4
```

```r
# conditionally break a while loop
i <- 1 
while (i < 5) {
  i <- i+1
  
  if (i == 3){
    break
  }
  
}
i # should be three, because that's when the loop is stopped
```

```
## [1] 3
```

```r
# if + else
i <- 1
while (i < 10) {
#   if (i %% 2 == 0) {
#     cat("The number", i, "is even\n")
#   } else {
#     cat("The number", i, "is odd\n")
#   }
  
  if (i == 7) {
    cat("    lucky number", i, "!\n")
  } else{
    cat("nobody cares about", i, " :(\n")
  }
  
  i <- i+1
}
```

```
## nobody cares about 1  :(
## nobody cares about 2  :(
## nobody cares about 3  :(
## nobody cares about 4  :(
## nobody cares about 5  :(
## nobody cares about 6  :(
##     lucky number 7 !
## nobody cares about 8  :(
## nobody cares about 9  :(
```

### Exercise 1
Write a for loop statements so that it runs from 1:9 and prints the following output to your screen:

```r
for(i in 1:9) {
  if (i < 9) {
    cat("\n")
  } else {
    cat("*")
  }
}
```

```
## 
## 
## 
## 
## 
## 
## 
## 
## *
```


### Exercise 2
Modify your for loop so that it prints 10 asterisks, with each asterisk separated by exactly one ampersand sign (&), with no spaces or new line characters.


```r
for(i in 1:9) {
  if (i < 9) {
    cat("*&")
  } else {
    cat("*&*")
  }
}
```

```
## *&*&*&*&*&*&*&*&*&*
```
