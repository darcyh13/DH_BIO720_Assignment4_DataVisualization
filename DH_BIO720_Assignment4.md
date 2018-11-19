The world of data visualization
-------------------------------

Two basic types of data visualizations (R uses both) 1. Exploratory:
visualizations help us understand data -keep as much detail as possible

1.  Explanatory: visualizatons help us share our understanding with
    other people -requires you to make choices ( ex. what features do
    you want to highlight) and edit (ex. remove distracting features)

There is 4 graphic systems in R 1. Base Graphics: Easiest to learn 2.
Grid Graphics: powerful set of modules for building other tools. Offers
more power and flexibilty than base. Steeper learning curve and more
effort required. 3. Lattice Graphics:general purpose system based on
grid graphics. Allows you to make conditional scatter plots. 4. ggplot2:
"the grammar of graphics". you can add details and modify.

Creating an exploratory plot array
----------------------------------

    Deepsea2<-read.table("/Users/DarcyHenderson/Desktop/DeepSea2.txt", header = TRUE)
    str(Deepsea2)

    ## 'data.frame':    780 obs. of  12 variables:
    ##  $ SampleID   : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Station    : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Time       : int  3 3 3 3 3 3 3 3 3 3 ...
    ##  $ Latitude   : num  50.2 50.2 50.2 50.2 50.2 ...
    ##  $ Longitude  : num  -14.5 -14.5 -14.5 -14.5 -14.5 ...
    ##  $ Xkm        : num  -34.1 -34.1 -34.1 -34.1 -34.1 ...
    ##  $ Ykm        : num  16.8 16.8 16.8 16.8 16.8 ...
    ##  $ Month      : int  4 4 4 4 4 4 4 4 4 4 ...
    ##  $ Year       : int  2001 2001 2001 2001 2001 2001 2001 2001 2001 2001 ...
    ##  $ BottomDepth: int  3939 3939 3939 3939 3939 3939 3939 3939 3939 3939 ...
    ##  $ Season     : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Discovery  : int  252 252 252 252 252 252 252 252 252 252 ...

    plot(Deepsea2)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-1-1.png)

-   this plot is exploratory as it plots the entire DeepSea2 data frame
    and allows you too see what is important information and information
    that is not necessary to plot

Creating an explanatory scatterplot
-----------------------------------

    plot(x =Deepsea2$Station, y = Deepsea2$BottomDepth, xlab = " Station", ylab = " Bottom Depth")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-2-1.png)

-   this plot is explanatory as it plots information we have deemed
    important from the exploratory plot. It is a much more specific view
    and helps to show information we feel is important to view/share.

The plot() function is generic
------------------------------

-   plot is generic which means results depend on oject applied to it
-   above produced scatter but what happens if factor variable is passed
    through

<!-- -->

    microarraysample<-read.table("/Users/DarcyHenderson/Desktop/microarray_sample.txt", header = TRUE)
    plot(microarraysample$group)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-3-1.png)

-plot function produces bar plot

A preview of some more and less useful techniques
-------------------------------------------------

sunflowerplots
==============

-are good when numerical data points are repeated as scatter plots do
not show this - 1 petal = each repeated data point

Bloxplot
========

-used to show how the distrubution of a numerical varible changes over
the discrete levels of a categorical variable -also useful in showing
relationship between a numerical y variable that assumes many different
values and a numerical x variable that assumes only a few values

Mosaicplots
===========

-designed to show relationships between two categorical variables -but
can also be used to show relationships between two numerical variables
with few values

High level
==========

-example is plot

Low level
=========

-points(): adds points -lines(): adds lines -&gt; usually curved
-text(): adds labels

par(): sets many graphic parameters mfrow() : allows you to set up
multiple plot arrays

Adding details to a plot using point shapes, color, and reference lines
-----------------------------------------------------------------------

