Introduction to R
========================================================
author: Joshua Rosenberg and Alex Lishinski
date: 10/23/2015

ARRR Matey
========================================================

### Why we love R and Why we think you will love R, too

* R is free. As an open-source project, you can use R free of charge: no worries about subscription fees, license managers, or user limits.

* R is a language. In R, you do data analysis by writing functions and scripts, not by pointing and clicking. A script documents all your work, from data access to reporting, and can instantly be re-run at any time.

* Graphics and data visualization. One of the design principles of R was that visualization of data through charts and graphs is an essential part of the data analysis process. As a result, it has excellent tools for creating graphics.

* A flexible statistical analysis toolkit. All of the standard data analysis tools are built right into the R language.

Why we love R
=========================================================

* Access to powerful, cutting-edge analytics. Leading academics and researches from around the world use R to develop the latest methods in statistics, machine learning, and predictive modeling.

* A robust, vibrant community. There's a wealth of community resources for R available on the Web, for help in just about every domain.

* Unlimited possibilities. With R, you're not restricted to choosing a pre-defined set of routines. You can use code contributed by others in the open-source community, or extend R with your own functions.

* R is what is used by the majority of academic statisticians.  This is where new developments are going to be implemented.

Why we love R
=========================================================

* R is effectively platform independent.  For Linux/Mac users that work with people who use windows, this is helpful.

* R is used by practitioners in a plethora of academic disciplines.  R users come from myriad industries and academic departments.

* R makes you think.  Being forced to code a procedure by hand, though more time consuming, helps make it “stick”.

* All encompasing. there's probably already an R package for whatever you'll ever do with data, no need for many different softwares.

What's an object and how do I make one?
========================================================

This is code (syntax):


```r
c() # makes a vector
: # makes a sequence
```

Let's make a vector of the numbers 1 to 10:


```r
my_vector <- c(1:10)
```

This is the result of typing the name of "my_vector":

```r
my_vector
```

```
 [1]  1  2  3  4  5  6  7  8  9 10
```

Let's read something
========================================================


```r
setwd("~/desktop")
my_data <- read.csv("r_introduction.csv", row.names = 1)
head(my_data)
```


What is a package and how do I install them?
========================================================

Here's how to install a package:

```r
install.packages("ggplot2")
```

Here's how to use a package (must do every time you use R):

```r
library(ggplot2)
```

What are some helpful packages?
========================================================

There are over 7000 packages, covering pretty much every topic you'd want


```r
# Great plotting functionality
library(ggplot2)
# Great data manipulation
library(dplyr)
# A number of basic statistical procedures you will want to use
library(psych)
# Miscellaneous functions that are quite useful
library(Hmisc)
# Importing data from other file formats, like .sav
library(foreign)
# Deal with dates in your data
library(lubridate)
```

What's this thing?
========================================================


```r
- ? # this is to find out what a function does
- str() # this is to find out the 'structure' of anything
- View() # this allows you to view a data frame (think spreadsheet) or matrix
- class() # this tells you what kind of object this is
```

How do I get my data in?
========================================================

Examples of loading data for different sorts of files


```r
readxl::read_excel("filename.xlsx")
read.csv("filename.csv", header = F)
haven::read_sav("filename.sav")
```

How do I pick just one part of this thing?
========================================================


```r
my_data[1, ] # just the first row of data frame

my_data[, 1] # just the first column of data frame

head(my_data) # first six rows of data frame

tail(my_data) # last six rows of data frame
```

dplyr is a very useful package for data manipulation
========================================================


```r
dplyr::select(my_data, ) # Select only certain columns

dplyr::filter(mydata, ) # select only certain rows

# how to find out more about how to use dplyr

# Vignettes are documents that explain how to use packages in fleshed out examples
vignette(package = "dplyr")
vignette("introduction", package = "dplyr")

dplyr::arrange(my_data, ) # arrange data by a variable
```

How do I do some basic statistics?
========================================================

Basic Descriptives


```r
mean(my_data$math) # mean of continuous variable
sd(my_data$math) # standard deviation of continous variable
table(my_data$Race) # counts frequencies and creates a table
```

Descriptives table from psych


```r
library(psych)
describe(my_data) # try it on your own!
```

Worked Example
========================================================


