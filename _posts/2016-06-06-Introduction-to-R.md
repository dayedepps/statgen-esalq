---
layout: post
title: Introduction to R
description: "For beginners with focus on Bioinformatics and Genetics."
modified: 2016-06-03
tags: [tips, introduction, tutorial, R]
image:
  feature: LogoFundoAzul.jpg
  creditlink: http://augusto-garcia.github.io/
---

*Written by [Rodrigo Rampazo Amadeu](http://augusto-garcia.github.io/statgen-esalq/people/)*

Purpose
=======

The idea of this course is to present the basic commands and concepts
about the R language for genetic and bioinformatic students. Everything
typeful on R will be on `verbatim`.

-   [Purpose](#purpose)
-   [Installing R](#installing-r)
-   [Using R](#using-r)
-   [R creating objects](#r-creating-objects)
-   [Importing and exporting data](#importing-and-exporting-data)
-   [Libraries](#libraries)
-   [Graphic Plotting](#graphic-plotting)
-   [The "for" and "if" structures](#the-for-and-if-structures)
-   [Simulating Data](#simulating-data)
-   [About it](#about-it)

Installing R
============

To install R, we strongly advise you to use RStudio for your firsts R
contact. To install it go to
[RStudio](https://www.rstudio.com/products/rstudio/download/) and follow
the instructions. If you are familiar with Emacs, try [ESS](http://ess.r-project.org/).

Using R
=======

Open R, if you are using RStudio you will see a script window and a
console window, all the commands here is to be used and wroted on the
console window. We strongly advise you to write it down on the script
window and press *run* line by line on the top right corner. In this way
you can save and track all of your code. Try to run the following lines
on the next section.

R as calculator
---------------

Sum

     3+3   #I can comment or annotate my scripts by writing after the # sign

Divide

     (3+3)/3

Square Root

     9^0.5 #or
     sqrt(9)

Exponent

     2^10

Logaritm

     log(10) #
     log(10,base = 10)
     log(10,base = 2)

Exponential *e*

     exp(2)

Now, try to calculate the following expression using R:

\\[ (\frac{10+5+1.5}{3})^3+2 \\]

Have you got 168.375? If yes, go and take the log at base 10 of it. Have
you got 2.221?


Functions
---------

There are a lot of functions in R. A function is represented by a name
and can be used calling it names followed by arguments. To visualize
what a function does, you can type `?function`, for example:

     ?log

If you are using Rstudio this command you change a window in the right
of your screen, if not, probably you going to see a pop-up window in
your screen. This new window says what the function `log` does. Mainly
in the help there is a description, the usage, and the arguments of it.
For example, this function has the arguments x (which has to be a
numeric or complex vector), and base.

R creating objects
==================

To create a object use the following syntax:

     x = 10

Your object name 'x' followed by '=' and then your variable. Now,
everytime you call (type) 'x' you we receive 10. For example,

     x*2
     x+x
     x^x
     log(x,x)

You can also have a character object (which can not be used in math
operations):

     x_name = "name"

You can call it in the same way:

     x_name

To see which type your object is:

     class(x_name)
     class(x)

Pay attention, R is case-sensitive (*i.e.* 'X' is different than 'x').
When in doubt, write everything of your script in lower case.

Another important class is the logical whice can be TRUE or FALSE. For
example:

     1<0 #is 1 greater than 0? FALSE
     1==0 #is 1 equal 0? FALSE
     1>0 #is 1 lower than 0? TRUE

This logical operation can be wrote in an R object

     z=1<0

Vectors
-------

A vector can be create using the following syntax:

     x = c(1.5,2.1,2.5,3.4,4.3,6.1)
     y = c("A","A","B","B","C","C")

The above line will create: the 'x' vector with 6 numeric objects, and
the 'y' vector with 6 character objects. To visualize this information
in a fashion way you can use the function `str`. To visualize a specific
object you can use:

     x[6] #the sixth object of vector x
     y[2] #the second object of vector y 

This function is really powerful when working with big data, keep it in
mind, it gives you all the `str`ucture of the object. Keep in mind, a
vector can has only *one* type of data, for instance character or
numeric.

     str(x) #a vector with 6 numeric objects (1:6)
     str(y) #a vector with 6 character objects (1:6)

Notice that you replace the old x object by this new one. Be careful
when naming your objects. With vector, you can make more complex
calculus.

     sum(x) #the sum of the vector objects
     mean(x) #the mean of the vector objects
     var(x) #the variance between the vector objects
     sum(y) #returns error, because y is not numeric

We can combine 'y' and 'x' in a more complex function structure. For
example with the 'tapply' function. In this function first you choose
your atomic object (vector x), following by your index (vector y), and
then for the function you want to use. Foe example:

     tapply(x,y,sum) #Compute the sums of x by each y categorie
     tapply(x,y,mean) #Compute the means of x by each y categorie
     tapply(x,y,var) #Compute the variance of x by each y categorie

Logical Operation
-----------------

We can build a logical vector, for example:

     z <- x3 #Which x is grater than 3
     class(z)

If you call the object 'z' (writing `z` on console and pressing `enter`)
you will see which values of x is grater than 3. The logical expressions
is very useful when combining with another functions. For example, with
function 'which'. This function returns the exact position of the vector
it has TRUE values. Combined with brackets '\[\]', it can return which
values in x is greater than 3.

     which(z) #The TRUE is in position 5 and 6.
     x[which(z)]

Now it is your turn, using logical operations, the which function, and
brackets, extract out of vector x the numbers lower than 4.

Data frame
----------

We can combine vectors of same lenght in a data frame, to combine x and
y vectors:

     df = data.frame(x=x,y=y,z=z)

Data frames is a versatile way to combine vectors of different classes
in a single object. You can access the different vectors using the
operator $. For example:

     df$x
     df$y
     df$z

When combining a character vector in a data frame it will be turned as a
factor. In this data frame notation, you can use the same codes earlier
seen. For example for extract the mean using y as index.

     tapply(df$x,df$y,mean)
     tapply(df$x,df$z,mean) #see what is going on here

Matrices
--------

We can combine vectors of same length and same class in a matrix, we
have to define the number of rows, the number of columns and the
direction to read the data. Look all the differencs on the below lines.

     x #visualizing your x vector
     matrix(x,nrow=3,ncol=2,byrow=TRUE)
     matrix(x,nrow=2,ncol=3,byrow=TRUE)
     matrix(x,nrow=3,ncol=2,byrow=FALSE)
     matrix(x,nrow=2,ncol=3,byrow=FALSE)

Of course, we can save this matrix as a object

     X <- matrix(x,nrow=3,ncol=2,byrow=TRUE) #note X is different than x (lower case)
     dim(x) #to check the dimension of X

To select a specific object inside this matrix you can use the following
notation:

     X[3,1] #The element of third row and first column
     X[3,] #All the elements of third row
     X[,1] #All the elements of first row
     X[1:2,] #A matrix with all elements of first and second rows

If it is a matrix of numeric objects you can do matrix algebra. For
example:

     t(X) # transpose of X (X prime)
     t(X) %*% X # transpose of X times X
     X + 1 #add 1 to all elements of X
     2*X #multiply all elements of X by 2
     solve(t(X) %*% X) # inverse of transpose of X times X
     solve(t(X) %*% X) + 1 # inverse of transpose of X times X plus 1

Lists
-----

We can combine different objects with variable format and lengths in a
list.

     everything <- list(df=df,
                       X=X)

The object everything is a list with two objects: a data frame and a
matrix.

To access the information inside a list you can use $ as in data frames.

     everything$x

Or you can use an indicator of the level your information is. For
example, to access the first object of the first level of your list
(*i.e.* x vector):

     everything[[1]]

If you want to access the second object of the first level object of
your list (*i.e.* the second object of x):

     everything[[1]][[2]]

If you want to access the third object of the second level object of the
first level object of your list (*i.e.* the second object of x):

     everything[[1]][[2]][[3]]

And this classification goes on. Now try to access the fifth value of
vector x using this approach.

To add a new object in a list, be sure in what level you are working
with.

To add a new vector inside the data frame (first object of everything):

     everything[[1]][[4]] = c(1,2,3,4,5,6)

To create a new third object:

     everything[[3]] = c(1,2,3,4,5,6)

To add 1 on this new object:

     everything[[3]] = everything[[3]]+1

An important guide to play with data frames in the function str().

     str(everything)

This function print the structure of your data frame and show all the
categories of it. Be familiar with lists, almost every data is handle in
this format.

Importing and exporting data
============================

First download the data at <http://www.google.com If you are using
Rstudio, it is easy go to *Session -&gt; Set Working Directory -&gt; To
Source File Location* and select the folder your file is. Otherwise, you
can use the function of set work directory `setwd()`, the arguments of
the folder file using this function can be slightly different depending
upon your operational system. To make of the syntax type getwd() and
follow the same syntax it shows. Use a specific folder for a specific
project/course, please do not mess up your R files with different
courses and projects.

Example of setwd function (if you use the easy way of RStudio, skip this
chunk)

     getwd()
     setwd("/Users/patricio/course/week2/practice") ##fill with your path to archives

Reading the data, if you can choose, choose csv format files, they are
easy to read and understand. Before you call it in R, pay attention in
what the exactly way your data is. For example in the 'data.csv' file,
the data has 2 vectors with column names (`header`) and our missing data
(`na.strings`) is coded as -9.

     read.table("data.csv")
     read.table("data.csv",header = TRUE, na.strings=-9)

Saving the table in a object:

     data<-read.table("data.csv",header = TRUE, na.strings=-9)

If you want to save this object in a csv file:

     write.table(data,file="data_export.csv")

Look at the file you create and notice the differences between it
(`data_export.csv`) and `data.csv`. To let it in the same format we have
to use some additional arguments of the function:

     write.table(data,file="data_export.csv",row.names=FALSE,quote=FALSE,na="-9")

Now we have a copy of the file originated created. The default field
separator is " " (single space), if you want comma as separator, just
add 'sep=","' on the arguments. Pay attention in what you are writing
and reading, this can drag a lot of minor errors in your data analysis.

Libraries
=========

Library is a set of functions and dataset you can add to your base R.
Some libraries came with your base R and someothers have to be
installed. The most usable package repository is the
[CRAN](https://cran.r-project.org/), to install a package from there you
need to type `install.packages("packagename")`. In bioinformatics the
repository [Bioconductor](https://www.bioconductor.org/) is a good one,
to install a package of it please go to the webpage of the repository
and follow the instruction. After installed, you have to call the
library to use its functions and datasets. On the next section we will
use data from the *datasets* package, which should be already available
with your R. To use this package type:

     library(datasets)

Graphic Plotting
================

There are several types of graphics in R. We will present some of the
most used ones. We will use the data `mtcars` from the library
*datasets*. To look all the data from this package go to
<https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/00Index.html.

     data(mtcars) #Now mtcars is an object
     ?mtcars #To look the data description
     mtcars #To look the data

Scatterplot
-----------

To plot a scatterplot graphic (x × y graphic) where x will be *mpg*
(Miler/Gallon) and y will be number of *hp* (Gross horsepower)

     plot(x=mtcars$mpg,y=mtcars$hp)
     #Changing title (main) and axis label (xlab and ylab)
     plot(x=mtcars$mpg,y=mtcars$hp, main="Scatterplot mpg x hp", xlab="mpg", ylab="hp")

Histogram
---------

     hist(x=mtcars$mpg, main="Histogram of mpg", xlab="mpg")

Density
-------

     plot(density(mtcars$mpg), main="Density", xlab="mpg")

Boxplot
-------

     boxplot(x=mtcars$mpg, main="Boxplot of mpg", xlab="mpg")

Boxplot by cylindrade
---------------------

In this case we use `x ~ y` which means x as function of y. For example:

     boxplot(mtcars$mpg ~ mtcars$cyl, main="Boxplot of mpg", xlab="mpg")

Exporting a graphic
-------------------

To save a png graphic first you need to create a png file with the
function `png`, then plot your graphic, and at last close your png file
with `dev.off()`. For example:

      png(filename = "Rplot.png", width = 480, height = 480)
      boxplot(mtcars$mpg ~ mtcars$cyl, main="Boxplot of mpg", xlab="mpg")
      dev.off()

There are several ways and formats to save a R graphic, all the ways
follow those paths, create a file, plot, close the device. `?png` to
more information about it.

The graphics here presented are the basic ones, you can make better ones
with the package `ggplot2` and interactive ones with package `shiny`.

Task
----

Build graphics with `airquality` dataset and save them as jpeg.

The "for" and "if" structures
=============================

"for"
-----

Using `for` is a great way to do repetitive tasks in R, it shorts your
script and saves your time. We will present some basic loop ideas ans
concepts. In the following `for`, you have a counter called `i` which
starts on 1 and goes to 10, 1 by 1. Each loop will increase your object
`x` by the `1`. If you `x` is 0 as the beggining, after the loop will be
10. In other words, you will add one on x ten times.

     x=0
     for( i in 1:10){
       x = x+1
     }
     x

A big help of the `for` structure is the function `cat`, you can use it
to print on console what is going on on your loop and let you track your
loop. For example:

     x=0
     for( i in 1:10){
       x = x+1
       print(i)
     }
     x

In the `for` above, you print the number of each loop. You can also
print your object within the loop (if your object is not too big). For
example:

     x=0
     for( i in 1:10){
       x = x+1
       print(i)
       print(x)
     }
     x

Notice that the print order is first i and then x (on this case they are
equal). You can also use a understandble print way using the function
`paste`:

     x=0
     for( i in 1:10){
       x = x+1
       print(paste("i=",i))
       print(paste("x=",x))
     }
     x

"if"
----

Using `if` is a great way to make alternative routes in your script.
Attention, inside a `if` structure has to have a logical object, if it
has a non-logical object it will be interpreted as TRUE. For example, if
you want to add 1 only on odd numbers you can add the following
structure to your `for`:

     x=0
     for( i in 1:10){
       x = x+1
         if(x%%2 == 1){ # %% is the modulus (remainder) operator
           x = x+1
         }
       print(paste("i=",i))
       print(paste("x=",x))
     }
     x

Look at your console and try to understand what is going on here.

"for" with vectors
------------------

In the following `for` we are checking which number of a given vector is
even and which is odd, if it is even multiply by 10, else multiply by
100.

     x = c(1:20) #1:20 means build a vector with numbers from 1 to 20
     j = length(x) #function length return the length of the object, in this case 20
     for( i in 1:j){
       if( x[i]%%2 == 0){
         x[i] = 10*x[i]
       }else{
         x[i] = 100*x[i]
       }
     }
     x #looking the result

When using `for` and `if` structures pay attention on the opening and
closing brackets. On RStudio you can track the opening/closing brackets
letting your text cursor on it. It is a good programming skill to keep
the indentation of the script growing up as it goes deeper on the if/for
structures and, of course, comment your code!

Simulating Data
===============

About it
========

We are currently writing this course, if you find any mistake (including
misspelling ones) or want to add something else please drop us an email
at *rramadeu at gmail dot com*. This material is written using
[RMarkdown](http://rmarkdown.rstudio.com/).

Good luck! Remember, we are here to help, but do your homework first. 
