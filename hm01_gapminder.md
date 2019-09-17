Assignment01-Exercise02
================

Exploring a dataset

``` r
#Finding a dataset of interest within the in-built R dataset collection
datasets::Titanic
```

    ## , , Age = Child, Survived = No
    ## 
    ##       Sex
    ## Class  Male Female
    ##   1st     0      0
    ##   2nd     0      0
    ##   3rd    35     17
    ##   Crew    0      0
    ## 
    ## , , Age = Adult, Survived = No
    ## 
    ##       Sex
    ## Class  Male Female
    ##   1st   118      4
    ##   2nd   154     13
    ##   3rd   387     89
    ##   Crew  670      3
    ## 
    ## , , Age = Child, Survived = Yes
    ## 
    ##       Sex
    ## Class  Male Female
    ##   1st     5      1
    ##   2nd    11     13
    ##   3rd    13     14
    ##   Crew    0      0
    ## 
    ## , , Age = Adult, Survived = Yes
    ## 
    ##       Sex
    ## Class  Male Female
    ##   1st    57    140
    ##   2nd    14     80
    ##   3rd    75     76
    ##   Crew  192     20

Using functions to explore the dataset

``` r
#Obtains the dimensions of the dataset
dim(Titanic)
```

    ## [1] 4 2 2 2

``` r
#Provide the number of rows & columns, respectively
nrow(Titanic)
```

    ## [1] 4

``` r
ncol(Titanic)
```

    ## [1] 2

``` r
#Returns the first part of the dataset
str(Titanic)
```

    ##  'table' num [1:4, 1:2, 1:2, 1:2] 0 0 35 0 0 0 17 0 118 154 ...
    ##  - attr(*, "dimnames")=List of 4
    ##   ..$ Class   : chr [1:4] "1st" "2nd" "3rd" "Crew"
    ##   ..$ Sex     : chr [1:2] "Male" "Female"
    ##   ..$ Age     : chr [1:2] "Child" "Adult"
    ##   ..$ Survived: chr [1:2] "No" "Yes"

``` r
#Provides result summaries
summary(Titanic)
```

    ## Number of cases in table: 2201 
    ## Number of factors: 4 
    ## Test for independence of all factors:
    ##  Chisq = 1637.4, df = 25, p-value = 0
    ##  Chi-squared approximation may be incorrect
