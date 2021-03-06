# Dplyr
Davide Romano  

#DataCamp notes



Load `dplyr` package and dataset `hflights`.


```r
library(dplyr)
library(hflights)
```

Convert data.frame into a tbl.


```r
hflights <- tbl_df(hflights)
hflights
```

```
## # A tibble: 227,496 × 21
##     Year Month DayofMonth DayOfWeek DepTime ArrTime UniqueCarrier
## *  <int> <int>      <int>     <int>   <int>   <int>         <chr>
## 1   2011     1          1         6    1400    1500            AA
## 2   2011     1          2         7    1401    1501            AA
## 3   2011     1          3         1    1352    1502            AA
## 4   2011     1          4         2    1403    1513            AA
## 5   2011     1          5         3    1405    1507            AA
## 6   2011     1          6         4    1359    1503            AA
## 7   2011     1          7         5    1359    1509            AA
## 8   2011     1          8         6    1355    1454            AA
## 9   2011     1          9         7    1443    1554            AA
## 10  2011     1         10         1    1443    1553            AA
## # ... with 227,486 more rows, and 14 more variables: FlightNum <int>,
## #   TailNum <chr>, ActualElapsedTime <int>, AirTime <int>, ArrDelay <int>,
## #   DepDelay <int>, Origin <chr>, Dest <chr>, Distance <int>,
## #   TaxiIn <int>, TaxiOut <int>, Cancelled <int>, CancellationCode <chr>,
## #   Diverted <int>
```

`Glimpse()` on tbl is similar to `str()`.


```r
glimpse(hflights)
```

```
## Observations: 227,496
## Variables: 21
## $ Year              <int> 2011, 2011, 2011, 2011, 2011, 2011, 2011, 20...
## $ Month             <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,...
## $ DayofMonth        <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 1...
## $ DayOfWeek         <int> 6, 7, 1, 2, 3, 4, 5, 6, 7, 1, 2, 3, 4, 5, 6,...
## $ DepTime           <int> 1400, 1401, 1352, 1403, 1405, 1359, 1359, 13...
## $ ArrTime           <int> 1500, 1501, 1502, 1513, 1507, 1503, 1509, 14...
## $ UniqueCarrier     <chr> "AA", "AA", "AA", "AA", "AA", "AA", "AA", "A...
## $ FlightNum         <int> 428, 428, 428, 428, 428, 428, 428, 428, 428,...
## $ TailNum           <chr> "N576AA", "N557AA", "N541AA", "N403AA", "N49...
## $ ActualElapsedTime <int> 60, 60, 70, 70, 62, 64, 70, 59, 71, 70, 70, ...
## $ AirTime           <int> 40, 45, 48, 39, 44, 45, 43, 40, 41, 45, 42, ...
## $ ArrDelay          <int> -10, -9, -8, 3, -3, -7, -1, -16, 44, 43, 29,...
## $ DepDelay          <int> 0, 1, -8, 3, 5, -1, -1, -5, 43, 43, 29, 19, ...
## $ Origin            <chr> "IAH", "IAH", "IAH", "IAH", "IAH", "IAH", "I...
## $ Dest              <chr> "DFW", "DFW", "DFW", "DFW", "DFW", "DFW", "D...
## $ Distance          <int> 224, 224, 224, 224, 224, 224, 224, 224, 224,...
## $ TaxiIn            <int> 7, 6, 5, 9, 9, 6, 12, 7, 8, 6, 8, 4, 6, 5, 6...
## $ TaxiOut           <int> 13, 9, 17, 22, 9, 13, 15, 12, 22, 19, 20, 11...
## $ Cancelled         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,...
## $ CancellationCode  <chr> "", "", "", "", "", "", "", "", "", "", "", ...
## $ Diverted          <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,...
```

The `dplyr` package contains five key data manipulation functions:

* `select()` return a subset of the columns
* `filter()` return a subset of the rows
* `arrange()` reorders the rows according to single or multiple variables
* `mutate()` add columns from existing data
* `summarise()` reduces each group to a single row by calculating aggregate 

###`select()`

Example of `select()` function.


```r
select(hflights,ActualElapsedTime, AirTime, ArrDelay, DepDelay)
```

```
## # A tibble: 227,496 × 4
##    ActualElapsedTime AirTime ArrDelay DepDelay
## *              <int>   <int>    <int>    <int>
## 1                 60      40      -10        0
## 2                 60      45       -9        1
## 3                 70      48       -8       -8
## 4                 70      39        3        3
## 5                 62      44       -3        5
## 6                 64      45       -7       -1
## 7                 70      43       -1       -1
## 8                 59      40      -16       -5
## 9                 71      41       44       43
## 10                70      45       43       43
## # ... with 227,486 more rows
```

Helper functions that can help to select groups:

* `starts_with("X")`
* `ends_with("X")`
* `contains("X")`
* `matches("X")`
* `num_range("x", 1:5)`
* `one_of(x)`

###`mutate()`

Example of `mutate()` function.


```r
mutate(hflights, ActualGroundTime = ActualElapsedTime - AirTime)
```

```
## # A tibble: 227,496 × 22
##     Year Month DayofMonth DayOfWeek DepTime ArrTime UniqueCarrier
##    <int> <int>      <int>     <int>   <int>   <int>         <chr>
## 1   2011     1          1         6    1400    1500            AA
## 2   2011     1          2         7    1401    1501            AA
## 3   2011     1          3         1    1352    1502            AA
## 4   2011     1          4         2    1403    1513            AA
## 5   2011     1          5         3    1405    1507            AA
## 6   2011     1          6         4    1359    1503            AA
## 7   2011     1          7         5    1359    1509            AA
## 8   2011     1          8         6    1355    1454            AA
## 9   2011     1          9         7    1443    1554            AA
## 10  2011     1         10         1    1443    1553            AA
## # ... with 227,486 more rows, and 15 more variables: FlightNum <int>,
## #   TailNum <chr>, ActualElapsedTime <int>, AirTime <int>, ArrDelay <int>,
## #   DepDelay <int>, Origin <chr>, Dest <chr>, Distance <int>,
## #   TaxiIn <int>, TaxiOut <int>, Cancelled <int>, CancellationCode <chr>,
## #   Diverted <int>, ActualGroundTime <int>
```

