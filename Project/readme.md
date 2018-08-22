# The Final Project

We're going to do some analysis on 3 assembled datasets 

Your species are Amphidinium klebsii, Tetraselmis suecica, and Gyrodinium instriatum. Thanks Mario for the first two!

I have already done the following steps:

1. Trim/QC
2. Assembly
3. TransDecoder (to predict open reading frames)
4. OrthoFinder (to identify Orthologues between the three species)

I'll provide everything you need, and I want each team to do the following:

1. Take an orthogroup and identify the genes involved using blastp 
2. Research their set of genes and come up with a detailed description of the pathway(s) involved - how do these pertain to the actual physiology of the organism?
3. Do a multiple sequence alignment of their genes, and produce a gene tree. 
4. **If there's time**, I may add an additional section to examine expression data - how much were these genes expressed? 

Please ask me for help if you get stuck, that's why I'm here!

## Download and unzip the [Project_Data](https://github.com/chazgoo/Shantou-2018/tree/master/Project/Project_Data) directory to your desktop

1. Follow the link and click download.

2. Unzip it. Either by right-clicking or in your terminal with bash:
```
$ cd /mnt/c/Users/<your user name>/Desktop/
$ unzip Project_Data
```

## Select your [Orthogroup](https://github.com/chazgoo/Shantou-2018/tree/master/Project/ogroups) file, copy the text into a new .txt file in the Project_Data directory.

*If that isn't working, ocme to me with a USB drive and I'll copy it for you*

