**UNDER CONSTRUCTION**


## Annotation of Assembled Data
Now that we've built assemblies, it's time to identify 'Open Reading Frames' (ORFs) in our datasets - this will provide us with the most likely protein-coding sequences. We'll do this by predicting them based on Hidden Markov Models. First, download the necessary software and databases. 

----

## TransDecoder

### Software
- [TransDecoder](https://github.com/TransDecoder/TransDecoder/wiki)
- [HMMER3](http://hmmer.janelia.org)

### PfamA Database
```
$ sudo wget "ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.gz"
```

### Predicting coding regions from a transcript fasta file 

The 'TransDecoder' utility is run on a fasta file containing the target transcript sequences.  The simplest usage is as follows:

#### Step 1: extract the long open reading frames
```    
TransDecoder.LongOrfs -t target_transcripts.fasta
```

By default, TransDecoder.LongOrfs will identify ORFs that are at least 100 amino acids long. You can lower this via the '-m' parameter, but know that the rate of false positive ORF predictions increases drastically with shorter minimum length criteria.


#### Step 2: (optional)
    
Optionally, identify ORFs with homology to known proteins via blast or pfam searches.

After running TransDecoder.LongOrfs, you'll find a multi-fasta protein file called 
> {transcripts_file}.transdecoder_dir/longest_orfs.pep 

Search these candidate peptides for homology using approaches below:

##### Pfam Search 

Search the peptides for protein domains using Pfam. This requires [HMMER](http://hmmer.janelia.org) and [Pfam](ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.gz) databases to be installed.

**First, download, unzip, and compress HMM database - only needs to happen once per database**
```
$ wget ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.gz
$ tar -zvxf Pfam-A.hmm.gz
$ ~/software/hmmer-3.1b2-linux-intel-x86_64/binaries/hmmpress Pfam-A.hmm
```

**Now we can scan**
```
$ hmmscan --cpu 8 --domtblout pfam.domtblout /path/to/Pfam-A.hmm transdecoder_dir/longest_orfs.pep
```
Just as with the blast search, if you have access to a computing grid, consider using [HPC GridRunner](https://github.com/HpcGridRunner/HpcGridRunner.github.io/releases).

#### Integrating the Pfam search results into coding region selection 

The outputs generated above can be leveraged by TransDecoder to ensure that those peptides with domain hits are retained in the set of reported likely coding regions.  Run TransDecoder.Predict like so:
```
$ TransDecoder.Predict -t target_transcripts.fasta --retain_pfam_hits pfam.domtblout 
```
The final coding region predictions will now include both those regions that have sequence characteristics consistent with coding regions in addition to those that have demonstrated blast homology or pfam domain content.


#### Step 3: predict the likely coding regions
```
TransDecoder.Predict -t target_transcripts.fasta [ homology options ]
```
The final set of candidate coding regions can be found as files '*.transdecoder.*' where extensions include .pep, .cds, .gff3, and .bed

----

## OrthoFinder

Software for inferring orthologues between species
  - Input: peptide data in fasta format
  - Output: Species phylogeny, gene phylogeny, orthologues, and summary statistics. 

Software repository and manuals: [here.](https://github.com/davidemms/OrthoFinder)

### Installation, Software Dependencies (From OrthoFinder repository)

1. Download the latest release from github: https://github.com/davidemms/OrthoFinder/releases (for this example we will assume it is OrthoFinder-1.0.6.tar.gz, change this as appropriate.)

2. In a terminal, 'cd' to where you downloaded the package 

3. Extract the files: `tar xzf OrthoFinder-1.0.6.tar.gz`

#### BLAST+
You already have this!

#### MCL
The mcl clustering algorithm is available in the repositories of some Linux distributions and so can be installed in the same way as any other package. For example, on Ubuntu, Debian, Linux Mint:

- `sudo apt-get install mcl`

Alternatively it can be built from source which will likely require the 'build-essential' or equivalent package on the Linux distribution being used. Instructions are provided on the MCL webpage, http://micans.org/mcl/.  

#### FastME
FastME can be obtained from http://www.atgc-montpellier.fr/fastme/binaries.php. The package contains a 'binaries/' directory. Choose the appropriate one for your system and copy it to somewhere in the system path e.g. '/usr/local/bin'** and name it 'fastme'. I.e.:

- `sudo cp fastme-2.1.5-linux64 /usr/local/bin/fastme`

----

**Add: Running TransDecoder** 

**Add: Running OrthoFinder**

**Add: MSAs of gene families (eg/ find orthogroup, ID w/ HMM and BLAST data, Perform MSA w/ MUSCLE)**