pch argument: can add different shapes col argument: can add different
colours points(): adds points to existing scatterplot aline(): adds
reference line

    source("http://www.openintro.org/stat/data/present.R") 


    str(present)

    ## 'data.frame':    63 obs. of  3 variables:
    ##  $ year : num  1940 1941 1942 1943 1944 ...
    ##  $ boys : num  1211684 1289734 1444365 1508959 1435301 ...
    ##  $ girls: num  1148715 1223693 1364631 1427901 1359499 ...

    plot( x= present$year, y= present$boys, pch = 17, col = "red")
    points(x= present$year, y= present$girls, pch = 16, col = "blue")
    abline(a = 0, b = 1, lty = 2)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-4-1.png)

Creating multiple plot arrays
-----------------------------

-when using plot() some options can or must be specified globally -other
options can only be specified locally

par(mfrow()):allows you to plot multiple graphs on a single pan

example: par(mfrow = c(1, 2)) creates a plot array with 1 row and 2
columns

    par(mfrow = c(1,2))

    plot(x = Deepsea2$SampleID, y = Deepsea2$Latitude)
    title("Original representation")

    plot(x = Deepsea2$SampleID, y = Deepsea2$Latitude, log = "xy")
    title("Log-log plot")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-5-1.png)

Avoid pie charts
----------------

-If you are thinking about using a pie chart, it is probably a bad idea

    par(mfrow = c(1,2))
    tbl <- sort(table(Deepsea2$Latitude),
                decreasing = TRUE)
    pie(tbl)
    title("Pie chart")

    barplot(tbl, las = 2, cex.names = 0.5)
    title("Bar chart")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-6-1.png)

The hist() and truehist() functions
-----------------------------------

    library(MASS)

    par(mfrow = c(1,2))
    hist(Deepsea2$BottomDepth, main = "hist() plot")

    truehist(Deepsea2$BottomDepth, main= "truehist() plot")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-7-1.png)

Density plots as smoothed histograms
------------------------------------

gives a better estimate of the density function for a random variable

    cars_df <- read.csv("/Users/DarcyHenderson/Desktop/cars.csv")

    index16 <- which(cars_df$Year == "70")

    HP_70 <- cars_df$Horsepower[index16]

    truehist(HP_70)
    lines(density(HP_70))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-8-1.png)

Using the qqPlot() function to see many details in data
-------------------------------------------------------

    library("car")

    ## Loading required package: carData

    qqPlot(HP_70)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-9-1.png)

    ## [1] 20  9

    qqPlot(Deepsea2$Time)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-9-2.png)

    ## [1] 78 79

-notice differences. -in plot with HP\_70 the Gaussian distribution
appears to be reasonable -in plot with Deepsea2 it is not reasonale

The sunflowerplot() function for repeated numerical data
--------------------------------------------------------

    par(mfrow = c(1,2))
    plot(Horsepower ~ Year, data = cars_df)
     title("Standard scatterplot")

     sunflowerplot(Horsepower ~ Year, data = cars_df)
     title("Sunflower plot")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-10-1.png)

-reinforces that scatterplots aren't the best choice when you have
repeated data points, as this isn't shown clearly -sunflowerplots are
able to show repeated data points

Useful options for the boxplot() function
-----------------------------------------

-varwidth allows for variable-width boxplots that show the different
sizes of the data subsets. -log allows for log-transformed y-values.
-las allows for more readable axis labels.

    boxplot( Horsepower ~ Year, 
      data = cars_df, 
      varwidth = T,
      log = "y",
      las = 1)

    title("Horsepower vs. Year")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-11-1.png)

-box plots that are wider are much larger subsets -in this examples they
are around the same size so subsets are around same size

Using the mosaicplot() function
-------------------------------

-scatterplot between categorical variables - useful in observing and
understanding relationship between numerical variables, that take only a
few different values

    mosaicplot(carb ~ cyl, 
      data = mtcars,
      color = T)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-12-1.png)

Using the bagplot() function
----------------------------

A single box plot gives a graphical representation of the range of
variation in a numerical variable, based on five numbers:

-The minimum and maximum values -The median (or "middle") value -Two
intermediate values called the lower and upper quartiles

library(aplpack)

