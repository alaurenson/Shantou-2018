## Working with *Amphidinium klebsii

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

This is what the full set of raw data for Amphidinium klebsii ("Akle" in the filename) looks like:
```
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ ls -lh
total 8.6G
-rw-r--r-- 1 cagood cagood 301M Aug  3 14:47 Akle_TTAGGC_L004_R1_001.fastq.gz
-rw-r--r-- 1 cagood cagood 368M Aug  3 14:48 Akle_TTAGGC_L004_R1_002.fastq.gz
-rw-r--r-- 1 cagood cagood 355M Aug  3 14:48 Akle_TTAGGC_L004_R1_003.fastq.gz
-rw-r--r-- 1 cagood cagood 365M Aug  3 14:48 Akle_TTAGGC_L004_R1_004.fastq.gz
-rw-r--r-- 1 cagood cagood 354M Aug  3 14:48 Akle_TTAGGC_L004_R1_005.fastq.gz
-rw-r--r-- 1 cagood cagood 364M Aug  3 14:48 Akle_TTAGGC_L004_R1_006.fastq.gz
-rw-r--r-- 1 cagood cagood 357M Aug  3 14:48 Akle_TTAGGC_L004_R1_007.fastq.gz
-rw-r--r-- 1 cagood cagood 370M Aug  3 14:48 Akle_TTAGGC_L004_R1_008.fastq.gz
-rw-r--r-- 1 cagood cagood 355M Aug  3 14:48 Akle_TTAGGC_L004_R1_009.fastq.gz
-rw-r--r-- 1 cagood cagood 356M Aug  3 14:48 Akle_TTAGGC_L004_R1_010.fastq.gz
-rw-r--r-- 1 cagood cagood 352M Aug  3 14:48 Akle_TTAGGC_L004_R1_011.fastq.gz
-rw-r--r-- 1 cagood cagood 357M Aug  3 14:48 Akle_TTAGGC_L004_R1_012.fastq.gz
-rw-r--r-- 1 cagood cagood 101M Aug  3 14:48 Akle_TTAGGC_L004_R1_013.fastq.gz
-rw-r--r-- 1 cagood cagood 362M Aug  3 14:48 Akle_TTAGGC_L004_R2_001.fastq.gz
-rw-r--r-- 1 cagood cagood 373M Aug  3 14:49 Akle_TTAGGC_L004_R2_002.fastq.gz
-rw-r--r-- 1 cagood cagood 361M Aug  3 14:49 Akle_TTAGGC_L004_R2_003.fastq.gz
-rw-r--r-- 1 cagood cagood 370M Aug  3 14:49 Akle_TTAGGC_L004_R2_004.fastq.gz
-rw-r--r-- 1 cagood cagood 360M Aug  3 14:49 Akle_TTAGGC_L004_R2_005.fastq.gz
-rw-r--r-- 1 cagood cagood 369M Aug  3 14:49 Akle_TTAGGC_L004_R2_006.fastq.gz
-rw-r--r-- 1 cagood cagood 355M Aug  3 14:49 Akle_TTAGGC_L004_R2_007.fastq.gz
-rw-r--r-- 1 cagood cagood 366M Aug  3 14:49 Akle_TTAGGC_L004_R2_008.fastq.gz
-rw-r--r-- 1 cagood cagood 356M Aug  3 14:49 Akle_TTAGGC_L004_R2_009.fastq.gz
-rw-r--r-- 1 cagood cagood 364M Aug  3 14:49 Akle_TTAGGC_L004_R2_010.fastq.gz
-rw-r--r-- 1 cagood cagood 357M Aug  3 14:49 Akle_TTAGGC_L004_R2_011.fastq.gz
-rw-r--r-- 1 cagood cagood 361M Aug  3 14:50 Akle_TTAGGC_L004_R2_012.fastq.gz
-rw-r--r-- 1 cagood cagood 102M Aug  3 14:50 Akle_TTAGGC_L004_R2_013.fastq.gz
-rw-r--r-- 1 cagood cagood  147 Aug  3 14:50 SampleSheet.csv
```

So we have 13 **pairs** of raw read files. 

The easiest way to process them is to join all R1 and all R2 files together. 

### How do we process all of the data at once? Cat (concatenate) all raw reads into a single file:

**1. Link all of the R1 and R2 raw sequence files together; one file for R1 and another for R2.**

We'll use the `cat` command, for "concatenate" - this means join end-to-end. Fastq format handles this really well, and `cat` maintains file order. Thus, if your files are numbered/alphabetical, the order will be maintained.

