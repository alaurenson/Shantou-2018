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