1. I will tell each team which "Orthogroup" file to use [here](https://github.com/chazgoo/Shantou-2018/tree/master/Project/ogroups)

(This was the result of using OrthoFinder to detect orthologous sequence in the three species)

## Use bash to modify the file

1. Navigate to that file in bash, and view it with ls

```
$ ls ogroup_34.txt

OG0000034       CA_NODE_20152_length_1893_cov_93.633621_g13266_i0.p1    CL_NODE_6803_length_2874_cov_53458231_g4381_i0, CL_NODE_6820_length_2871_cov_53514820_g4381_i1, CL_NODE_6925_length_2854_cov_53837771_g4381_i2, CL_NODE_6989_length_2842_cov_54069162_g4381_i3, ...
```

This file contains the **names** of contigs in a given orthogroup, as determined by OrthoFinder.

2. We need to modify the file so that it looks like this:
```
OG0000034
CA_NODE_20152_length_1893_cov_93.633621_g13266_i0.p1
CL_NODE_6803_length_2874_cov_53458231_g4381_i0
CL_NODE_6820_length_2871_cov_53514820_g4381_i1
CL_NODE_6925_length_2854_cov_53837771_g4381_i2 
CL_NODE_6989_length_2842_cov_54069162_g4381_i3
```
Steps:
- Place each ID on a new line
- Remove all spaces and commas

You can do this in your text editor, OR you can use bash commands. The file MUST look like this though - if it's in the wrong format, the rest of this won't work. 

The spaces are very important, so if you need to, copy/paste the line code after `$` ONE AT A TIME into bash. You can't do them all at once.
 
Remember, `#` means I (Charlie) am talking to you. 

The `$` means "this is code to use", but make sure you don't copy the `$` in.

**NOTE: You need to modify 'ogroup_34.txt' to whatever your ogroup_# is!**

**The bash commands**
```
# sed is used to 'substitute'

# Do these commands EXACTLY, copy/paste if you're unsure!
# I want you to use 'less' so that you can see the changes that are being made.

$ sed 's/  */ /g' ogroup_34.txt > og34_mod.txt

$ less og34_mod.txt

$ sed -i 's/ /,/g' og34_mod.txt

$ less og34_mod.txt

$ sed -i 's/,,/,/g' og34_mod.txt

$ less og34_mod.txt

$ sed -i 's/,/\n/g' og34_mod.txt

$ less og34_mod.txt

$ sed -i 's/ //g' og34_mod.txt

$ less og34_mod.txt
```

## Use bash commands to extract Protein data from TransDecoder output

The TransDecoder output files are fasta-format protein sequence files, which were generated from the assemblies of each species. 

You will have 1 og_mod.txt file which you made, and 3 TransDecoder ORF files (for 3 species) which I gave you - the following lines must be called for all 3 species' files. 

**The bash commands**

**Do these 9 commands for each TransDecoder file - you will need to modify "Akle..." to "Gins_C1..." and "Tsue..."**

```
# Ask me if you need help!
# Again, I want you to use 'less' to see what changes are happening

$ less Akle.pep.fasta

# This line formats the TD output file so that the text 'wraps', which means the sequence is on one line
$ sed -e 's/\(^>.*$\)/#\1#/' Akle.pep.fasta | tr -d "\r" | tr -d "\n" | sed -e 's/$/#/' | tr "#" "\n" | sed -e '/^$/d' > Akle_oneline.pep.fasta

$ less Akle_oneline.pep.fasta

# This command searches for sequences matching the IDs in ogmod.txt
$ grep -F -A 1 -f 'og_mod.txt' 'Akle_oneline.pep.fasta' > Akle_ortho_seqs.pep.fasta

$ less Akle_ortho_seqs.pep.fasta

# Remove some extra spaces
$ sed -i 's/ //g' Akle_ortho_seqs.pep.fasta

$ less Akle_ortho_seqs.pep.fasta

# Remove '--' lines
$ sed -i 's/--//g' Akle_ortho_seqs.pep.fasta

$ less Akle_ortho_seqs.pep.fasta

# Remove '*' characters
$ sed -i 's/*//g' Akle_ortho_seqs.pep.fasta

$ less Akle_ortho_seqs.pep.fasta
```

## Blast Protein data to ID; describe how the genes function in vivo

View each ortho.pep.fasta file using `less` - they'll look something like this:

```
$ ls Akle_ortho.pep.fasta

>NODE_6803_length_2874_cov_53458231_g4381_i0Telomere_Sde2_2|PF13297.5|2.8e-24
MAKGSQIFVKDLEGRWHCLQFVSSCVSGSELKERLESSLGVPAGIQRLVTGTREVENETLLVGSDDMCDNDEELGYGGGGGFYDDDEELGYGGGGFGPVLLPSCTLLLRLLGGKGGFGSLLRGAATKAGQKKTTNFDACRDMSGRRLRHVNAEKKLKEWQRDGKQRELEKAALQFLRKTERERTVEVGRNVDLAKLREESAEARDMVVDAVASGLEAAKENKRRQRMENAAKEQAGEGSPKRIRMLEMLEAVEESDEEDSEYKEHEDKSDGAGTSGSAGSEDEGSGYNSSPRGPLGDGPFASSPAQSTDGSRGESHEEGGVYSSQRLSTGAESGGVEPVADNCAVITIAHDVCEGGSGHSAGEDASNRSPSLPSDNPSALKDRRGVNSVATGSGCINGHSSSASVAEKSMSGTSSPISVDASISADGESLCFGNFNSAKDLEVLGLDRLKAELQKRGLKCGGSLEERAARLFLLKLTPLNKLDKKHFARPLVKKG*

>NODE_6820_length_2871_cov_53514820_g4381_i1Telomere_Sde2_2|PF13297.5|3e-24
MINTKNKKNKKKKKRKVKGKVVAMAKGSQIFVKDLEGRWHCLQFVSSCVSGSELKERLESSLGVPAGIQRLVTGTREVENETLLVGSDDMCDNDEELGYGGGGGFYDDDEELGYGGGGFGPVLLPSCTLLLRLLGGKGGFGSLLRGAATKAGQKKTTNFDACRDMSGRRLRHVNAEKKLKEWQRDGKQRELEKAALQFLRKTERERTVEVGRNVDLAKLREESAEARDMVVDAVASGLEAAKENKRRQRMENAAKEQAGEGSPKRIRMLEMLEAVEESDEEDSEYKEHEDKSDGAGTSGSAGSEDEGSGYNSSPRGPLGDGPFASSPAQSTDGSRGESHEEGGVYSSQRLSTGAESGGVEPVADNCAVITIAHDVCEGGSGHSAGEDASNRSPSLPSDNPSALKDRRGVNSVATGSGCINGHSSSASVAEKSMSGTSSPISVDASISADGESLCFGNFNSAKDLEVLGLDRLKAELQKRGLKCGGSLEERAARLFLLKLTPLNKLDKKHFARPLVKKG*

...
``` 

**Using [NCBI blastp](https://blast.ncbi.nlm.nih.gov/Blast.cgi), identify the genes from your Orthogroup.** 

You may simply copy/paste the sequences into the query window on the blast website.  

Remember, I want you to do this for all three species!

Set the following options:
- Database: "UniprotKB/Swiss-Prot(swissprot)"
- Algorithm: blastp

Download the highest scoring blast alignment each time, so that you can compare them all at the end!

I want you to research the gene/genes you've identified, and then describe how those genes pertain to the in-vivo physiology of the organisms.

**Note:** If your sequences are returning no significant matches, then I picked a bad orthogroup - I chose randomly, and I haven't balsted these myself, so I don't know what you're getting. Tell me and I'll give you a new one. 


## Do a Multiple Sequence Alignment with MUSCLE

First we need to concatenate our ortho.pep.fasta files!

```
$ cat Akle_ortho.pep.fasta Gins_C1_ortho.pep.fasta Tsue_ortho.pep.fasta > all_orthos.pep.fasta
```

1. Go to the [MUSCLE](https://www.ebi.ac.uk/Tools/msa/muscle/) site and use the 'upload' button to add the all_orthos.pep.fasta file.

2. Don't change anything, use ClustalW format

3. Submit 

Explore the output, download the alignment and the resulting phylogenetic tree. 

----

## Extra: Kallisto data? Plot a histogram of relative expression for each gene.  

If I think that there will be time for this, I'll update this section. 
 
This is probably going to happen - so be ready. 
 