par(mfrow = c(1,2))
boxplot(microarraysample*g*1, *m**i**c**r**o**a**r**r**a**y**s**a**m**p**l**e*g2)

bagplot(microarraysample*g*1, *m**i**c**r**o**a**r**r**a**y**s**a**m**p**l**e*g2,
cex = 1.20)

abline(0,1, lty = 2)

-problem loading aplpack package -cex makes point size larger

Plotting correlation matrices with the corrplot() function
----------------------------------------------------------

Correlation matrices are useful for obtaining a preliminary view of the
relationships between multiple numerical variables

-ellipses that are thin and elongated indicate a large correlation value
between the indicated variables -ellipses that are nearly circular
indicate correlations near zero

    library(corrplot)

    ## corrplot 0.84 loaded

    str(microarraysample)

    ## 'data.frame':    10 obs. of  6 variables:
    ##  $ g1   : num  0.5531 -0.0783 -0.1981 0.42 -0.0275 ...
    ##  $ g2   : num  -0.648 0.744 -0.744 -0.135 -1.309 ...
    ##  $ g3   : num  0.238 -0.453 1.88 -0.242 1.099 ...
    ##  $ g4   : num  0.115 -0.591 1.215 -0.239 1.084 ...
    ##  $ g5   : num  0.2 -0.315 -0.71 1.93 0.738 ...
    ##  $ group: Factor w/ 2 levels "cancer","healthy": 1 1 1 1 1 2 2 2 2 2

    col_numeric <- sapply(microarraysample, is.numeric)

    numericalVars <- microarraysample[,col_numeric]

    str(numericalVars)

    ## 'data.frame':    10 obs. of  5 variables:
    ##  $ g1: num  0.5531 -0.0783 -0.1981 0.42 -0.0275 ...
    ##  $ g2: num  -0.648 0.744 -0.744 -0.135 -1.309 ...
    ##  $ g3: num  0.238 -0.453 1.88 -0.242 1.099 ...
    ##  $ g4: num  0.115 -0.591 1.215 -0.239 1.084 ...
    ##  $ g5: num  0.2 -0.315 -0.71 1.93 0.738 ...

    corrMat <- cor(numericalVars)
    corrMat

    ##             g1          g2         g3         g4          g5
    ## g1  1.00000000  0.08402531 -0.1228094 -0.3784068  0.09647332
    ## g2  0.08402531  1.00000000 -0.2024758 -0.1776144 -0.41087142
    ## g3 -0.12280940 -0.20247584  1.0000000  0.9014782 -0.34419819
    ## g4 -0.37840683 -0.17761436  0.9014782  1.0000000 -0.26628671
    ## g5  0.09647332 -0.41087142 -0.3441982 -0.2662867  1.00000000

    corrplot(corrMat, method = "ellipse")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-13-1.png)

-g4 is correlated with g3

Building and plotting rpart() models
------------------------------------

-   decision trees represent a popular form of predictive model

<!-- -->

    library(rpart)

    tree_model <- rpart(medv ~ ., data = Boston)

    plot(tree_model)

    text(tree_model, cex = .7)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-14-1.png)

Introduction to the par() function
----------------------------------

parameters may be set by a call in the form par(name = value) where name
is the name of the parameter to be set and value is the value to be
assigned to this parameter.

    plot_pars <- par()
    names(plot_pars)

    ##  [1] "xlog"      "ylog"      "adj"       "ann"       "ask"      
    ##  [6] "bg"        "bty"       "cex"       "cex.axis"  "cex.lab"  
    ## [11] "cex.main"  "cex.sub"   "cin"       "col"       "col.axis" 
    ## [16] "col.lab"   "col.main"  "col.sub"   "cra"       "crt"      
    ## [21] "csi"       "cxy"       "din"       "err"       "family"   
    ## [26] "fg"        "fig"       "fin"       "font"      "font.axis"
    ## [31] "font.lab"  "font.main" "font.sub"  "lab"       "las"      
    ## [36] "lend"      "lheight"   "ljoin"     "lmitre"    "lty"      
    ## [41] "lwd"       "mai"       "mar"       "mex"       "mfcol"    
    ## [46] "mfg"       "mfrow"     "mgp"       "mkh"       "new"      
    ## [51] "oma"       "omd"       "omi"       "page"      "pch"      
    ## [56] "pin"       "plt"       "ps"        "pty"       "smo"      
    ## [61] "srt"       "tck"       "tcl"       "usr"       "xaxp"     
    ## [66] "xaxs"      "xaxt"      "xpd"       "yaxp"      "yaxs"     
    ## [71] "yaxt"      "ylbias"

    length(plot_pars)

    ## [1] 72

