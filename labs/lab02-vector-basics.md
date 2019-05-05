Lab 2: Vectors
================
Gaston Sanchez

> ### Learning Objectives
> 
>   - Work with vectors of different data types
>   - Understand the concept of *atomic* structures
>   - Learn how to subset and slice R vectors
>   - Understand the concept of *vectorization*
>   - Understand *recycling* rules in R

### General Instructions

  - Write your descriptions, explanations, and code in an `Rmd` (R
    markdown) file.
  - Name this file as `lab02-first-last.Rmd`, where `first` and `last`
    are your first and last names (e.g. `lab02-gaston-sanchez.Rmd`).
  - Knit your `Rmd` file as an html document (default option).
  - Submit your `Rmd` and `html` files to bCourses, in the corresponding
    lab assignment.
  - Due date displayed in the syllabus (see github repo).

-----

## Getting the Data File

In this lab, you are going to work with a handful of variables about NBA
players from the regular season 2017-2018:

  - `player`: name of player.
  - `team`: team name abbreviation.
  - `position`: player position.
  - `age`: age of player.
  - `experience`: years of experience in NBA.
  - `salary`: salary (in dollars).
  - `scored`: total scored points.
  - `points1`: number of free throws, worth 1 point each.
  - `points2`: number of 2-point field goals, worth 2 points each.
  - `points3`: number of 3-point field goals, worth 3 points each.

