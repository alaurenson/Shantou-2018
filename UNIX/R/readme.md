## A crash-course in R

#### R is a statistical programming language used for many purposes. For data-exploration and plotting figures, it's nearly unparalleled. 

Today, we're going to download R and the associated IDE (Integrated Development Environment) called R Studio - with these, we'll work through a tutorial, and then get our first look at the data we'll be using for the remainder of the course. 

Once we finish this, you'll have enough of a background that we can properly begin our analysis!

### Installation of R:

For [Windows](https://cran.rstudio.com/bin/windows/)
1. Follow the link, and click 'base', then click 'Download R 3.5.1 for Windows'
2. When the download completes, open the the executable setup file, R-3.5.1-win. 
3. Follow the on-screen prompts and install using default settings

----

For [Mac](https://cran.rstudio.com/bin/macosx/)
1. Follow the link, and click on the most recent version (R-3.5.1.pkg)
2. When the download completes, open the .pkg file
3. Follow the on-screen prompts and install using default settings

----

For Linux, it's a little more complicated. Maybe.

[Here](https://cran.rstudio.com/bin/linux/) is the official page that lists the software for each of the four major linux distributions. You don't need to click this yet. 

First, check if R came with your version of Linux. This happens sometimes.
Open a terminal and type `R`

If you hit enter, and it says "R version... etc...", **and** it's v3.1.0 or greater, and your cursor looks like >, then congrats! You're done. 
 
If not, you'll need to install it through the terminal. My instructions below should work for Ubuntu. Please ask for help if something isn't working!

In your terminal:
```
# Get your linux version - note this! You'll need it in the next step
$ cat /etc/*release

# Add an external repository (maintained by CRAN, to keep your software up-to-date)
# !!! Replace ubuntu and YOUR_VERSION/ below with your distro and version. e.g. ubuntu lucid/
$ sudo sh -c 'echo "deb http://cran.rstudio.com/bin/linux/ubuntu YOUR_VERSION/" >> /etc/apt/sources.list'

# Send key to CRAN server
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

# Update packages
$ sudo apt-get update

# (Finally) install R
$ sudo apt-get install r-base-dev
```
----

### Installation of R studio

Go [here](https://www.rstudio.com/products/rstudio/download/), and find your operating system under "Installers" near the bottom of the page.  

Download your installer, and follow the on-screen prompts using default settings. 

----

### Install and run [swirl()](https://swirlstats.com), the tutorial package

For Windows and Mac:

1. Open R Studio
2. In the R console, type the following commands:
```
# Note that R's console uses '>' rather than Bash's '$'
# Also note that this scheme is how we install and use all packages in R. 

> install.packages("swirl")
> library("swirl")
> swirl()
```

For Linux:
1. Open a normal terminal, type the following:
```
# Install RCurl, which is an R package that allows for internet downloads

$ sudo apt-get install libcurl4-openssl-dev
```
2. Open R Studio
3. In the R console, type the following commands:
```
# Note that R's console uses '>' rather than Bash's '$'
# Also note that this scheme is how we install and use all packages in R. 

> install.packages("swirl")
> library("swirl")
> swirl()
```
----
----

Now that we've installed everything, we'll work through some of the swirl exercises to get a feel for how R works. 

Everyone do the following:
1. Type `swirl()` into the command line and press enter
2. Follow the prompts until we see:
```
...

| To begin, you must install a course. I can install a course for you from the
| internet, or I can send you to a web page
| (https://github.com/swirldev/swirl_courses) which will provide course options
| and directions for installing courses yourself. (If you are not connected to
| the internet, type 0 to exit.)

1: R Programming: The basics of programming in R
2: Regression Models: The basics of regression modeling in R
3: Statistical Inference: The basics of statistical inference in R
4: Exploratory Data Analysis: The basics of exploring data in R
5: Don't install anything for me. I'll do it myself.
```
3. Type `1` and press enter. When you see this:
```
| Please choose a lesson, or type 0 to return to course menu.

 1: Basic Building Blocks      2: Workspace and Files     
 3: Sequences of Numbers       4: Vectors                 
 5: Missing Values             6: Subsetting Vectors      
 7: Matrices and Data Frames   8: Logic                   
 9: Functions                 10: lapply and sapply       
11: vapply and tapply         12: Looking at Data         
13: Simulation                14: Dates and Times         
15: Base Graphics
```
4. Type `1` again. We're starting at the beginning and working our way through these exercises together. These will help us get comfortable with the R environment. 

----

If we can get through all of this with time to spare, I'll show you how to use R to view your own data! 

Throughout this course, we'll use R for a variety of things. Database management and generating plots are the big ones. 

----

### Further exercises

This isn't required, but if you want additional practice, then swirl() topic **4: Exploratory Data Analysis** is well worth your time. 

You can access it like this:

```
> library("swirl")
> install_course("Exploratory_Data_Analysis")
> swirl()
> 2         # "No. Let me start something new."
> 1         # "Exploratory Data Analysis"
```

The [Swirl course repository](https://github.com/swirldev/swirl_courses) has a number of good lessons, if you find yourself wanting to learn R more thoroughly. 