```r
# load built-in datasets
data(mtcars)

psych::describe(mtcars) # try it on your own!
```

```
     vars  n   mean     sd median trimmed    mad   min    max  range  skew
mpg     1 32  20.09   6.03  19.20   19.70   5.41 10.40  33.90  23.50  0.61
cyl     2 32   6.19   1.79   6.00    6.23   2.97  4.00   8.00   4.00 -0.17
disp    3 32 230.72 123.94 196.30  222.52 140.48 71.10 472.00 400.90  0.38
hp      4 32 146.69  68.56 123.00  141.19  77.10 52.00 335.00 283.00  0.73
drat    5 32   3.60   0.53   3.70    3.58   0.70  2.76   4.93   2.17  0.27
wt      6 32   3.22   0.98   3.33    3.15   0.77  1.51   5.42   3.91  0.42
qsec    7 32  17.85   1.79  17.71   17.83   1.42 14.50  22.90   8.40  0.37
vs      8 32   0.44   0.50   0.00    0.42   0.00  0.00   1.00   1.00  0.24
am      9 32   0.41   0.50   0.00    0.38   0.00  0.00   1.00   1.00  0.36
gear   10 32   3.69   0.74   4.00    3.62   1.48  3.00   5.00   2.00  0.53
carb   11 32   2.81   1.62   2.00    2.65   1.48  1.00   8.00   7.00  1.05
     kurtosis    se
mpg     -0.37  1.07
cyl     -1.76  0.32
disp    -1.21 21.91
hp      -0.14 12.12
drat    -0.71  0.09
wt      -0.02  0.17
qsec     0.34  0.32
vs      -2.00  0.09
am      -1.92  0.09
gear    -1.07  0.13
carb     1.26  0.29
```

Data manipulation with dplyr
========================================================


```r
# selecting only the columns I want
importantData <- dplyr::select(mtcars, mpg, cyl, disp, hp, wt)
head(importantData)
```

```
                   mpg cyl disp  hp    wt
Mazda RX4         21.0   6  160 110 2.620
Mazda RX4 Wag     21.0   6  160 110 2.875
Datsun 710        22.8   4  108  93 2.320
Hornet 4 Drive    21.4   6  258 110 3.215
Hornet Sportabout 18.7   8  360 175 3.440
Valiant           18.1   6  225 105 3.460
```

```r
# Selecting only some rows
goodCars <- dplyr::filter(mtcars, cyl == 8, mpg > 15)
head(goodCars)
```

```
   mpg cyl  disp  hp drat    wt  qsec vs am gear carb
1 18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
2 16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
3 17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
4 15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
5 15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
6 15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
```

```r
# Rearranging the data
sortedData <- dplyr::arrange(importantData, mpg)
head(sortedData)
```

```
   mpg cyl disp  hp    wt
1 10.4   8  472 205 5.250
2 10.4   8  460 215 5.424
3 13.3   8  350 245 3.840
4 14.3   8  360 245 3.570
5 14.7   8  440 230 5.345
6 15.0   8  301 335 3.570
```

The mighty lm() for linear models (i.e., regression) (Alex)
========================================================


```r
data(mtcars) # get mtcars data

# create model and save as variable
model <- lm(mpg ~ cyl + disp + hp,  data = mtcars)
model

# get more detailed model summary
summary(model)

# anova table
anova(model)

assumps <- AutoModel::assumptions_check(model)
assumps
```

What are some other things we can do? (Alex & Josh)
========================================================


```r
library(lavaan) # SEM
library(lme4) # HLM
library(tm) & library(quanteda) # text analysis / text mining
library(matchit) # PSM
library(caret) # machine learning
library(igraph) # social network analysis
```

Rmarkdown & knitr
=========================================================

Rmarkdown documents are documents that include plain text that can be styled with very simple syntax as well as executable R code

This presentation was made from an R markdown document

R markdown documents can be turned into nice looking pdf, word, and html files

Makes sharing results extremely easy

* Easy to make changes and rerun analyses
* No cutting and pasting values and tables
* Less time wasted formatting documents

Conclusion
======================================================

What you should take away from this?

* R is awesome
* There is a learning curve
* Everyone I know who waited to start R regrets it
* All the cool kids are using it
* Nobody can ever take it away from you
