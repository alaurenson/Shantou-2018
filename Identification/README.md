### Identification: BLAST+ (Basic Local Alignment Search Tool)

#### [The BLAST Guide](https://www.ncbi.nlm.nih.gov/books/NBK1762/)

> Add: Links to Altschul papers

> Add: Flavors of Blast

> Add: Black Box vs. Manual runs, advantages and disadvantages of both

----

### Installation and Instruction for Manual Opperation

*I'm including this for your future perusal! In class we'll actually be using the black-box method.* 

NCBI BLAST and its several variants are available in the repositories from most Linux distributions and so can be installed in the same way as any other package. For example, on Ubuntu, Debian, Linux Mint:

```
sudo apt-get install ncbi-blast+
```

Alternatively, instructions are provided for installing BLAST+ on Mac, Windows, and various flavours of Linux on the "Standalone BLAST Setup for Windows/Mac/Unix" page of the BLAST+ Help manual [here](http://www.ncbi.nlm.nih.gov/books/NBK1762/). Follow the instructions under "Configuration" in the BLAST+ help manual to add BLAST+ to the PATH environment variable.

The download itself may be found [here](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=Download).

In addition to the software, you'll need a database for comparing your data. For the most thorough possible job, you'll want to download the "non-redundant blast database"; this is a list of every sequence that NCBI has accrued. There are a lot. This is a big file. All of this might take a little while.

```
# Download the nr database 
# Make sure to navigate to the directory where you want it to go!
$ sudo wget ftp://ftp.ncbi.nlm.nih.gov/blast/db/FASTA/nr.gz

# Unzip prior to use
$ gunzip nr.gz
```

While blasting against the NCBI nr database is the most thorough option, it isn't always feasible, nor is it always necessary! It's possible to download only portions of the nr by pasting the following in your browser:
> ftp://ftp.ncbi.nlm.nih.gov/blast/db/


And here's a sample workthrough with blastx:
```
# Make a blast database - either with the nr data, or with a custom selection
$ ~/Path/To/Blast_program_files/makeblastdb -in ~/Path/To/Data/nr.fasta -dbtype dna

# Call the blast
nohup nice ~/Path/To/Blast_program_files/blastx -db ~/Path/To/database.fasta -query ~/Path/To/Assembly.fasta -evalue 0.00001 -num_threads 16 -outfmt "7 qseqid qlen sseqid slen qstart qend sstart send evalue bitscore length pident gaps" -out ~/Path/To/Assembly_blastx.out &
```  

----

### Instruction for the black-box method

Today, we're going to use blast on an arbitrary selection of our assembled data so that we can get a feel for what kind of output the program can provide, and to take a look at the identity of some of our assembled contigs. We'll start with a single sequence, and see where we can get!

Later in the course (after some further analysis) we'll choose more specific blast targets. For example:  
  - Highest expressing (via kallisto expression data) 
  - Specific orthogroups (via Orthofinder)
  - etc...




```
awk "/^>/ {n++} n>10 {exit} {print}" assembly_file.fasta > sample_file.fasta
```

An awk script consists of one or more statements of the form: **pattern {actions}**. The input is read line-by-line, and if the current line matches the pattern, the corresponding actions are executed.

Our script consists of 3 such statements:

1. /^>/ {n++} increments the counter each time a new sequence is started. /.../ denotes a regular expression pattern, and ^> is a regular expression that matches the > sign at the beginning of a line. An uninitialized variable in awk has the value 0, which is exactly what we want here. If we needed some other initial value (say, 1), we could have added a BEGIN pattern like this: BEGIN {n=1}.

2. n>$NSEQS {exit} aborts processing once the counter reaches the desired number of sequences.

3. {print} is an action without a pattern (and thus matching every line), which prints every line of the input until the script is aborted by exit.

