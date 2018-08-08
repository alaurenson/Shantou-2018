## A crash-course in R

#### R is a statistical programming language used for many purposes. For data-exploration and plotting figures, it's nearly unparalleled. 

Today, we're going to download R and the associated IDE (Integrated Development Environment) called R Studio - with these, we'll work through a tutorial, and then get our first look at the data we'll be using for the remainder of the course. 

Once we finish this, you'll have enough of a background that we can properly begin our analysis!

----

### Installation of R:

For [Windows](https://cran.rstudio.com/bin/windows/)
1. Follow the link, and click 'base', then click 'Download R 3.5.1 for Windows'
2. When the download completes, open the the executable setup file, R-3.5.1-win. 
3. Follow the on-screen prompts and install using default settings

For [Mac](https://cran.rstudio.com/bin/macosx/)
1. Follow the link, and click on the most recent version (R-3.5.1.pkg)
2. When the download completes, open the .pkg file
3. Follow the on-screen prompts and install using default settings

For Linux, it's a little more complicated. Maybe.

[Here](https://cran.rstudio.com/bin/linux/) is the official page that lists the software for each of the four major linux distributions. You don't need to click this yet. 

First, check if R came with your version of Linux. This happens sometimes.
Open a terminal and type 'R':
```
R
```
If you hit enter, and it says "R version... etc...", **and** it's v3.1.0 or greater, and your cursor looks like >, then congrats! You're done. 
 
If not, you'll need to install it through the terminal. My instructions below should work for Ubuntu. Please ask for help if something isn't working!

In your terminal:
```
# Get your linux version - note this! You'll need it in the next step
cat /etc/*release

# Add an external repository (maintained by CRAN, to keep your software up-to-date)
# !!! Replace ubuntu and YOUR_VERSION/ below with your distro and version. e.g. ubuntu lucid/
sudo sh -c 'echo "deb http://cran.rstudio.com/bin/linux/ubuntu YOUR_VERSION/" >> /etc/apt/sources.list'

# Send key to CRAN server
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

# Update packages
sudo apt-get update

# (Finally) install R
sudo apt-get install r-base-dev
```

### Installation of R studio

Go [here](https://www.rstudio.com/products/rstudio/download/), and find your operating system under "Installers" near the bottom of the page.  

Download your installer, and follow the on-screen prompts using default settings. 

----

### Installing swirl(), the tutorial package