-simply shows what these graphics parameters are

Exploring the type option
-------------------------

-mfrow specifies the numbers of rows and columns in an array of plot
-values are two-element numerical vectors

values for how plot is made:

"p" for "points" "l" for "lines" "o" for "overlaid" (i.e., lines
overlaid with points) "s" for "steps"

    tb_rates<-read.csv("/Users/DarcyHenderson/Desktop/tb_rates.csv", header = TRUE)
    par(mfrow = c(2,2))

    plot(tb_rates$X2000, type = "p")
    title("points")

    plot(tb_rates$X2000, type = "l")
    title("lines")


    plot(tb_rates$X2000, type = "o")
    title("overlaid")

    plot(tb_rates$X2000, type = "s")
    title("steps")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-16-1.png)

The surprising utility of the type "n" option
---------------------------------------------

type = "n" -purposefor when plotting data from multiple sources on a
common set of axes - can compute ranges for the x- and y-axes so that
all data points will appear on the plot

    max_hp <- max(Cars93$Horsepower, mtcars$hp)
    max_mpg <- max(Cars93$MPG.city, Cars93$MPG.highway, mtcars$mpg)
    plot(Cars93$Horsepower, Cars93$MPG.city,
         type = "n", 
         xlim = c(0, max_hp),
         ylim = c(0, max_mpg), 
         xlab = "Horsepower",
         ylab = "Miles per gallon")

    points(mtcars$hp, mtcars$mpg, pch = 1)
    points(Cars93$Horsepower, Cars93$MPG.city, pch = 15)
    points(Cars93$Horsepower, Cars93$MPG.highway, pch = 2)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-17-1.png)

The lines() function and line types
-----------------------------------

    x <- seq(0, 10, length = 200)

    gauss1 <- dnorm(x, mean = 2, sd = 0.2)

    gauss2 <- dnorm(x, mean = 4, sd = 0.5)

    plot(x, gauss1, 
      type = "l",
      ylab = "Gaussian probability density")

    lines(x, gauss2, lty = 2, lwd = 3)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-18-1.png)

-shows what this bell curve looks like for exactly Gaussian data -shows
how the lines() function can be used to add lines to plot

-line types are set by the lty -lty = 1 specifying solid lines -lty = 2
specifying dashed lines -lty = 3 specifying dotted lines -lwd argument
specifies the width

The points() function and point types
-------------------------------------

    plot(mtcars$hp, mtcars$mpg,
      type='n',
      xlab = "Horsepower",
      ylab = "Gas mileage")

    points(mtcars$hp, mtcars$mpg, pch = mtcars$cyl)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-19-1.png)

    plot(mtcars$hp, mtcars$mpg, 
      type='n',
      xlab = "Horsepower",
      ylab = "Gas mileage")

    points(mtcars$hp, mtcars$mpg, pch = as.character(mtcars$cyl))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-19-2.png)

-first plot specifies the point shapes using numerical values of the pch
argument defined by the cyl variable in the mtcars data frame -The
second plot shows that pch can also be specified as a vector of single
characters, causing each point to be drawn as the corresponding
character

Adding trend lines from linear regression models
------------------------------------------------

abline() adds a straight line to an existing plot -line is specified by
an intercept parameter a and a slope parameter b -but can also specify
these parameters through a linear regression model that determines them
from data

