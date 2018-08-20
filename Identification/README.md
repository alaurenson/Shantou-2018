### Identification: BLAST+ (Basic Local Alignment Search Tool)

#### [The BLAST Guide](https://www.ncbi.nlm.nih.gov/books/NBK1762/)

### Flavors of blast

- **[blastn](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome)**: DNA sequence vs. DNA database
- **[blastp](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastp&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome)**: Protein sequence vs. protein database
- **[blastx](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastx&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome)**: Take DNA sequence, predict protein coding sequence, and compare to a protein database
- **[tblastn](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=tblastn&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome)**: the reverse - take protein sequence, predict the DNA sequence, and compare to a DNA database

Stephen Altshul's BLAST algorithm is the most widely-used sequence comparison process used in modern biology: he is the most highly cited academic author today. 

Using BLAST, you compare your DNA or protein sequence data to a known database, and the process returns a putative ID for your sequence. The uses for this are numerous, but the most basic is to figure out just what sequences you're looking at!

There are two ways to use BLAST: black-box and manual operation. 

Black-box refers to a 'hidden' process - here this means we simply use the NCBI website to run the data. This is very convenient for smaller datasets, or for selections of genes. It is not very efficient though - you would NEVER want to run an entire assembly through the BLAST website. 

For larger datasets, you will want to download and run the software yourself. 

I've provided instructions for both. 

----

### Instructions for the black-box method (using the website)

Luckily, this is a very easy process. It is not practical for large-scale blasts. Use this if you have a few sequences to check out, but NOT if you want to ID your whole assembly - if that's your goal, it's better to run the blast locally: see the next section. 

1. Start [here](https://blast.ncbi.nlm.nih.gov/Blast.cgi)

You'll see a few options - what you pick depends on your data. We're going to use DNA in our example, and so we'll use **blastn**. 

2. Click **blastn**

3. Copy your sequence into the window, or upload a fasta file in the "enter query sequence" box.

4. Choose your search set in the next box. NCBI's "non-redundant" database is actively modified and maintained, and is a great starting point. 

5. You may also narrow down your search by choosing a family or species - this can make your search much faster. 

6. The remaining options are for advanced runs - you don't need to worry about those for now. Just click BLAST. 

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

### Selecting an arbitrary number of sequences from a fasta file

This is an example of a very powerful language called awk - the following line allows you to arbitratily select a number of sequences from the top of a fasta file. 

Originally, I tabbed this out for use with an exercise with blast, but we're no longer going to use it. That said, I wanted to leave it up because it's a useful example for those of you interested in more advanced coding. 

Awk is fantastic. 

```
awk "/^>/ {n++} n>10 {exit} {print}" assembly_file.fasta > sample_file.fasta
```

An awk script consists of one or more statements of the form: **pattern {actions}**. The input is read line-by-line, and if the current line matches the pattern, the corresponding actions are executed.

Our script consists of 3 such statements:

1. /^>/ {n++} increments the counter each time a new sequence is started. /.../ denotes a regular expression pattern, and ^> is a regular expression that matches the > sign at the beginning of a line. An uninitialized variable in awk has the value 0, which is exactly what we want here. If we needed some other initial value (say, 1), we could have added a BEGIN pattern like this: BEGIN {n=1}.

2. n>$NSEQS {exit} aborts processing once the counter reaches the desired number of sequences.

3. {print} is an action without a pattern (and thus matching every line), which prints every line of the input until the script is aborted by exit.
