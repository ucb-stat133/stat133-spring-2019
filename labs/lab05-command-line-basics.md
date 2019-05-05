Lab 5: Command Line Basics
================
Gaston Sanchez

> ### Learning Objectives
> 
>   - Practicing with the command line
>   - Navigating the filesystem and managing files
>   - Practice basic manipulation of data files
>   - Practice exporting tables from R
>   - Practice exporting displayed output (as is) from R
>   - Practice exporting plot images from R

### General Instructions

  - Write your descriptions, explanations, and code in an `Rmd` (R
    markdown) file.
  - Name this file as `lab05-first-last.Rmd`, where `first` and `last`
    are your first and last names (e.g. `lab05-gaston-sanchez.Rmd`).
  - Knit your `Rmd` file as an html document (default option).
  - Submit your `Rmd` and `html` files to bCourses, in the corresponding
    lab assignment.

-----

## Basic Shell Commands

The first part of the lab involves navigating the file system and
manipulating files (and directories) with the following basic shell
commands:

  - `pwd`: print working directory
  - `ls`: list files and directories
  - `cd`: change directory (move to another directory)
  - `mkdir`: create a new directory
  - `touch`: create a new (empty) file
  - `cp`: copy file(s)
  - `mv`: rename file(s)
  - `rm`: delete file(s)

#### Online Man Pages for Windows Users

If you are using **git-bash** (i.e. your OS is Windows) you don’t have
the `man` command to see the manual documentation of other commands. In
this case you can check the *man* pages online:

<http://man7.org/linux/man-pages/index.html>

#### Unevaluated Code Chunks

In this lab you will be writing bash commands. Depending on your
Operating System, you could include such commands inside code chunks in
an `Rmd` file, that get evaluated when knitting into html. But we won’t
do that today (mainly because some of you use Windows computers).

Instead, write your bash commands inside a chunk that is NOT evaluated.
One way to do this is to add the option `eval = FALSE` inside the curly
braces of the chunk (see image below)

![](lab05-images/unevaluated-chunk.png)

-----

### 1\) Your Turn\*: Lab Directory

  - Open (or launch) the command line

  - Use the command `pwd` to see what’s your current directory

  - Use `mkdir` to create a new directory `stat133-lab05`

  - Change directory to `stat133-lab05`

  - Use the command `curl` to download the following text file:

<!-- end list -->

``` bash
# the option is the letter O (Not the number 0)
curl -O http://textfiles.com/food/bread.txt
```

  - Use the command `ls` to list the contents in your current directory

  - Use the command `curl` to download these other text files:
    
      - <http://textfiles.com/food/btaco.txt>
      - <http://textfiles.com/food/1st_aid.txt>
      - <http://textfiles.com/food/beesherb.txt>
      - <http://textfiles.com/food/bakebred.txt>

  - Use the command `curl` to download the following csv
        files:
    
      - <http://archive.ics.uci.edu/ml/machine-learning-databases/forest-fires/forestfires.csv>
      - <http://web.pdx.edu/~gerbing/data/cars.csv>
      - <http://web.pdx.edu/~gerbing/data/color.csv>
      - <http://web.pdx.edu/~gerbing/data/snow.csv>
      - <http://web.pdx.edu/~gerbing/data/mid1.csv>
      - <http://web.pdx.edu/~gerbing/data/mid2.csv>
      - <http://web.pdx.edu/~gerbing/data/minutes1.csv>
      - <http://web.pdx.edu/~gerbing/data/minutes2.csv>

### 2\) Your Turn\*: Inspecting a Directory

  - Use the command `ls` to list the contents in your current directory

  - Now try `ls -l` to list the contents in your current directory in
    long format

  - Look at the `man` documentation of `ls` to find out how to list the
    contents in reverse order

  - How would you list the contents in long format arranged by time?

  - Find out how to use the wildcard `*` to list all the files with
    extension `.txt`

  - Use the wildcard `*` to list all the files with extension `.csv` in
    reverse order

  - You can use the character `?` to represent a single character: e.g.
    `ls mid?.csv`. Find out how to use the wilcard `?` to list `.csv`
    files with names made of 4 characters (e.g. `mid1.csv`, `snow.csv`)

  - The command `ls *[1]*.csv` should list `.csv` files with names
    containing the number 1 (e.g. `mid1.csv`, `minutes1.csv`). Adapt the
    command to list `.csv` files with names containing the number 2.

  - Find out how to list files with names containing any number.

### 3\) Your Turn\*: Moving Files

  - Inside `stat133-lab05` create a directory `data`

  - Change directory to `data`

  - Create a directory `txt-files`

  - Create a directory `csv-files`

  - Use the command `mv` to move the `bread.txt` file to the folder
    `txt-files`. Without changing directories, use `ls` to confirm that
    `bread.txt` is now inside `txt-files`.

  - Use the wildcard `*` to move all the `.txt` files to the directory
    `txt-files`. Without changing directories, use `ls` to confirm that
    all the `.txt` files are inside `txt-files`.

  - Use the wildcard `*` to move all the `.csv` files to the directory
    `csv-files`. Without changing directories, use `ls` to confirm that
    all the `.csv` files are inside `csv-files`.

  - Try using the command `tree` to see a visual display of the
    filestructure. *Warning: You may not have this command in git-bash
    or in another shell flavor*.

