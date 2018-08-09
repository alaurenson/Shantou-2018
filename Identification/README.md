**UNDER CONSTRUCTION**


Identification
----

### [The BLAST Manual](https://www.ncbi.nlm.nih.gov/books/NBK1762/)

#### BLAST+
NCBI BLAST+ is available in the repositories from most Linux distributions and so can be installed in the same way as any other package. For example, on Ubuntu, Debian, Linux Mint:

```
sudo apt-get install ncbi-blast+
```

Alternatively, instructions are provided for installing BLAST+ on Mac, Windows, and various flavours of Linux on the "Standalone BLAST Setup for Windows/Mac/Unix" page of the BLAST+ Help manual [here](http://www.ncbi.nlm.nih.gov/books/NBK1762/). Follow the instructions under "Configuration" in the BLAST+ help manual to add BLAST+ to the PATH environment variable.

The download itself may be found [here](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download).

In addition to the software, you'll want to download the "non-redundant blast database"; this is a list of every sequence that NCBI has accrued. There are a lot. This is a big file. All of this might take a little while. 

```
# Make a new directory for blast stuff
$ mkdir ~/Desktop/blast; cd ~/Desktop/blast

# Download the nr database
$ sudo wget ftp://ftp.ncbi.nlm.nih.gov/blast/db/FASTA/nr.gz

# Unzip
$ gunzip nr.gz
```

It's possible to download only portions of the nr by pasting the following in your browser:
> ftp://ftp.ncbi.nlm.nih.gov/blast/db/ 

I may decide that this is more appropriate, depending on how long downloads are taking.

----

**Add: blasting selections of contigs**