```
# The hard (but always accurate) way: explicitly list files
$ cat Akle_TTAGGC_L004_R1_001.fastq.gz Akle_TTAGGC_L004_R1_002.fastq.gz Akle_TTAGGC_L004_R1_003.fastq.gz Akle_TTAGGC_L004_R1_004.fastq.gz Akle_TTAGGC_L004_R1_005.fastq.gz Akle_TTAGGC_L004_R1_006.fastq.gz Akle_TTAGGC_L004_R1_007.fastq.gz Akle_TTAGGC_L004_R1_008.fastq.gz Akle_TTAGGC_L004_R1_009.fastq.gz Akle_TTAGGC_L004_R1_010.fastq.gz Akle_TTAGGC_L004_R1_011.fastq.gz Akle_TTAGGC_L004_R1_012.fastq.gz Akle_TTAGGC_L004_R1_013.fastq.gz > Akle_R1.fastq.gz

# The easy (but possible to screw up) way: regular expressions!
$ cat *_R1_*.fastq.gz > Akle_R1.fastq.gz
```

When possible to use them, regular expressions make life easy. Here, `*_R1_*.fastq.gz` can be translated like so:
> "match anything"\_R1\_"match anything".fastq.gz

This means that `cat` will go down the list of files and use each 'R1' file, in numeric order.

We *should* be able to call `$ cat *_R1_*.fastq.gz > Akle_R1.fastq.gz` and `$ cat *_R2_*.fastq.gz > Akle_R2.fastq.gz` to obtain the concatenated raw files.

This can very easily be done *incorrectly*, especially if you don't keep in mind what's in your current working directory. What if there were **Tsue** files mixed in with **Akle**??

**The commands I used**
```
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ cat Akle_TTAGGC_L004_R1_* > Akle_raw_R1.fastq.gz

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ cat Akle_TTAGGC_L004_R2_* > Akle_raw_R2.fastq.gz
```

Afterward, we have these additional files

```
-rw-r--r-- 1 cagood cagood 3.1G Aug  3 15:08 Akle_R1.fastq.gz
-rw-r--r-- 1 cagood cagood 3.1G Aug  3 15:10 Akle_R2.fastq.gz
```

This single pair represents ALL of the R1/R2 sequences from above, combined end-to-end, in order.

MOST IMPORTANTLY, notice that all of the R1 files and all of the R2 files are combined separately.  

- Why is it important that the sequences stay in the same order?
- Why is it important not to mix R1 and R2?


### Run FastQC on the raw reads

```
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ nohup ~/software/FastQC/fastqc Akle_raw_R1.fastq.gz &

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ nohup ~/software/FastQC/fastqc Akle_raw_R2.fastq.gz &
```

### Trim the data using bbduk

```
# Remove adapters

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ ~/software/bbmap/bbduk.sh -Xmx1g in=Akle_raw_R1.fastq.gz out=temp.fastq ref=~~/software/bbmap/resources/adapters.fa ktrim=r k=23 mink=11 hdist=1 tpe tbo

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ ~/software/bbmap/bbduk.sh -Xmx1g in=Akle_raw_R2.fastq.gz out=temp.fastq ref=~~/software/bbmap/resources/adapters.fa ktrim=r k=23 mink=11 hdist=1 tpe tbo

# Remove low quality reads

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ ~/software/bbmap/bbduk.sh -Xmx1g in=temp.fastq out=Akle_R1.fastq qtrim=rl trimq=10

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ ~/software/bbmap/bbduk.sh -Xmx1g in=temp.fastq out=Akle_R2.fastq qtrim=rl trimq=10
```


### Run FastQC on the trimmed reads

```
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ nohup ~/software/FastQC/fastqc Akle_R1.fastq.gz &
[5] 9342
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ nohup: ignoring input and appending output to 'nohup.out'

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ nohup ~/software/FastQC/fastqc Akle_R2.fastq.gz &
[6] 9365
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ nohup: ignoring input and appending output to 'nohup.out'
```

### Call the assembly

```
nice ~/software/SPAdes-3.11.1-Linux/bin/spades.py --rna --pe1-1 /home/cagood/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed/Akle_R1.fastq.gz --pe1-2 /home/cagood/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed/Akle_R2.fastq.gz -o /home/cagood/Shantou_2018/Seq_data/Amphidinium_klebsii/assembled/spades;
```
