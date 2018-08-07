## A crash-course in bash

#### We'll begin our work by working through some exercises developed by Keith Bradnam and Ian Korf at UC Davis. This will help you get comfortable in a UNIX working environment, and ensure that we're all starting from the same place.

There are two ways you can download the files:

1. Follow this link: [Unix and Perl Primer for Biologists - v3.1.2](http://korflab.ucdavis.edu/Unix_and_Perl/index.html). From there, scroll down to v3.1.2, and download "all course material". Unzip the file. 

2. If you want to jump right in, open a new terminal window and type the following to achieve the same thing:
```
# NOTE: This is a code block. This is how I'll share commands!
# All comments will start with "#", don't type out comments - these are for your understanding.
# All commands should be typed as a single line - press enter or return to execute the command, then go to the next line. 

# Change directory to your desktop
cd ~/Desktop

# Make a directory called "Shantou_2018", and move into that directory
mkdir Shantou_2018; cd Shantou_2018

# Make a directory called "bash_practice", and move into that directory
mkdir bash_practice; cd bash_practice 

# Download "this" from the internet
wget "http://korflab.ucdavis.edu/Unix_and_Perl/current.zip"

# Look at what's in the directory
ls

# Unzip the file
unzip current.zip

# Remove the .zip file
rm current.zip
```

Notice, the bash commands do exactly the same thing! It's just a different way of navigating your computer. I promise that after some practice, you'll find yourself using bash often because of how convenient it is - even when you're not doing bioinformatic work.

#### Now that we've downloaded the files, let's get started. We're going to work through the first several exercises together. My goal is to have us finish Unit 1 today. 