1.generate a scatterplot of y versus x 2.then fit a linear model that
predicts y from x 3.call abline() to add this best fit line to the plot

    linear_model <- lm(Gas ~ Temp, data = whiteside)
    plot(whiteside$Temp, whiteside$Gas)
    abline(linear_model, lty = 2)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-20-1.png)
-dashed line shows general trend of data

Using the text() function to label plot features
------------------------------------------------

text() is used to add labels -x specifies the value for the x variable
-y specifies the value for the y variable -label specifies the label for
the x-y value pair

    plot(Cars93$Horsepower, Cars93$MPG.city, pch = 15)

    head(Cars93)

    ##   Manufacturer   Model    Type Min.Price Price Max.Price MPG.city
    ## 1        Acura Integra   Small      12.9  15.9      18.8       25
    ## 2        Acura  Legend Midsize      29.2  33.9      38.7       18
    ## 3         Audi      90 Compact      25.9  29.1      32.3       20
    ## 4         Audi     100 Midsize      30.8  37.7      44.6       19
    ## 5          BMW    535i Midsize      23.7  30.0      36.2       22
    ## 6        Buick Century Midsize      14.2  15.7      17.3       22
    ##   MPG.highway            AirBags DriveTrain Cylinders EngineSize
    ## 1          31               None      Front         4        1.8
    ## 2          25 Driver & Passenger      Front         6        3.2
    ## 3          26        Driver only      Front         6        2.8
    ## 4          26 Driver & Passenger      Front         6        2.8
    ## 5          30        Driver only       Rear         4        3.5
    ## 6          31        Driver only      Front         4        2.2
    ##   Horsepower  RPM Rev.per.mile Man.trans.avail Fuel.tank.capacity
    ## 1        140 6300         2890             Yes               13.2
    ## 2        200 5500         2335             Yes               18.0
    ## 3        172 5500         2280             Yes               16.9
    ## 4        172 5500         2535             Yes               21.1
    ## 5        208 5700         2545             Yes               21.1
    ## 6        110 5200         2565              No               16.4
    ##   Passengers Length Wheelbase Width Turn.circle Rear.seat.room
    ## 1          5    177       102    68          37           26.5
    ## 2          5    195       115    71          38           30.0
    ## 3          5    180       102    67          37           28.0
    ## 4          6    193       106    70          37           31.0
    ## 5          4    186       109    69          39           27.0
    ## 6          6    189       105    69          41           28.0
    ##   Luggage.room Weight  Origin          Make
    ## 1           11   2705 non-USA Acura Integra
    ## 2           15   3560 non-USA  Acura Legend
    ## 3           14   3375 non-USA       Audi 90
    ## 4           17   3405 non-USA      Audi 100
    ## 5           13   3640 non-USA      BMW 535i
    ## 6           16   2880     USA Buick Century

    index3 <- which(Cars93$Cylinders == 3)
    index3

    ## [1] 39 80 83

    text(x = Cars93$Horsepower[index3],
         y = Cars93$MPG.city[index3], 
         labels = Cars93$Make[index3], 
         adj = 0)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-21-1.png)

Adjusting text position, size, and font
---------------------------------------

-adj argument can change horizontal text placement -&gt; value between
0-1 -making adj (-) causes text to start to right of specified position
-making adj (+) causes text to start to left of specified postion

-cex scales the default text size -for example cex = 0.5 increases text
size by 50%

-font is used to specify text font -font = 1 is default -font = 2 is
bold -font = 3 is italic -font = 4 is bold and italic

    plot(Cars93$Horsepower, Cars93$MPG.city, pch = 1)

    index3 <- which(Cars93$Cylinders == 3)

    points(Cars93$Horsepower[index3], Cars93$MPG.city[index3], pch = 16)

    text(
      Cars93$Horsepower[index3], 
      Cars93$MPG.city[index3], 
      Cars93$Make[index3], 
      adj = -0.2,
      cex = 1.2,
      font = 4)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-22-1.png)

-label is much more clear with adjustments

Rotating text with the srt argument
-----------------------------------

