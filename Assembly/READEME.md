## Assembly

The first step in many bioinformatic pipelines is to assemble your raw sequencer output into workable data. We'll begin by obtaining all of the necessary software.

----

### Software & Dependencies  
#### Most programs that we'll use rely on other software in order to run properly. You probably have some or all of them already. 
 
- [Python]()
- [Java Runtime Environment (JRE)](https://www.java.com/en/)
- [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

To check whether you have them:
```
# For Python, you'll notice the command line change from bash's '$' to Python's '>>>'. Type quit() to exit the Python prompt.
$ python
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

- To obtain reports about the quality of our sequence data: [FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- To clean up our raw data prior to assembly: [Trimmomatic](http://www.usadellab.org/cms/index.php?page=trimmomatic)
- To assemble our cleaned-up data: [RNAspades](http://cab.spbu.ru/software/rnaspades/)

----
