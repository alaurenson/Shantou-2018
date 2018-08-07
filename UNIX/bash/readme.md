## A crash-course in bash
----
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

#### Now that we've downloaded the files, let's get started. We're going to work through the first several exercises together. My goal is to have us finish Part 1 today in class.

1. Navigate (as you normally would) to the folder we just downloaded - go into "Unix_and_Perl_course", and open the pdf file "unix_and_perl_primer_v3.1.2.pdf"

2. Go to p.13, and follow exercises U1, U2, U3, and U4

3. Because we downloaded the folder directly, our data isn't where exercise U5 says it is. 

The PDF will continually refer to /Volumes/USB/Unix_and_Perl_course - 

**our file is located at /Desktop/Shantou_2018/bash_practice/Unix_and_Perl_course**. 

Going forward, you can follow the exercises without a problem, just remember where our file is! This is good practice for developing your directory awareness.

Instead of U5, open a new terminal window and type the following:
```
# Change to the desired directory
cd Desktop/Shantou_2018/bash_practice/Unix_and_Perl_course

# Check the contents of that directory
ls

# Check your "present working directory"
pwd
```

4. From here, we should be able to continue together from U6 onward - hopefully we can get to U36!

I realize there are a lot of commands to learn: don't worry about memorizing them - I promise that you will eventually learn them through use!

----

### Futher reading & additional resources
Part 2 of the Unix and Perl Primer is very useful; if you can get up through at least U45, and tell me what the following command does, I'll be extremely impressed. NOT REQUIRED.
```
# This is from U45 - it's cut off in the PDF; this is the full command:
$ tr '\n' '@' < intron_IME_data.fasta | sed 's/>/#>/g' | tr '#' '\n' | grep "i1_.*5UTR" | sort -nk 3 -t "_" | head -n 5 | tr '@' '\n'
``` 