-srt argument allows you to rotate the text srt = 90 causes the text to
be rotated 90 degrees counter-clockwise

    plot(whiteside$Temp, whiteside$Gas, pch=17)

    indexB <- which(whiteside$Insul == "Before")

    indexA <- which(whiteside$Insul == "After")

    text(x = whiteside$Temp[indexB], y = whiteside$Gas[indexB],
         labels = "Before", col = 'blue', srt = 30, cex = .8)

    text(x = whiteside$Temp[indexA], y = whiteside$Gas[indexA],
         labels = "After", col = 'red', srt = -20, cex = .8)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-23-1.png)

Using the legend() function
---------------------------

legends() adds explanatory text to a plot

    plot(whiteside$Temp, whiteside$Gas,
         type = "n", 
         xlab = "Outside temperature",
         ylab = "Heating gas consumption")

    indexB <- which(whiteside$Insul == "Before")

    indexA <- which(whiteside$Insul == "After")

    points(whiteside$Temp[indexB], whiteside$Gas[indexB], pch = 17)

    points(whiteside$Temp[indexA], whiteside$Gas[indexA], pch = 1)

    legend("topright", pch = c(17, 1), legend = c("Before", "After"))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-24-1.png)

Adding custom axes with the axis() function
-------------------------------------------

When you want to add custom axes you need to: 1. suppress default axes
2. call function axis()

The side argument tells the function which axis to create -value of 1
adds an axis below the plot -2 adds an axis on the left -3 puts it
across the top -4 puts it on the right side.

-at is a vector that defines points where tick-marks will be drawn on
the axis

-labels is a vector that defines labels at each of these tick-marks

    boxplot(sugars ~ shelf, data = UScereal, axes = F)

    axis(side = 2)

    axis(side = 1, at = c(1,2,3))

    axis(side = 3, at = c(1,2,3),
         labels = c("floor","middle","top"))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-25-1.png)

Using the supsmu() function to add smooth trend curves
------------------------------------------------------

sometimes scatterplots show trends that are not linear, so what do you
do?

-supsmu() allows for a curved line to be added

-The bass argument controls the degree of smoothness in the resulting
trend curve

    plot(Cars93$Horsepower, Cars93$MPG.city)

    trend1 <- supsmu(Cars93$Horsepower, Cars93$MPG.city)

    lines(trend1)

    trend2 <- supsmu(Cars93$Horsepower, Cars93$MPG.city, bass = 10)

    lines(trend2, lty = 3, lwd = 2)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-26-1.png)

Too much is too much
--------------------

when you use the plot() function to a data frame with many columns, it
will generate an enormous array of scatterplots that are small and not
useful

    ncol(Deepsea2)^2

    ## [1] 144

    plot(Deepsea2)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-27-1.png)

Deciding how many scatterplots is too many
------------------------------------------

-multiple plot arrays can be extremely helpful in illustrating: 1.
difference between datasets 2. different views of same dataset
3.similarities between datasets 4.related views of the same dataset

matplot() generates a plot with several scatterplots on the same set of
axe

    keep_vars <- c("calories", "protein", "fat",
                   "fibre", "carbo", "sugars")

    df <- UScereal[, keep_vars]
    str(df)

    ## 'data.frame':    65 obs. of  6 variables:
    ##  $ calories: num  212 212 100 147 110 ...
    ##  $ protein : num  12.12 12.12 8 2.67 2 ...
    ##  $ fat     : num  3.03 3.03 0 2.67 0 ...
    ##  $ fibre   : num  30.3 27.3 28 2 1 ...
    ##  $ carbo   : num  15.2 21.2 16 14 11 ...
    ##  $ sugars  : num  18.2 15.2 0 13.3 14 ...

    par(mfrow = c(2,2))

    matplot(
      UScereal$calories, 
      UScereal[,c('protein', 'fat')], 
      xlab = "calories",
      ylab = "")

    title("Two scatterplots")

    matplot(
      UScereal$calories, 
      UScereal[,c('protein', 'fat', 'fibre')], 
      xlab = "calories",
      ylab = "")

    title("Three scatterplots")

    matplot(
      UScereal$calories, 
      UScereal[,c('protein', 'fat', 'fibre', 'carbo')], 
      xlab = "calories",
      ylab = "")

    title("Four scatterplots")

    matplot(
      UScereal$calories, 
      UScereal[,c('protein', 'fat', 'fibre', 'carbo','sugars')], 
      xlab = "calories",
      ylab = "")

    title("Five scatterplots")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-28-1.png)

