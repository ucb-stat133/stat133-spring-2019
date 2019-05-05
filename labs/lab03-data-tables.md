Lab 3: Data Frame Basics
================
Gaston Sanchez

> ### Learning Objectives
> 
>   - Importing Data Tables in R
>   - Default reading-table functions
>   - Basic manipulation of data frames

### General Instructions

  - Write your descriptions, explanations, and code in an `Rmd` (R
    markdown) file.
  - Name this file as `lab03-first-last.Rmd`, where `first` and `last`
    are your first and last names (e.g. `lab03-gaston-sanchez.Rmd`).
  - Knit your `Rmd` file as an html document (default option).
  - Submit your `Rmd` and `html` files to bCourses, in the corresponding
    lab assignment.

## Abalone Data Set

The data set for this lab is the **Abalone Data Set** that is part of
the [UCI Machine Learning
Repository](http://archive.ics.uci.edu/ml/datasets/Abalone)

The location of the data file
is:

<http://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.data>

The location of the data dictionary (description of the data)
is:

<http://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.names>

### Your Turn

Look at both the dataset file, and the file with its description, and
answer the following questions:

  - What’s the character delimiter?
  - Is there a row for column names?
  - Are there any missing values? If so, how are they codified?
  - What is the data type of each column?

-----

### Getting a Local Copy of the Data

One basic way to read this file in R is by passing the url location of
the file directly to any of the `read.table()`
functions:

``` r
url <- "http://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.data"
abalone <- read.table(url, sep = ",")
```

My suggestion when reading datasets from the Web, is to always try to
get a local copy of the data file in your machine (as long as you have
enough free space to save it in your computer). To do this, you can use
the function `download.file()` and specify the url address, and the name
of the file that will be created in your computer. For instance, to save
the abalone data file in **your working directory**, type the following
commands directly on the R console:

``` r
# do NOT include this code in your Rmd file
# download it to your working directory
origin <- 'http://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.data'
destination <- 'abalone.data'
download.file(origin, destination)
```

-----

## Basic Importing

Now that you have a local copy of the dataset, you can read it in R with
`read.table()` like so:

``` r
# reading data from your working directory
abalone <- read.table("abalone.data", sep = ",")
```

Keep in mind that the above command will work as long as the data file
is in your working directory. After reading in a data table, you may
want to start looking at its contents, usually taking a peek at a few
rows. This can be done with `head()` and/or with `tail()`:

``` r
# take a peek of first rows
head(abalone)

# take a peek of last rows
tail(abalone)
```

Likewsie, you may also want to examine how R has decided to take care of
the storage details (what data type is used for each column). Use the
function `str()` to check the structure of the data frame:

``` r
# check data frame's structure
str(abalone, vec.len = 1)
```

### Detailed information about the columns

So far we have been able to read the data file in R. But we are missing
a few things. First, we don’t have names for the columns. Second, it
would be nice if we could specify the data types of each column instead
of letting R guess how to handle each data type.

Look at the data description (see “Attribute information”) in the
following
link:

<http://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.names>

According to the description of the Abalone data set, we could assign
the following data types to each of the columns as:

| Name           | Data Type  |
| -------------- | ---------- |
| Sex            | character  |
| Length         | continuous |
| Diameter       | continuous |
| Height         | continuous |
| Whole weight   | continuous |
| Shucked weight | continuous |
| Viscera weight | continuous |
| Shell weight   | continuous |
| Rings          | integer    |

### Your Turn

  - Create a vector `column_names` for the name of each column. Use the
    variable names displayed in the section “7. Attributes Information”:
    
      - `Sex`
      - `Length`
      - `Diameter`
      - `Height`
      - `Whole`
      - `Shucked`
      - `Viscera`
      - `Shell`
      - `Rings`

  - Create another vector `column_types` with R data types (e.g.
    `character`, `real`, `integer`). Match the R data types with the
    suggested type in “7. Attributes Information” (nominal =
    `character`, continuous = `real`, integer = `integer`).

  - Optionally, you could also specify a type `"factor"` for the
    variable `sex` since this is supposed to be in nominal scale
    (i.e. it is a categorical variable). Also note that the variable
    `rings` is supposed to be integers, therefore we can choose an
    `integer` vector for this column.

  - Look at the documentation of the function `read.table()` and try to
    read the `abalone.data` table in R. Find out which arguments you
    need to specify so that you pass your vectors `column_names` and
    `column_types` to `read.table()`. Read in the data as `abalone`, and
    then check its structure with `str()`.

  - Now re-read `abalone.data` with the `read.csv()` function. Name this
    data as `abalone2`, and check its structure with `str()`.

  - How would you read just the first 10 lines in `abalone.data`? Name
    this data as `abalone10`, and check its structure with `str()`.

  - How would you skip the first 10 lines in `abalone.data`, in order to
    read the next 10 lines (lines 11-20)? Name this data as `abalone20`,
    and check its structure with `str()`.

  - Read the documentation of `read.table()` about the argument
    `colClasses`. What happens when you specify the data-type of one or
    more columns as `"NULL"`?

  - Use the following functions to start examining descriptive aspects
    about the `abalone` data frame:
    
      - `str()`
      - `summary()`
      - `head()` and `tail()`
      - `dim()`
      - `names()`
      - `colnames()`
      - `nrow()`
      - `ncol()`

  - Use R functions to compute descriptive statistics, and confirm the
    following statistics. Your output does not have to be in the same
    format of the table below. The important thing is that you begin
    learning how to manipulate columns (or vectors) of a data.frame.

<!-- end list -->

``` 
       Length Diam  Height  Whole  Shucked  Viscera    Shell    Rings
Min    0.075  0.055 0.000   0.002    0.001    0.001    0.002        1
Max    0.815  0.650 1.130   2.826    1.488    0.760    1.005       29
Mean   0.524  0.408 0.140   0.829    0.359    0.181    0.239    9.934
SD     0.120  0.099 0.042   0.490    0.222    0.110    0.139    3.224
```

-----

## Filtering, Slicing, and Selecting

The second part of this lab involves learning about basic manipulation
tasks of data tables.

Perhaps the most basic operations have to do with selecting rows and
columns. Analysts tend to refer to these operations in various ways:
filtering, slicing, and selecting. Here’s a description of such
operations.

**Slicing** has to do with selecting rows by indicating their index
position. Using bracket notation, you pass a numeric vector for the
rows:

``` r
# first three rows
three_rows <- abalone[1:3, ]
three_rows
```

**Filtering** involves selecting rows by specifying a certain (logical)
condition. The selected rows will be those for which the condition is
TRUE.

``` r
# subset rows given a condition
# (length greater than 0.6)
gt <- abalone[abalone$length > 0.6]
gt
```

**Selecting** has to do with selecting columns by name (or position).
Using bracket notation, you pass a character vector with the names of
the columns for the column-index:

``` r
length_diam <- abalone[ ,c('Length', 'Diameter')]
head(length_diam)
```

### Your Turn

  - slice the data by selecting the first 5 rows

  - slice the data by selecting rows 5, 10, 15, 20, 25, …, 50.

  - slice the data by selecting the last 5 rows; try doing this without
    using `tail()`, and without hard coding the numbers of the alst five
    rows.

  - create a data frame `height14` by filtering the data with those
    abalones with Height less than 0.14, and display its dimensions with
    `dim()`

  - create a data frame `infant` by filtering the data about Infant
    abalones, and display its dimensions with `dim()`

  - create a data frame `male_female` by filtering the data with Male
    and Female abalones, and display its dimensions with `dim()`

  - filter the data with those abalones with more than 25 Rings,
    displaying only their Sex, and Rings.

  - filter the data with those infant abalones with more than 3 Rings
    and less than 6, displaying only their Sex, Rings, and Diameter.

-----

## Adding new variables and Sorting rows

Another basic data-table manipulation task involves adding new
variables. Let’s create a small data frame `abies` by filtering only
infant abalones, and gathering columns Length, Height, and Diameter:

``` r
# creating a small data frame
abies <- abalone[abalone$Sex == 'I', c('Length', 'Height', 'Diameter')]
```

Say you want to add a column `Ht_Len` to `abies` with the ratio `height
/ length`. Here’s how to do it:

``` r
abies$Ht_Len <- abies$Height / abies$Length
```

Another common type of task consists of reordering rows. For example,
say you want to get a data frame `abies2` by ordering the rows in
`abies` by `Length` in decreasing order:

``` r
abies2 <- abies[order(abies$Length, decreasing = TRUE), ]
```

### Your Turn

  - using the data frame `abies`, add a new variable `product` with the
    product of `Whole` and `Shucked`.

  - create a new data frame `abies3`, by adding columns `log_height` and
    `log_length` with the log transformations of `height` and `length`.

  - use the original data frame `abalone` to *filter* and *arrange*
    those abalones with height less than 0.12, in increasing order.

  - display a data frame with the Sex, Diameter, and Rings, of the top-5
    highest abalones

  - display a data frame with the Sex, Diameter, and Rings, of the top-5
    longest abalones

-----

## Basic Plots

As you can tell, the `abalone` data contains 9 variables. To start
exploring the content, we begin by producing charts for each single
variable, focused on looking at their distributions:

  - Quantitative variables: histogram, boxplot
  - Qualitative variables: barchart, piechart

When examining a factor (or any categorical variable) you can always
create a frequency table first—via `table()`—and then plot a barchart
with `barplot()`

``` r
table_sex <- table(abalone$Sex)
barplot(table_sex)
```

Alternativey, you can also create a piechart with `pie()`.

For a quantitative variable, the typical graphics to examine the
distribution are histograms (`hist()`) and boxplots (`boxplot()`)

``` r
hist(abalone$Diameter)
boxplot(abalone$Diameter, horizontal = TRUE)
```

### Your Turn

The workhorse plotting function in base R is `plot()`. This function is
actually a *method*, meaning that it behaves differently depending on
the type of input.

Find out what kind of graphic is returned by `plot()` when you pass it
the following inputs:

  - a numeric variable: e.g. `abalone$Height`

  - a factor: e.g. `Sex`

  - two numeric variables: e.g. `abalone$Height` and `abalone$Length`

  - a data frame with two numeric columns: e.g. `Height`, and `Length`

  - a data frame with more than two numeric columns: `Height`, `Length`,
    and `Diameter`

  - a 2-column data frame with one factor in the first column, and one
    numeric vector in the second column: e.g. `Sex` and `Length`

  - a 2-column data frame with one numeric vector in the first column,
    and one factor in the second column: e.g. `Length` and `Sex`

### Your Turn: Scatter Diagrams

Perhaps the most common use of `plot()` is to create scatter diagrams
(i.e. scatterplots). Actually, the deafult scatterplot function is
`plot.deafult()`.

Look at the documentation of `plot()`, `plot.default()`, the graphical
parameters `par()`, as well as `points()`, and experiment with several
scatterplots specifying arguments like:

  - point character: `pch` (see `?points`)
  - point color(s): `col` (see \`?points)
  - point size: `cex` (see `?cex`)
  - x-axis label: `xlab` (see `?plot`)
  - y-axis label: `ylab` (see `?plot`)
  - title: `main` (see `?plot`)
  - subtitle: `sub` (see `?plot`)
  - logarithmic transformation of x and/or y: `log` (see
    `?plot.default`)
  - feel free to play with other graphical parameters
