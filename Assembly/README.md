## Trimming, QC, Assembly

The first step in many bioinformatic pipelines is to assemble your raw sequencer output into workable data. Unless you've opted to pay for pre-trimmed sequence, there are a couple of (easy) steps to take that will ensure your assembly most accurately reflects the true sequence of the organism. 

We'll begin, as usual, by obtaining all of the necessary software.

----

### Software & Dependencies  
#### Most programs that we'll use rely on other software in order to run properly. You probably have some or all of them already. 
 
- [Python]()
- [Java Runtime Environment (JRE)](https://www.java.com/en/)
- [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

To check whether you have them:
```
# For Python, you'll notice the command line change from bash's '$' to Python's '>>>'. 
$ python

# Type quit() to exit the Python prompt.
>>> quit()
```
```
# For JRE/JDK, if installed you'll see the 'help' page in your terminal. If not, you'll see nothing happen.
# JRE
$ java -version

# For JDK
$ javac
```
If you're missing any of them, please follow the above links and install them!

#### Now that we have all of our dependencies installed, we'll download the programs that actually perform the analysis and assembly. 

The method I use in dealing with bioinformatic software is to save all of my software downloads to a single directory. This is nice for a few reasons:

1. You'll always know where the software is
2. You can call processes directly from that location no matter what your present working directory
3. You need not worry about random programs piling up deep in your computer

So - let's download our first three pieces of software. Follow the links and download all three program files into a directory. 

- To obtain reports about the quality of our sequence data: [FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- To clean up our raw data prior to assembly: BBduk, part of [BBmap](https://sourceforge.net/projects/bbmap/)
- To assemble our cleaned-up data: [RNAspades](http://cab.spbu.ru/software/rnaspades/)

----
