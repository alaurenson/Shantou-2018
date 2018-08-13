Identification
----

### [The BLAST Manual](https://www.ncbi.nlm.nih.gov/books/NBK1762/)

> Add: Links to Altschul papers

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

While blasting against the NCBI nr database is the most thorough option, it isn't always feasible, nor is it always necessary! It's possible to download only portions of the nr by pasting the following in your browser:
> ftp://ftp.ncbi.nlm.nih.gov/blast/db/

I may decide that this is more appropriate, depending on how long downloads are taking.

----

### For our exercise today, we're going to blast only an arbitrary selection of our assembled data against the nr database. Later in the course (after some further analysis) we'll choose more specific blast targets.  

> Add: blasting selections of contigs
  - today, top 20 longest assembled contigs (via grep -20 ">" > sample.txt?)
  - later, we'll look at highest expressing (via kallisto?), specific orthogroups (via Orthofinder?), etc...
  - Also blastx w/ uniprot data.

Here's a sample workthrough with blastx:
```
# Make a blast database - either with the nr data, or with a custom selection
$ ~/Path/To/Blast/makeblastdb -in ~/Path/To/Data/nr.fasta -dbtype dna #(Charlie, check this! Is nr.gz already formatted?)

# Call the blast
nohup nice blastx -db ~/Path/To/Data/database.fasta -query ~/Path/To/Assembly.fasta -evalue 0.00001 -num_threads 16 -outfmt "7 qseqid qlen sseqid slen qstart qend sstart send evalue bitscore length pident gaps" -out ~/Path/To/Assembly_blastx.out &
```  
