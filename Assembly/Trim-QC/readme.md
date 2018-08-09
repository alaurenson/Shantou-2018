QC, Trimming, and QC again!
----

This effectively represents the beginning of any analysis of NGS (Next-Generation Sequencing) data. 

Whether you are looking for differential gene expression in a de-novo transcriptome assembly, or doing a reference-guided genome assembly - any time you recieve sequence data, each sequence will contain a portion derived from the adapters used in sequencing. We need to get rid of these. This is called "trimming". 

In addition, sequencer output files (in fastq format) are accompanied by quality scores. We also want to remove reads that are below acceptible quality thresholds to ensure that our data is biologically accurate. 

----

This is an example of raw output:
```
@HWI-1KL118:98:C374TACXX:4:1101:1247:2191 1:N:0:TTAGGC
CCTGCATGTGGCAAGTCTGTGCCCTGACCAGTGGTGCGAGGTGACATGAGCCGCTCACGAGTTGCAGGATCCGTACTTTCCTTTGCTGGAATGACAATGGT
+
BCCFFFFFHHHHHJJHJHEHHIIJIHIIIIJIJJFHIIIJJ?FHIIIJIIJJJJIJJHHHF?BEFEEECEDCBBBDBFEDDDDDCDDDDBDDDDDDDDDDC
```

Essentially, this is what it says:
```
@Instrument_name:Run_ID:Flow-cell_ID:Lane:Tile:X_and:Y_coord_of_tile Pair-member:Filtered?:Controlled?:Index
[Sequence]
+
[Scores]
```

Here, each character in the score line represents a value of certainty for the accuracy of the base call. Different sequencing protocols have different notation, but in this example the scores are stronger later in the alphabet, and symbols are weakest. Thus J is good, B or ? is not so good. 

A good trimming program will take the whole score into account, and use the average to decide whether or not to keep the read. 

----

To demonstrate the neccesity of working with clean data, we are going to do the following:
1. Use FastQC to assess the overall quality of a raw dataset
2. Use BBDuk to trim out adapter sequences and low-quality reads
3. Use FastQC to check the newly-trimmed dataset's overall quality. 

In the next section, we'll use RNASpades to assemble the trimmed dataset.

----

### 1. FastQC with raw data
Set a permission. The fastqc program can be used many ways. Because we're going to run it directly, we need to set an "execute" permission. 
```
# Navigate into the FastQC software directory
$ cd ~/Desktop/bio_software/FastQC

# Look at what's there
$ ls -l

# Notice that "fastqc" has a permission line like this: -rw-r--r--. It's not executable. Make it executable
$ chmod u+x fastqc

# Check if it worked
$ ls -l

# Now the permissions line should look like this: -rwxr--r--. That "x" makes all the difference. 
```
Cool, onward!

You'll each recieve a set of raw reads, the file will be called something like this:
> Akle_TTAGGC_L004_R1_001.fastq.gz

Next, use FastQC to generate a quality report. Navigate in your terminal to the directory with your fastq file and do the following:
```
$ ~/Desktop/bio_software/FastQC/fastqc ./Akle_TTAGGC_L004_R1_001.fastq.gz
```

When complete, two files will be generated, a .html and a .zip. Open the .html file in your browser (by double-clicking, wherever you have it saved!)

Now we'll go through and compare our results.

### 2. Trimming with bbduk

This involves two steps: trimming adapters, and removing low quality sequence. 

In the terminal, navigate to wherever the raw file is, and do the following:

```
$ ~/software/bbmap/bbduk.sh -Xmx1g in=Akle_TTAGGC_L004_R1_001.fastq.gz out=temp.fastq ref=~/software/bbmap/resources/adapters.fa ktrim=r k=23 mink=11 hdist=1 tpe tbo

$ ~/software/bbmap/bbduk.sh -Xmx1g in=temp.fastq out=trimmed_Akle_TTAGGC_L004_R1_001.fastq qtrim=rl trimq=10
```