-   as you can see in this adding to many scatterplots is not useful

How many words is too many?
---------------------------

-scatterplot arrays can become not useful if they become too complex

wordcloud() is a function that is used to create wordclouds -present
words in varying sizes depending on their frequency -called with
character vector of words and second numerical vector giving the number
of times each word appears

-scale argument is a two-component numerical vector giving the relative
size of the largest word in the display and that of the smallest word
-wordcloud only includes those words that occur at least min.freq times
in the collection and the default value for this argument is 3

    library(wordcloud)

    ## Loading required package: RColorBrewer

    mfr_table <- table(Cars93$Manufacturer)

    wordcloud(
      words = names(mfr_table), 
      freq = as.numeric(mfr_table), 
      scale = c(2, 0.25))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-29-1.png)

    wordcloud(
      words = names(mfr_table), 
      freq = as.numeric(mfr_table), 
      scale = c(2, 0.25),
      min.freq = 1)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-29-2.png)

    model_table <- table(Cars93$Model)

    wordcloud(
      words = names(model_table), 
      freq = as.numeric(model_table), 
      scale = c(.75, .25), 
      min.freq = 1)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-29-3.png)

The Anscombe quartet
--------------------

-datasets can appear very similar when comparing summary statistics

The utility of common scaling and individual titles
---------------------------------------------------

-you can see the differences in these datasets if you plot scatterplots
with the same x and y ranges

Using multiple plots to give multiple views of a dataset
--------------------------------------------------------

-multiple plot arrays also let you see multiple related views of the
same dataset -gives a deeper understanding of a data variable

Constructing and displaying layout matrices
-------------------------------------------

-layout() function creates plot array -0 represents empty space and
other numbers represent the plot number ex. a 1 in the layout matrix
reders to the visualization that was first called

-create matrix with three rows and two columns -1st row is empty plot to
the left and plot 1 to the right -2nd row is plot 2 to the left and
empty plot to right -3rd row is empty plot to ledt and plot 3 to right

    layoutMatrix <- matrix(
      c(
        0, 1,
        2, 0,
        0, 3
      ), 
      byrow = T, 
      nrow = 3
    )

    layout(layoutMatrix)

    layout.show(n = 3)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-30-1.png)

Creating a triangular array of plots
------------------------------------

-can create three differnt views of data.frame -sometimes it is not
possible to construct a plot array using the mfrow parameter(as it is
used for rectangular arrays only)

    layout(layoutMatrix)

    indexB <- which(whiteside$Insul == "Before")
    indexA <- which(whiteside$Insul == "After")

    plot(whiteside$Temp[indexB], whiteside$Gas[indexB],
         ylim = c(0,8))
    title("Before data only")


    plot(whiteside$Temp, whiteside$Gas,
         ylim = c(0,8))
    title("Complete dataset")

    plot(whiteside$Temp[indexA], whiteside$Gas[indexA],
         ylim = c(0,8))
    title("After data only")

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-31-1.png)

Creating arrays with different sized plots
------------------------------------------

-layout() can be used to create plot arrays with different sized
component plots

    row1 <- c(1,0,0)
    row2 <- c(0,2,2)
    layoutVector <- c(row1,row2, row2)

    layoutMatrix <- matrix(layoutVector, byrow = T, nrow = 3)

    layout(layoutMatrix)

    plot(Boston$rad, Boston$zn)

    sunflowerplot(Boston$rad, Boston$zn)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-32-1.png)

Some plot functions also return useful information
--------------------------------------------------

