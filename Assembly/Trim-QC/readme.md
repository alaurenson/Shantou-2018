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
Cool. Onward!

You'll each recieve a set of raw reads, the file will be called something like this:
> Akle_TTAGGC_L004_R1_001.fastq.gz

This example will reflect THIS filename. Make sure when you're working to use YOUR file instead.

Next, use FastQC to generate a quality report. Navigate in your terminal to the directory with your fastq file and do the following:
```
$ ~/Desktop/bio_software/FastQC/fastqc ./Akle_TTAGGC_L004_R1_001.fastq.gz
```
When complete, two files will be generated, a .html and a .zip. Open the .html file in your browser (by double-clicking, wherever you have it saved!)

Now we'll go through and compare our results.

----

### 2. Trimming with bbduk

This involves two steps: trimming adapters, and removing low quality sequence.

In the terminal, navigate to wherever your raw file is, and do the following:
```
# Remove any identified adapter sequences - bbduk has an internal database of common adapters that it checks against.
# "in" is set to my reads file (exactly as I recieved it). You need to alter this to reflect your file.
# "out" is set as "temp.fastq", for "temporary". You may leave this as it is, or change it.
# "ref" is the "reference" that bbduk uses to identify adapter sequence.
# The other parameters are explained in the bbduk manual, link below.

$ ~Desktop/bio_software/bbmap/bbduk.sh -Xmx1g in=Akle_TTAGGC_L004_R1_001.fastq.gz out=temp.fastq ref=~Desktop/bio_software/bbmap/resources/adapters.fa ktrim=r k=23 mink=11 hdist=1 tpe tbo

# Remove low-quality sequences/
# "in" is set to the outfile from the previous step, "temp.fastq"
# "out" is set to a a new fastq file beginning with "trimmed", so we can tell it apart from the raw file.
# The other parameters are explained in the bbduk manual, link below.

$ ~Desktop/bio_software/bbmap/bbduk.sh -Xmx1g in=temp.fastq out=trimmed_Akle_TTAGGC_L004_R1_001.fastq qtrim=rl trimq=10
```

[BBDuk guide](https://jgi.doe.gov/data-and-tools/bbtools/bb-tools-user-guide/bbduk-guide/)

----

### 3. Run FastQC on the trimmed data

Now, like you did in step 1, **run FastQC on your new trimmed file.**

(Note - You don't need to set the permission again, you already did that!)

----

### 4. Compare the FastQC reports for the raw and trimmed data; what differences can you see?
