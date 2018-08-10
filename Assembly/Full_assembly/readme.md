## Trim, QC, and Assemble a full dataset

In the previous exercise, we used a single set of reads - your file looked something like this:
> Akle_TTAGGC_L004_R1_001.fastq.gz

Notice the "R1" in that file name. This refers to "Read 1" of a **pair** of "paired-end reads". There will be an associated "R2" file with the same name. 

In addition, a full set of NGS data will almost certainly consist of multiple pairs of read files. 

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

- What can you tell about the command I used to view them? 
- What do you notice about how the files are listed? Size? Permissions?

So now the challenge at hand is to get these **raw** files processed in such a way that we're left with a single pair of trimmed files (which we'll use for assembly), which will look like this:
```
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/trimmed$ ls -lh
total 6.2G
-rw-r--r-- 1 cagood cagood 3.1G Aug  3 15:08 Akle_R1.fastq.gz
-rw-r--r-- 1 cagood cagood 3.1G Aug  3 15:10 Akle_R2.fastq.gz
```

This single pair represents ALL of the sequence from above, combined end-to-end, in order. 

- Why isn't the total size exactly equal to the raw files? (It's not because the .csv file is missing)
- Why is it important that the sequences stay in the same order?

### How do we process all of the data at once? 

**1. Link all of the R1 and R2 raw sequence files together; one file for R1 and another for R2.**

We'll use the "cat" command, for "concatenate"

```
# The hard (but always accurate) way: explicitly list files
$ cat Akle_TTAGGC_L004_R1_001.fastq.gz Akle_TTAGGC_L004_R1_002.fastq.gz Akle_TTAGGC_L004_R1_003.fastq.gz Akle_TTAGGC_L004_R1_004.fastq.gz Akle_TTAGGC_L004_R1_005.fastq.gz Akle_TTAGGC_L004_R1_006.fastq.gz Akle_TTAGGC_L004_R1_007.fastq.gz Akle_TTAGGC_L004_R1_008.fastq.gz Akle_TTAGGC_L004_R1_009.fastq.gz Akle_TTAGGC_L004_R1_010.fastq.gz Akle_TTAGGC_L004_R1_011.fastq.gz Akle_TTAGGC_L004_R1_012.fastq.gz Akle_TTAGGC_L004_R1_013.fastq.gz > Akle_R1.fastq.gz

# The easy (but possible to screw up) way: regular expressions!
$ cat *_R1_*.fastq.gz > Akle_R1.fastq.gz
```
When possible to use them, regular expressions make life really easy. Here, `*_R1_*.fastq.gz` can be translated like so:
> "match anything"\_R1\_"match anything".fastq.gz

This means that `cat` will go down the list of files and use each 'R1' file, in numeric order. 

We *should* be able to call `$ cat *_R1_*.fastq.gz > Akle_R1.fastq.gz` and `$ cat *_R2_*.fastq.gz > Akle_R2.fastq.gz` to obtain the concatenated raw files. 

This can very easily be done incorrectly, especially if you don't keep in mind what's in your pwd. What if there were **Tsue** files mixed in with **Akle**??

**2. QC (FastQC) and trim (bbduk) the concatenated raw files, just like we did with the example file earlier**

Rather than tell you exactly how to do it here, I'd like you to try and use the [example](https://github.com/chazgoo/Shantou-2018/tree/master/Assembly/Trim-QC) to figure it out.

**3. Check that bbduk was effective by running FastQC on the trimmed files**

**4. FINALLY, run an assembly**
