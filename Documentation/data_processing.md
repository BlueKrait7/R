

```r
library(xlsx)
```

```
## Error in library(xlsx): there is no package called 'xlsx'
```

```r
## Loading required package: rJava
## Loading required package: xlsxjars

setwd("/Users/chenfeiyang")
```

```
## Error in setwd("/Users/chenfeiyang"): cannot change working directory
```

```r
cameraData <- read.xlsx("./data/cameras.xlsx", sheetIndex = 1, header = TRUE)
```

```
## Error in read.xlsx("./data/cameras.xlsx", sheetIndex = 1, header = TRUE): could not find function "read.xlsx"
```

```r
cameraData <- read.xlsx("./data/cameras.xlsx", "Baltimore Fixed Speed Cameras", 
    header = TRUE)
```

```
## Error in read.xlsx("./data/cameras.xlsx", "Baltimore Fixed Speed Cameras", : could not find function "read.xlsx"
```

```r
head(cameraData)
```

```
## Error in head(cameraData): object 'cameraData' not found
```

```r
##                          address direction      street  crossStreet
## 1       S CATON AVE & BENSON AVE       N/B   Caton Ave   Benson Ave
## 2       S CATON AVE & BENSON AVE       S/B   Caton Ave   Benson Ave
## 3 WILKENS AVE & PINE HEIGHTS AVE       E/B Wilkens Ave Pine Heights
## 4        THE ALAMEDA & E 33RD ST       S/B The Alameda      33rd St
## 5        E 33RD ST & THE ALAMEDA       E/B      E 33rd  The Alameda
## 6        ERDMAN AVE & N MACON ST       E/B      Erdman     Macon St
##                 intersection                      Location.1
## 1     Caton Ave & Benson Ave (39.2693779962, -76.6688185297)
## 2     Caton Ave & Benson Ave (39.2693157898, -76.6689698176)
## 3 Wilkens Ave & Pine Heights  (39.2720252302, -76.676960806)
## 4     The Alameda  & 33rd St (39.3285013141, -76.5953545714)
## 5      E 33rd  & The Alameda (39.3283410623, -76.5953594625)
## 6         Erdman  & Macon St (39.3068045671, -76.5593167803)

# Read specific rows and columns in Excel
colIndex <- 2:3
rowIndex <- 1:4
cameraDataSubset <- read.xlsx("./data/cameras.xlsx", sheetIndex = 1, colIndex = colIndex, 
    rowIndex = rowIndex)
```

```
## Error in read.xlsx("./data/cameras.xlsx", sheetIndex = 1, colIndex = colIndex, : could not find function "read.xlsx"
```

```r
cameraDataSubset
```

```
## Error in eval(expr, envir, enclos): object 'cameraDataSubset' not found
```

```r
##   direction      street
## 1       N/B   Caton Ave
## 2       S/B   Caton Ave
## 3       E/B Wilkens Ave

# Subsetting - quick review
set.seed(13435)
X <- data.frame(var1 = sample(1:5), var2 = sample(6:10), var3 = sample(11:15))
X <- X[sample(1:5), ]
X$var2[c(1, 3)] = NA
X
```

```
##   var1 var2 var3
## 5    2   NA   11
## 4    4   10   12
## 1    3   NA   14
## 2    1    7   15
## 3    5    6   13
```

```r
##   var1 var2 var3
## 1    2   NA   15
## 4    1   10   11
## 2    3   NA   12
## 3    5    6   14
## 5    4    9   13

X[, 1]
```

```
## [1] 2 4 3 1 5
```

```r
## [1] 2 1 3 5 4
X[, "var1"]
```

```
## [1] 2 4 3 1 5
```

```r
## [1] 2 1 3 5 4
X[1:2, "var2"]
```

```
## [1] NA 10
```

```r
## [1] NA 10

# Logicals and: & , or: |
X[(X$var1 <= 3 & X$var3 > 11), ]
```

