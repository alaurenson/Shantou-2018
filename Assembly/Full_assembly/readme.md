## Trim, QC, and Assemble a full dataset

In the previous exercise, we used a single set of reads - your file looked something like this:
> Akle_TTAGGC_L004_R1_001.fastq.gz

Notice the "R1" in that file name. This refers to "Read 1" of a **pair** of "paired-end reads". There will be an associated "R2" file with the same name. 

------>
---------
  <------

In addition, a full set of NGS data will almost certainly consist of multiple pairs of read files. 

This is what the full set of raw data for Amphidinium klebsii ("Akle" in the filename) looks like:
```
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ ls -lh
-rwxr-xr-x 1 cagood cagood 301M Aug  3 14:47 Akle_TTAGGC_L004_R1_001.fastq.gz
-rwxr-xr-x 1 cagood cagood 368M Aug  3 14:48 Akle_TTAGGC_L004_R1_002.fastq.gz
-rwxr-xr-x 1 cagood cagood 355M Aug  3 14:48 Akle_TTAGGC_L004_R1_003.fastq.gz
-rwxr-xr-x 1 cagood cagood 365M Aug  3 14:48 Akle_TTAGGC_L004_R1_004.fastq.gz
-rwxr-xr-x 1 cagood cagood 354M Aug  3 14:48 Akle_TTAGGC_L004_R1_005.fastq.gz
-rwxr-xr-x 1 cagood cagood 364M Aug  3 14:48 Akle_TTAGGC_L004_R1_006.fastq.gz
-rwxr-xr-x 1 cagood cagood 357M Aug  3 14:48 Akle_TTAGGC_L004_R1_007.fastq.gz
-rwxr-xr-x 1 cagood cagood 370M Aug  3 14:48 Akle_TTAGGC_L004_R1_008.fastq.gz
-rwxr-xr-x 1 cagood cagood 355M Aug  3 14:48 Akle_TTAGGC_L004_R1_009.fastq.gz
-rwxr-xr-x 1 cagood cagood 356M Aug  3 14:48 Akle_TTAGGC_L004_R1_010.fastq.gz
-rwxr-xr-x 1 cagood cagood 352M Aug  3 14:48 Akle_TTAGGC_L004_R1_011.fastq.gz
-rwxr-xr-x 1 cagood cagood 357M Aug  3 14:48 Akle_TTAGGC_L004_R1_012.fastq.gz
-rwxr-xr-x 1 cagood cagood 101M Aug  3 14:48 Akle_TTAGGC_L004_R1_013.fastq.gz
-rwxr-xr-x 1 cagood cagood 362M Aug  3 14:48 Akle_TTAGGC_L004_R2_001.fastq.gz
-rwxr-xr-x 1 cagood cagood 373M Aug  3 14:49 Akle_TTAGGC_L004_R2_002.fastq.gz
-rwxr-xr-x 1 cagood cagood 361M Aug  3 14:49 Akle_TTAGGC_L004_R2_003.fastq.gz
-rwxr-xr-x 1 cagood cagood 370M Aug  3 14:49 Akle_TTAGGC_L004_R2_004.fastq.gz
-rwxr-xr-x 1 cagood cagood 360M Aug  3 14:49 Akle_TTAGGC_L004_R2_005.fastq.gz
-rwxr-xr-x 1 cagood cagood 369M Aug  3 14:49 Akle_TTAGGC_L004_R2_006.fastq.gz
-rwxr-xr-x 1 cagood cagood 355M Aug  3 14:49 Akle_TTAGGC_L004_R2_007.fastq.gz
-rwxr-xr-x 1 cagood cagood 366M Aug  3 14:49 Akle_TTAGGC_L004_R2_008.fastq.gz
-rwxr-xr-x 1 cagood cagood 356M Aug  3 14:49 Akle_TTAGGC_L004_R2_009.fastq.gz
-rwxr-xr-x 1 cagood cagood 364M Aug  3 14:49 Akle_TTAGGC_L004_R2_010.fastq.gz
-rwxr-xr-x 1 cagood cagood 357M Aug  3 14:49 Akle_TTAGGC_L004_R2_011.fastq.gz
-rwxr-xr-x 1 cagood cagood 361M Aug  3 14:50 Akle_TTAGGC_L004_R2_012.fastq.gz
-rwxr-xr-x 1 cagood cagood 102M Aug  3 14:50 Akle_TTAGGC_L004_R2_013.fastq.gz
-rwxr-xr-x 1 cagood cagood  147 Aug  3 14:50 SampleSheet.csv
```

So we have 13 **pairs** of raw read files.

Aside:
- What can you tell about the command I used to view them? 
- What do you notice about how the files are listed? Size? Permissions? Why would "x" be in the permissions?

So now the challenge at hand is to get these **raw** files processed in such a way that we're left with a single pair of trimmed files (which we'll use for assembly)