### 4\) Your Turn\*: Copying Files

  - Go back to the parent directory `stat133-lab05`

  - Create a directory `copies`

  - Use the command `cp` to copy the `bread.txt` file (the one inside
    the folder `txt-files`) to the `copies` directory

  - Without changing directories, use `ls` to confirm that `bread.txt`
    is now inside `copies`.

  - Use the wildcard `*` to copy all the `.txt` files in the directory
    `copies`

  - Without changing directories, use `ls` to confirm that all the
    `.txt` files is now inside `copies`.

  - Use the wildcard `*` to copy all the `.csv` files in the directory
    `copies`

  - Try using the command `tree` to see a visual display of the
    filestructure.

### 5\) Your Turn\*: Renaming and Deleting Files

  - Change to the directory `copies`

  - Use the command `mv` to rename the file `bread.txt` as
    `bread-recipe.txt`

  - Rename the file `cars.csv` as `autos.csv`

  - Rename the file `btaco.txt` as `breakfast-taco.txt`

  - Change to the parent directory (i.e. `stat133-lab05`)

  - Rename the directory `copies` as `copy-files`

  - Find out how to use the `rm` command to delete the `.csv` files that
    are in `copy-files`

  - Find out how to use the `rm` command to delete the directory
    `copy-files`

  - List the contents of the directory `txt-files` displaying the
    results in reverse (alphabetical) order

-----

### Optional challenge

If you are already familiar with the basic bash commands to navigate the
filesystem (or if you want to expand your R skills), use the R functions
to manipulate files and directories to perform the exact same tasks from
within R. See `?files` for more information.

  - `getwd()`
  - `setwd()`
  - `download.file()`
  - `dir.create()`
  - `list.files()`
  - `list.dirs()`
  - `file.create()`
  - `file.copy()`
  - `file.rename()`
  - `file.remove()`

-----

## Abalone Data Set

The second part of the lab involves downloading the **Abalone Data Set**
that you used in lab03: <http://archive.ics.uci.edu/ml/datasets/Abalone>

The location of the data file
is:

<http://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.data>

The location of the data dictionary (description of the data)
is:

<http://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.names>

### Your Turn:

  - Change to the directory `stat133-lab05`

  - Create a directory `abalone`

  - Change to `abalone` directory

  - Use `curl` to download the file `abalone.data`

  - Use the `file` command to know what type of file is `abalone.data`.

  - Use the *word count* command `wc` to obtain information about: 1)
    newline count, 2) word count, and 3) byte count, of the
    `abalone.data` file.

  - See the `man` documentation of `wc` and learn what option you should
    use to obtain only the number of lines in `abalone.data`.

  - Use `head` to take a peek at the first lines (10 lines by default)
    of `abalone.data`

  - See the `man` documentation of `head` and learn what option you
    should use to display only the first 5 files in `abalone.data`.

  - How would you display the first 15 files in `abalone.data`?

  - Use `tail` to take a peek at the last lines (10 lines by default) of
    `abalone.data`

  - See the `man` documentation of `tail` and learn what option you
    should use to display only the last 3 files in `abalone.data`.

  - Use the `less` command to look at the contents of `abalone.data`
    (this command opens a *paginator* so you can move up and down the
    contents of the file). Press the key `q` to exit the paginator.

  - Rename `abalone.data` as `abalone.csv`

  - Make a copy of `abalone.csv`, naming this copy `dataset.csv`

  - Move `dataset.csv` to the directory `csv-files`

-----

## Exporting Objects from R to External Files

In this second part of the lab, you will practice exporting different
objects and outputs from R to external files. The underlying goal is
that you practice specifying relative file paths.

  - Create a directory `exports` inside `stat133-lab05`.

  - The data that you will have to use is the built-in data frame
    `mtcars`

<!-- end list -->

``` r
head(mtcars)
```

    ##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
    ## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
    ## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
    ## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
    ## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
    ## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
    ## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1

### Exporting Tables from R’s console

Let’s begin by exporting the data `mtcars` to a CSV file, **executing
commands from the console**. Suppose that we want to export `mtcars`
inside the directory `exports`. The first thing to do is to find out
what is the *working directory* that the R console is paying attention
to.

``` r
# get working directory
getwd()
```

#### Example 1

Let’s assume that the working directory of R’s console is `Desktop`, and
that `stat133-lab105` is a subdirectory of `Desktop`, like in the
following scheme:

    Desktop/
      stat133-lab05/
        exports/

Here’s how you could export `mtcars` to a CSV file named `mtcars.csv`,
to be saved in the folder `exports`, using the function `write.csv()`:

``` r
write.csv(
  x = mtcars, # R object to be exported
  file = 'stat133-lab05/exports.csv'  # file path
)
```

#### Example 2