```
##   var1 var2 var3
## 1    3   NA   14
## 2    1    7   15
```

```r
##   var1 var2 var3
## 1    2   NA   15
## 2    3   NA   12
X[(X$var1 <= 3 | X$var3 > 15), ]
```

```
##   var1 var2 var3
## 5    2   NA   11
## 1    3   NA   14
## 2    1    7   15
```

```r
##   var1 var2 var3
## 1    2   NA   15
## 4    1   10   11
## 2    3   NA   12

## Dealing with missing values
X[which(X$var2 > 8), ]
```

```
##   var1 var2 var3
## 4    4   10   12
```

```r
##   var1 var2 var3
## 4    1   10   11
## 5    4    9   13

# Sorting
sort(X$var1)
```

```
## [1] 1 2 3 4 5
```

```r
## [1] 1 2 3 4 5
sort(X$var1, decreasing = TRUE)
```

```
## [1] 5 4 3 2 1
```

```r
## [1] 5 4 3 2 1
sort(X$var2, na.last = TRUE)
```

```
## [1]  6  7 10 NA NA
```

```r
## [1]  6  9 10 NA NA

# Ordering
X[order(X$var1), ]
```

```
##   var1 var2 var3
## 2    1    7   15
## 5    2   NA   11
## 1    3   NA   14
## 4    4   10   12
## 3    5    6   13
```

```r
##   var1 var2 var3
## 4    1   10   11
## 1    2   NA   15
## 2    3   NA   12
## 5    4    9   13
## 3    5    6   14

X[order(X$var1, X$var3), ]
```

```
##   var1 var2 var3
## 2    1    7   15
## 5    2   NA   11
## 1    3   NA   14
## 4    4   10   12
## 3    5    6   13
```

```r
##   var1 var2 var3
## 4    1   10   11
## 1    2   NA   15
## 2    3   NA   12
## 5    4    9   13
## 3    5    6   14

## Sort using the arrange function of the plyr package

library(plyr)
```

```
## Error in library(plyr): there is no package called 'plyr'
```

```r
arrange(X, var1)
```

```
## Error in arrange(X, var1): could not find function "arrange"
```

```r
##   var1 var2 var3
## 1    1   10   11
## 2    2   NA   15
## 3    3   NA   12
## 4    4    9   13
## 5    5    6   14

arrange(X, desc(var1))
```

```
## Error in arrange(X, desc(var1)): could not find function "arrange"
```

```r
##   var1 var2 var3
## 1    5    6   14
## 2    4    9   13
## 3    3   NA   12
## 4    2   NA   15
## 5    1   10   11

# Add row and column
X$var4 <- rnorm(5)
X
```

```
##   var1 var2 var3       var4
## 5    2   NA   11 -0.4150458
## 4    4   10   12  2.5437602
## 1    3   NA   14  1.5545298
## 2    1    7   15 -0.6192328
## 3    5    6   13 -0.9261035
```

```r
##   var1 var2 var3     var4
## 1    2   NA   15  0.18760
## 4    1   10   11  1.78698
## 2    3   NA   12  0.49669
## 3    5    6   14  0.06318
## 5    4    9   13 -0.53613

Y <- cbind(X, rnorm(5))
Y
```

```
##   var1 var2 var3       var4    rnorm(5)
## 5    2   NA   11 -0.4150458 -0.66549949
## 4    4   10   12  2.5437602 -0.02166735
## 1    3   NA   14  1.5545298 -0.17411953
## 2    1    7   15 -0.6192328  0.23900438
## 3    5    6   13 -0.9261035 -1.83245959
```

```r
##   var1 var2 var3     var4 rnorm(5)
## 1    2   NA   15  0.18760  0.62578
## 4    1   10   11  1.78698 -2.45084
## 2    3   NA   12  0.49669  0.08909
## 3    5    6   14  0.06318  0.47839
## 5    4    9   13 -0.53613  1.00053
```

