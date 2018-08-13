## Trim, QC, and Assemble a full dataset

### First, some comments on how we're going to approach the rest of this course:

Now that we're beginning to deal with full datasets, we've gotten to the point where our personal laptops may struggle to handle such work, at least in a reasonable amount of time... A large assembly could take a WEEK or more, even on very good machines.

In bioinformatics, we'll often make use of powerful remote servers, or computer clusters, or even cloud computing (via services like Amazon) to accomplish our goals. Where your laptop might have a CPU with 4 or 8 cores, a server will have 24 CPUs with 8 cores each. Usually, we operate servers through the terminal, much like we've been doing - so it should hopefully feel familiar!

We've set up a local machine to act as a mock-server so that we can practice remote operating via the `ssh` command.

> Insert section on SSHing into the "server"

Moving forward in this class, I'm going to divide you into groups: each group will be given a raw dataset to process. This will be yours for the remainder of the class, so be careful! Always ask me first if you are unsure of a step.

> Insert section on using SSH to access the data - we're no longer doing processing on our PCs! Explain potential "French Cooking" aspect

#### Read the following sections, and then each group should work through the steps together - only one final assembly is needed per group. I'd like for each group to document their work by writing out their commands in a text document.

----

### Assembly

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

This single pair represents ALL of the R1/R2 sequences from above, combined end-to-end, in order.

MOST IMPORTANTLY, notice that all of the R1 files and all of the R2 files are combined separately.  

- Why isn't the total size exactly equal to the raw files? (It's not because the .csv file is missing)
- Why is it important that the sequences stay in the same order?
- Why is it important not to mix R1 and R2?

----

### How do we process all of the data at once?

**1. Link all of the R1 and R2 raw sequence files together; one file for R1 and another for R2.**

We'll use the `cat` command, for "concatenate" - this means join end-to-end. Fastq format handles this really well, and `cat` maintains file order. Thus, if your files are numbered/alphabetical, the order will be maintained.

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

This can very easily be done *incorrectly*, especially if you don't keep in mind what's in your current working directory. What if there were **Tsue** files mixed in with **Akle**??

**2. QC (FastQC) and trim (bbduk) the concatenated raw files, just like we did with the example file earlier**

Rather than tell you exactly how to do it here, I'd like you to try and use the [example we did together](https://github.com/chazgoo/Shantou-2018/tree/master/Assembly/Trim-QC) to figure it out.

**3. Check that bbduk was effective by running FastQC on the trimmed files**

Again, please try and use the example in the previous section to model your command.

**4. FINALLY, we'll run an assembly!**

Since we haven't done this yet, here's how to call an assembly using paired-end reads (using MY files and directory structure):
```
# Run from the directory holding your trimmed & concatenated pair of files
# Remember that you must substitute your own file and directory names!

$ nohup nice ~/Desktop/bio_software/SPAdes-3.11.1-Linux/bin/spades.py --rna --pe1-1 Akle_R1.fastq.gz --pe1-2 Akle_R2.fastq.gz -o ./Akle_assembly &
```

While this single line of code is short, it accomplishes a great deal. Let's talk about what we see:
- **nohup** `code` **&**: Any time you run a large job, it should always be wrapped in these two commands. What this does is tell the computer to run the job in the background "with no hang-up". This means if you're operating a server remotely, the server will continue to work even if you close the terminal. It also means you can't see the program output unless you check the 'nohup.out' log file. We'll use this extensively - it's important in big data processing.

- Next you'll see `~/Desktop/bio_software/SPAdes-3.11.1-Linux/bin/spades.py --rna`, which is the call to our assembler (SPAdes) to do an RNA-data assembly. You should now recognize that this is very often how we call programs. In this case, you need to include everything exactly as I have it written.

- After the program call, we have `--pe1-1 Akle_R1.fastq.gz --pe1-2 Akle_R2.fastq.gz`; this tells SPAdes which pair of files to assemble (sometimes we have more than one pair in a folder!)

- Finally, we have `-o ./Akle_assembly` - this is an optional parameter we can set to force the output to have a particular name and be put in a particular place. Here, ./Akle_assembly means "make a file called Akle_assembly" in the current directory.

If you wanted the Assembler output to go someplace else, how would you do that?

Think through all of these aspects of the command, and then go ahead and assemble your data! Use the -o parameter to send your output to [Charlie, choose location!]. Make sure to document what you've done. 