The data is in the file `nba2018-salary-points.RData`, located in the
github repository `https://github.com/ucb-stat133/stat133-labs`. The
original source of the data is the website
[www.basketball-reference.com](http://www.basketball-reference.com/)

Open a new session in Rstudio, and make sure you have a clean workspace
by typing this command on the console:

``` r
# remove existing objects
rm(list = ls())
```

You can download the `.RData` file to your working directory, and then
`load()` it with the code below. Do NOT include these commands in your
source Rmd file; simply type them directly on the console:

``` r
# download RData file into your working directory
rdata <- "https://github.com/ucb-stat133/stat133-labs/raw/master/data/nba2018-salary-points.RData"

download.file(url = rdata, destfile = 'nba2018-salary-points.RData')
```

### What’s happening in the code above?

The function `download.file()` allows you to download any type of file
from the Web. In this case you are downloading the file called
`nba2018-salary-points.RData` which is located in the github repository
of the course. This file is a binary file. To be more precise, the file
extension `.RData` is the default extension used by R for its binary
native format.

Where does the file get downloaded? By default, the file
`nba2018-salary-points.RData` gets downloaded to your **working
directory**. If you are curious about what is the current directory to
which R is paying attention to, simply type the function `getwd()`—which
stands for *get the working directory*.

If you want to specify a specific location for the downloaded file, then
modify the `destfile` parameter. For instance, if you are using Mac, and
you want the file to be downloaded to your desktop, you can use:

``` r
# download RData file to your Desktop (assuming you use Mac)
rdata <- "https://github.com/ucb-stat133/stat133-labs/raw/master/data/nba2018-salary-points.RData"
download.file(url = rdata, destfile = '~/Desktop/nba2018-salary-points.RData')
```

### Loading the data file

To load or import the contents of the binary file into your R session
you use `load()`. This function allows you to import R binary files.
This time, include the code below in your `Rmd` file:

``` r
# load data in your R session
load('nba2018-salary-points.RData')
```

Note: the code above will only work as long as your `Rmd` file lives in
the same directory of the `.RData` file. So far I’m assuming that you
have both files in your working directory.

Once you imported (or loaded) the data, use the function `ls()` which
allows you to **list** all the available R objects:

``` r
# list the available objects with ls()
ls()
```

-----

### Your turn: subsetting vectors

Create a vector `four` by selecting the first four elements in `player`:

``` r
four <- head(player, n = 4)
```

Single brackets `[ ]` are used to subset (i.e. subscript, split)
vectors. Find out what happens if you specify:

  - number one: `four[1]`
  - an index of zero: `four[0]`?
  - a negative index: `four[-1]`?
  - various negative indices: `four[-c(1,2,3)]`?
  - an index greater than the length of the vector: `four[5]`?
  - repeated indices: `four[c(1,2,2,3,3,3)]`?

Often, you will need to generate vectors of numeric sequences, like the
first five elements `1:5`, or from the first till the last element
`1:length(player)`. R provides the colon operator `:`, and the functions
`seq()`, and `rep()` to create various types of sequences.

### Your turn: sequences and repetitions

Figure out how to use `seq()`, `rep()`, and bracket notation, to
extract:

  - all the even elements in `player`
  - all the odd elements in `salary`
  - all multiples of 5 (e.g. 5, 10, 15, etc) of `team`
  - elements in positions 10, 20, 30, 40, etc of `scored`
  - all the even elements in `team` but this time in reverse order

-----

## Logical Subsetting and Comparisons

Another kind of subsetting/subscripting is the so-called **logical
subsetting**. This kind of subsetting typically takes place when making
comparisons. A **comparison operation** occurs when you use comparison
operators such as:

  - `>` greater than
  - `>=` greater than or equal
  - `<` less than
  - `<=` less than or equal
  - `==` equal
  - `!=` different

For example:

``` r
scored_four <- scored[1:4]

# elements greater than 100
scored_four[scored_four > 100]

# elements less than 100
scored_four[scored_four < 100]

# elements less than or equal to 10
scored_four[scored_four <= 10]

# elements different from 10
scored_four[scored_four != 10]
```

In addition to using comparison operators, you can also use **logical
operators** to produce a logical vector. The most common type of logical
operators are:

  - `&` AND
  - `|` OR
  - `!` negation

Run the following commands to see what R does:

``` r
# AND
TRUE & TRUE
TRUE & FALSE
FALSE & FALSE

# OR
TRUE | TRUE
TRUE | FALSE
FALSE | FALSE

# NOT
!TRUE
!FALSE
```

Logical operators allow you to combine several comparisons:

``` r
# players of Golden State (GSW)
player[team == 'GSW']

# name of players with salaries greater than 20 million dollars
player[salary > 20000000]

# name of players with scored points between 1000 and 1200 (exclusive)
player[scored > 1000 & points < 1200]
```

### Your turn: logical subsetting

Write commands, using bracket notation, to answer the following
questions (you may need to use `min()`, `max()`, `which()`,
`which.min()`, `which.max()`):

  - players in position Center, of Warriors (GSW)
  - players of both GSW (warriors) and LAL (lakers)
  - players in positions Shooting Guard and Point Guards, of Lakers
    (LAL)
  - subset Small Forwards of GSW and LAL
  - name of the player with largest salary
  - name of the player with smallest salary
  - name of the player with largest number of scored points
  - salary of the player with largest number of points
  - largest salary of all Centers
  - team of the player with the largest number of scored points
  - name of the player with the largest number of 3-pointers

-----

### Some plotting

Use the function `plot()` to make a scatterplot of `scored` and `salary`

``` r
plot(scored, salary)
```

Keep in mind that `plot()` is a generic function. This means that the
behavior of `plot()` depends on the type of input. When you pass two
numeric vectors, `plot()` will attempt to create a scatter plot.

### Plots with `"plotly"`

The function `plot()` produces static plots. But you can also try to get
interactive plots. One option to do this is via the R package
`"plotly"`. To use this package, you will have to install `"ggplot2"`
and `"plotly"`. Remember to use the `install.packages()` function but do
NOT include it in your Rmd:

``` r
install.packages(c("ggplot2", "plotly"))
```

What you DO need to include is the `library()` function to load
`"plotly`“:

``` r
library(plotly)
```

    ## Loading required package: ggplot2

    ## 
    ## Attaching package: 'plotly'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

The main function to graph data with `"plotly"` is the `plot_ly()`
function. When your data is in vectors, you can graph a scatterplot like
this:

``` r
plot_ly(x = scored, y = salary, type = "scatter", mode = "markers")
```

By the way, the output of `plot_ly()` will only work when you knit an
html file. If you try to knit using a different format, then `plot_ly()`
won’t work.

Looking at the generated plot, can you see any issues?

To get a better display of the scatterplot, let’s create two vectors
`log_scored` and `log_salary` by transforming `scored` and `salary` with
the logarithm function `log()`

``` r
log_scored <- log(scored)
log_salary <- log(salary)
```

Make another scatterplot but now use the log-transformed vectors:

``` r
plot(log_scored, log_salary)
```

To add the names of the players in the plot, you can use the low-level
graphing function `text()`:

``` r
plot(log_scored, log_salary)
text(log_scored, log_salary, labels = player)
```

Now we have another problem. The labels in the plot are very messy. A
quick and dirty fix is to use `abbreviate()` to shorten the displayed
names:

``` r
plot(log_scored, log_salary)
text(log_scored, log_salary, labels = abbreviate(player))
```

**Your Turn**: create a scatterplot of points and salary for the
Warriors (GSW), displaying the names of the players. Generate two
scatterplots, one with raw values (original scale, and another plot with
log-transformations).

-----

## Factors

As mentioned before, vectors are the most essential type of data
structure in R. They are *atomic* structures (can contain only one type
of data): integers, real numbers, logical values, characters, complex
numbers.

Related to vectors, there is another important data structure in R
called **factor**. Factors are data structures exclusively designed to
handle categorical data.

The object `team` is an R factor. You can confirm this by using
`is.factor()` or `class()`

``` r
is.factor(team)
```

    ## [1] TRUE

### Creating Factors

Use `factor()` to create an object `position_fac` by converting
`position` into a factor:

``` r
position_fac <- factor(position)
```

If you have a factor, you can invoke `table()` to get a table with the
frequencies (i.e. counts) of the factor categories or *levels*:

``` r
table(position_fac)
```

    ## position_fac
    ##   C  PF  PG  SF  SG 
    ##  97  98  96  84 102

### Your turn: Manipulating Factors

Because factors are internally stored as integers, you can manipulate
factors as any other vector:

``` r
position_fac[1:5]
```

    ## [1] C  PF SG PG SF
    ## Levels: C PF PG SF SG

Practice manipulating `position_fac` to get:

  - positions of Warriors
  - positions of players with salaries \> 15 millions
  - frequencies (counts) of positions with salaries \> 15 millions
  - relative frequencies (proportions) of ‘SG’ (Shooting Guards) in each
    team

### Your turn: More Plots

Let’s go back to the scatterplot of `scored` and `salary`

``` r
plot(scored, salary)
```

  - Use your factor `position_fac` to add some color to the dots in the
    scatterplot.
  - Pass the factor to the `col =` parameter inside `plot()`
  - Experiment with other `plot()` arguments like the *point character*
    `pch =`, the *size of dots* with the parameter `cex =`, the axes
    labels `xlab` and `ylab` and so on.

-----