Let’s make things a bit more interesting. Suppose now that the working
directory of R’s console is the directory `Documents`, which is at the
same level of `Desktop`.

To export `mtcars` to a CSV file named `mtcars.csv`, you can use a
relative path like this:

``` r
write.csv(
  x = mtcars, # R object to be exported
  file = '../Desktop/stat133-lab05/exports.csv'  # file path
)
```

### Exporting some R output

What about exporting some output returned by a function or some other
computation? For example, say you are interested in exporting the
summary statistics of `mpg` and `disp`, exactly in the same way they are
displayed by R (in its console):

``` r
summary(mtcars[ ,c('mpg', 'disp')])
```

    ##       mpg             disp      
    ##  Min.   :10.40   Min.   : 71.1  
    ##  1st Qu.:15.43   1st Qu.:120.8  
    ##  Median :19.20   Median :196.3  
    ##  Mean   :20.09   Mean   :230.7  
    ##  3rd Qu.:22.80   3rd Qu.:326.0  
    ##  Max.   :33.90   Max.   :472.0

One naive option to “export” this output would be to manually copy the
text displayed on the console, and then paste it to a text file. While
this may work, it is labor intensive, error prone, and highly
irreproducible.

#### Example 3

A better way to achieve this task is with the `sink()` function. Assume
again that R’s console working directory is `Desktop`. Here’s how to
export the output of `summary()` to a text file `summary-mpg-disp.txt`

``` r
# divert output to the specified file
sink(file = 'stat133-lab05/summary-mpg-disp.txt')
summary(mtcars[ ,c('mpg', 'disp')])
# closing sinking operation
sink()
```

The first call to `sink()` opens a connection to the specified file, and
then all outputs are diverted to that location. The second call to
`sink()`, i.e. the one without any arguments, closes the connection.

While you are `sink()`ing output to a specified file, all the results
will be sent to such file. In other words, nothing will be printed on
the console. Only after the sinking process has finished and the
connection is closed, you will be able to execute commands and see
results displayed on R’s console.

### Exporting some “base” graphs

In the same way that R output, as it appears on the console, can be
exported to some files, you can do the same with graphics and plots.
Actually, saving plot images is much more common than `sink()`ing
output.

Base R provides a wide array of functions to save images in most common
formats:

  - `png()`
  - `jpeg()`
  - `tiff()`
  - `bmp()`
  - `svg()`
  - `pdf()`

Similar to the writing table functions such as `write.table()` or
`write.csv()`, and the `sink()` function, the graphics device functions
require a file name to be provided.

#### Example 4

Here’s how to save a simple scatterpot of `mpg` and `disp` in png format
to the folder `exports/`:

``` r
# saving a scatterplot in png format
png(filename = "stat133-lab05/exports/scatterplot-mpg-disp.png")
plot(mtcars$mpg, mtcars$disp, pch = 20, 
     xlab = 'Miles per Gallon', ylab = 'Displacement')
dev.off()
```

  - The function `png()` tells R to save the image in PNG format, using
    the provided filename.
  - Invoking `png()` will open a graphics device; not the graphics
    device of RStudio, so you won’t be able to see the graphic.
  - The `plot()` function produces the scatterplot.
  - The function `dev.off()` closes the graphics device.

-----

### Your turn\*

Instead of executing commands from the R console, you will have to
perform the following tasks inside code chunks of your `Rmd` file. This
implies that the working directory, when knitting the file into an html
document, will be the directory in which the `Rmd` files is located (by
default).

  - Export a data frame with columns `mpg`, `disp`, and `hp`, to a CSV
    file `dataset.csv` in the `exports/` subdirectory.

  - Export the output of `str()` on `mtcars` to a text file called
    `mtcars-structure.txt` (inside the `exports/` subdirectory).

  - Export the `summary()` of the entire data frame `mtcars` to a text
    file `summary-mtcars.txt`, in the `exports/` folder.

  - Open the help documentation of `png()` and related graphic devices.

  - Use `png()` to save a scatterplot of `mpg` and `wt` with `plot()`.
    Save the graph as `scatterplot-mpg-wt.png` in the `exports/` folder.

  - Save another version of the scatterplot between `hp` and `wt`, but
    now try to get an image with higher resolution. Save the plot as
    `scatterplot-hp-wt.png` in `exports/`.

  - Save a histogram in JPEG format of `mpg` with dimensions (width x
    height) 600 x 400 pixels, name the file `histogram-mpg.jpeg`.

  - Use `pdf()` to save the previous histogram of `age` in PDF format,
    with dimensions (width x height) 7 x 5 inches, name the file
    `histogram-mpg.pdf`.

  - The package `"ggplot2"` comes with a wrapper function `ggsave()`
    that allows you to save ggplot graphics to a specified file. By
    default, `ggsave()` saves images in PDF format.

  - Use `ggplot()` to make a scatterplot of `mpg` and `disp`, and store
    it in a ggplot object named `gg_mpg_disp`. Then use `ggsave()` to
    save the plot with dimensions (width x height) 7 x 5 inches, as
    `scatterplot-mpg-disp.pdf`.