-barplot() returns a numerical vector with the center position of each
bar in the plot -this vector is normally returned invisibly but you can
observe it -this vector is useful when you want to overlay text on the
bars of a horixontal barplot

    tbl <- table(Cars93$Cylinders)

    mids <- barplot(tbl, 
      horiz = T,
      col = "transparent",
      names.arg = "")

    text(20, mids, names(tbl))
    text(35, mids, as.numeric(tbl))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-33-1.png)

Using the symbols() function to display relations between more than two variables
---------------------------------------------------------------------------------

-symbols() allows you to show influence of other variables -x and y
define scatterplot -circles argument creates bubbleplot -each data point
is represented by a circle whose radius depends on the third variable

    symbols(Cars93$Horsepower, Cars93$MPG.city,
            circles = sqrt(Cars93$Price))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-34-1.png)

    symbols(Cars93$Horsepower, Cars93$MPG.city,
            circles = sqrt(Cars93$Price),
            inches = 0.1)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-34-2.png)

-notice differences in size of circles

Saving plot results as files
----------------------------

-png() function sets the name of the png file to be generated and sets
up a special environment that captures all graphical output until you
exit environment with the dev.off() command

Iliinsky and Steele's 12 recommended colors
-------------------------------------------

IScolors &lt;- c("red", "green", "yellow", "blue", "black", "white",
"pink", "cyan", "gray", "orange", "brown", "purple")

Using color to enhance a bubbleplot
-----------------------------------

-colour can be used in bubbleplots to illustrate differences

    IScolors <- c("red", "green", "yellow", "blue",
                  "black", "white", "pink", "cyan",
                  "gray", "orange", "brown", "purple")
    cylinderLevel <- as.numeric(Cars93$Cylinders)

    symbols(
      Cars93$Horsepower, Cars93$MPG.city, 
      circles = as.numeric(Cars93$Cylinders), 
      inches = 0.2, 
      bg = IScolors[cylinderLevel])

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-35-1.png)

Using color to enhance stacked barplots
---------------------------------------

-Stacked bar plots can be made using the barplot() -each bar in the plot
is partitioned into segments characterizing portions of the data
characterized by the bar

    tbl <- table(Cars93$Cylinders, Cars93$Origin)
    barplot(tbl)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-36-1.png)

    barplot(tbl, col = IScolors)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-36-2.png)

-notice difference when using colour

The tabplot package and grid graphics
-------------------------------------

-tablot is a package that allows you to use grid graphics -tableplot()
allows you to visualize data distributions and relationships between
variables in large data sets -&gt; constructs side by side horizonatal
barplots, for each variable -&gt; works best for viewing up to 10

A lattice graphics example
--------------------------

-built on grid graphics -lattice graphics and base graphics are similar
functions but can produce very different results -lattice graphics
supports conditional plots -&gt; show relationships between variables
within different groups

    library(lattice)
    calories_vs_sugars_by_shelf <- calories ~ sugars | shelf
    xyplot(calories_vs_sugars_by_shelf, data = UScereal)

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-37-1.png)

A ggplot2 graphics example
--------------------------

-grid graphics -based on the grammar of graphics -&gt; approach to
building and changing graphical displays. Start with basics and add to
it through use of modifiers

    library(ggplot2)

    basePlot <- ggplot(Cars93, aes(x = Horsepower, y = MPG.city))

    basePlot + 
      geom_point()

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-38-1.png)
- This is basic plot -can now add to it

     basePlot + 
      geom_point(colour = IScolors[Cars93$Cylinders])

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-39-1.png)
-adds colour

      basePlot + 
      geom_point(colour = IScolors[Cars93$Cylinders], 
                 size = as.numeric(Cars93$Cylinders))

![](DH_BIO720_Assignment4_files/figure-markdown_strict/unnamed-chunk-40-1.png)
-makes point size vary

Why Base R?
-----------

-flexible -good for exploratory analysis -easy to learn

Why Use Grid Graphics?
----------------------

-greater control over low level graphical details -more flexible than
base graphics -comes at cost of steep learning curve
