## Assembly

The first step in many bioinformatic pipelines is to assemble your raw sequencer output into workable data. 

----

### Software & Dependencies  
Most programs that we'll use rely on other software in order to run properly. You probably have some or all of them already. 
 
- [Python]()
- [Java Runtime Environment (JRE)](https://www.java.com/en/)
- [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

To check whether you have them:
```
# 1. For Python
$ python
>>> quit()

# 2. For JRE
$ java -version

# 3. For JDK
$ javac
```
For Python, you'll notice the command line change from bash's '$' to Python's '>>>'. Type quit() to exit the Python prompt. 

For JRE/JDK, if installed you'll see the 'help' page in your terminal. If not, you'll see nothing happen. 

If you're missing any of them, please follow the above links and install them!

#### Now that we have all of our dependencies installed, we'll download the programs that actually perform the analysis and assembly. 

- For Windows, use [winSCP](https://winscp.net/eng/download.php)
- For Mac & Linux, use [CyberDuck](https://cyberduck.io)

----