###`filter()`

Example of `filter()` function.


```r
filter(hflights,Distance > 1000)
```

```
## # A tibble: 65,389 × 21
##     Year Month DayofMonth DayOfWeek DepTime ArrTime UniqueCarrier
##    <int> <int>      <int>     <int>   <int>   <int>         <chr>
## 1   2011     1          1         6    1824    2106            AS
## 2   2011     1          2         7    1823    2103            AS
## 3   2011     1          3         1    1827    2107            AS
## 4   2011     1          4         2    1845    2132            AS
## 5   2011     1          5         3    1821    2109            AS
## 6   2011     1          6         4    1834    2133            AS
## 7   2011     1          7         5    1823    2118            AS
## 8   2011     1          8         6    1822    2112            AS
## 9   2011     1          9         7    1938    2228            AS
## 10  2011     1         10         1    1820    2159            AS
## # ... with 65,379 more rows, and 14 more variables: FlightNum <int>,
## #   TailNum <chr>, ActualElapsedTime <int>, AirTime <int>, ArrDelay <int>,
## #   DepDelay <int>, Origin <chr>, Dest <chr>, Distance <int>,
## #   TaxiIn <int>, TaxiOut <int>, Cancelled <int>, CancellationCode <chr>,
## #   Diverted <int>
```

###`arrange()`

Example of `arrange()` function.


```r
head(arrange(hflights,DepDelay))
```

```
## # A tibble: 6 × 21
##    Year Month DayofMonth DayOfWeek DepTime ArrTime UniqueCarrier FlightNum
##   <int> <int>      <int>     <int>   <int>   <int>         <chr>     <int>
## 1  2011    12         24         6    1112    1314            OO      5440
## 2  2011     2         14         1    1917    2027            MQ      3328
## 3  2011     4         10         7    2101    2206            XE      2669
## 4  2011     8          3         3    1741    1810            XE      2603
## 5  2011     1         18         2    1542    1936            CO      1688
## 6  2011    10          4         2    1438    1813            EV      5412
## # ... with 13 more variables: TailNum <chr>, ActualElapsedTime <int>,
## #   AirTime <int>, ArrDelay <int>, DepDelay <int>, Origin <chr>,
## #   Dest <chr>, Distance <int>, TaxiIn <int>, TaxiOut <int>,
## #   Cancelled <int>, CancellationCode <chr>, Diverted <int>
```

###`summarise()`

Example of `summarise()` function.


```r
summarise(hflights, min_dist = min(Distance),max_dist = max(Distance))
```

```
## # A tibble: 1 × 2
##   min_dist max_dist
##      <int>    <int>
## 1       79     3904
```

R contains many aggregating functions, as `dplyr` calls them:

* `min(x)` - minimum value of vector x.
* `max(x)` - maximum value of vector x.
* `mean(x)` - mean value of vector x.
* `median(x)` - median value of vector x.
* `quantile(x, p)` - pth quantile of vector x.
* `sd(x)` - standard deviation of vector x.
* `var(x)` - variance of vector x.
* `IQR(x)` - Inter Quartile Range (IQR) of vector x.
* `diff(range(x))` - total range of vector x.

An example to summarise the longest `Distance` for `diverted` flights.


```r
summarise(filter(hflights, Diverted==1), max_div=max(Distance))
```

```
## # A tibble: 1 × 1
##   max_div
##     <int>
## 1    3904
```

`dplyr` provides several helpful aggregate functions:

* `first(x)` - The first element of vector x.
* `last(x)` - The last element of vector x.
* `nth(x, n)` - The nth element of vector x.
* `n()` - The number of rows in the data.frame or group of observations that summarise() describes.
* `n_distinct(x)` - The number of unique values in vector x.
* `sum()`
* `mean()`

Example:


```r
summarise(hflights, n_obs = n(), n_carrier = n_distinct(UniqueCarrier), n_dest = n_distinct(Dest))
```

```
## # A tibble: 1 × 3
##    n_obs n_carrier n_dest
##    <int>     <int>  <int>
## 1 227496        15    116
```

<br>

##Pipes `%>%`

The following two commands that are completely equivalent:


```r
mean(c(1, 2, 3, NA), na.rm = TRUE)
```

```
## [1] 2
```

```r
c(1, 2, 3, NA) %>% mean(na.rm = TRUE)
```

```
## [1] 2
```

<br>

##`group_by()`

`group_by()` lets you define groups within your data set.


```r
hflights %>%
  group_by(UniqueCarrier) %>%
  summarise(p_canc = mean(Cancelled == 1) * 100) %>%
  arrange(p_canc)
```

```
## # A tibble: 15 × 2
##    UniqueCarrier    p_canc
##            <chr>     <dbl>
## 1             AS 0.0000000
## 2             CO 0.6782614
## 3             F9 0.7159905
## 4             FL 0.9817672
## 5             US 1.1268986
## 6             YV 1.2658228
## 7             OO 1.3946828
## 8             XE 1.5495599
## 9             WN 1.5504047
## 10            DL 1.5903067
## 11            UA 1.6409266
## 12            AA 1.8495684
## 13            B6 2.5899281
## 14            MQ 2.9044750
## 15            EV 3.4482759
```
