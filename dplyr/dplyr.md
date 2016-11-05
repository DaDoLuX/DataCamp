# Dplyr
Davide Romano  

##DataCamp notes



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

