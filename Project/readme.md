## Use OrthoFinder output to select an Orthogroup

1. I will provide each team with an "Orthogroup" file (which was the result of using OrthoFinder to detect orthologous sequence in the three species)

## Use bash to modify the file

1. Navigate to that file in bash, and view it with ls

```
$ ls ogroup.txt

OG0000034       CA_NODE_20152_length_1893_cov_93.633621_g13266_i0.p1    CL_NODE_6803_length_2874_cov_53458231_g4381_i0, CL_NODE_6820_length_2871_cov_53514820_g4381_i1, CL_NODE_6925_length_2854_cov_53837771_g4381_i2, CL_NODE_6989_length_2842_cov_54069162_g4381_i3, ...
```

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

**The bash commands**
```
# sed is used to 'substitute'

# Do these commands EXACTLY, copy/paste if you're unsure!
# I want you to use 'less' so that you can see the changes that are being made.

$ sed 's/  */ /g' ogroup.txt > ogmod.txt

$ less ogmod.txt

$ sed -i 's/ /,/g' ogmod.txt

$ less ogmod.txt

$ sed -i 's/,,/,/g' ogmod.txt

$ less ogmod.txt

$ sed -i 's/,/\n/g' ogmod.txt

$ less ogmod.txt

$ sed -i 's/ //g' ogmod.txt

$ less ogmod.txt
```

## Use bash commands to extract Protein data from TransDecoder output

You will have 1 ogmod.txt file, and 3 TransDecoder ORF files (for 3 species) - the following lines must be called for each species. 

**The bash commands**

**Do these 9 commands for each TransDecoder file - you will need to modify "species_1..." to "species_2..." and "species_3..." - you can do this simply by changing the number!**

```
# Ask me if you need help!
# Again, I want you to use 'less' to see what changes are happening

$ less species_1_TD_output.fasta

# This line formats the TD output file so that the text 'wraps', which means the sequence is on one line
$ sed -e 's/\(^>.*$\)/#\1#/' species_1_TD_output.pep.fasta | tr -d "\r" | tr -d "\n" | sed -e 's/$/#/' | tr "#" "\n" | sed -e '/^$/d' > species_1_oneline.pep.fasta

$ less species_1_oneline.pep.fasta

# This command searches for sequences matching the IDs in ogmod.txt
$ grep -F -A 1 -f 'ogmod.txt' 'species_1_oneline.pep.fasta' > species_1_orthos.pep.fasta

$ less species_1_orthos.pep.fasta

# Remove some extra spaces
$ sed -i 's/ //g' species_1_orthos.pep.fasta

$ less species_1_orthos.pep.fasta

# Remove '--' lines
$ sed -i 's/--//g' species_1_orthos.pep.fasta

$ less species_1_orthos.pep.fasta

# Remove '*' characters
$ sed -i 's/*//g' species_1_orthos.pep.fasta

$ less species_1_orthos.pep.fasta
```

## Blast DNA and protein data to ID; describe how the genes function in vivo

View each _orthos.pep.fasta file using `less` - they'll look like this:
```
$ ls species_1_orthos.pep.fasta

>CL_NODE_6803_length_2874_cov_53458231_g4381_i0Telomere_Sde2_2|PF13297.5|2.8e-24
MAKGSQIFVKDLEGRWHCLQFVSSCVSGSELKERLESSLGVPAGIQRLVTGTREVENETLLVGSDDMCDNDEELGYGGGGGFYDDDEELGYGGGGFGPVLLPSCTLLLRLLGGKGGFGSLLRGAATKAGQKKTTNFDACRDMSGRRLRHVNAEKKLKEWQRDGKQRELEKAALQFLRKTERERTVEVGRNVDLAKLREESAEARDMVVDAVASGLEAAKENKRRQRMENAAKEQAGEGSPKRIRMLEMLEAVEESDEEDSEYKEHEDKSDGAGTSGSAGSEDEGSGYNSSPRGPLGDGPFASSPAQSTDGSRGESHEEGGVYSSQRLSTGAESGGVEPVADNCAVITIAHDVCEGGSGHSAGEDASNRSPSLPSDNPSALKDRRGVNSVATGSGCINGHSSSASVAEKSMSGTSSPISVDASISADGESLCFGNFNSAKDLEVLGLDRLKAELQKRGLKCGGSLEERAARLFLLKLTPLNKLDKKHFARPLVKKG*

>CL_NODE_6820_length_2871_cov_53514820_g4381_i1Telomere_Sde2_2|PF13297.5|3e-24
MINTKNKKNKKKKKRKVKGKVVAMAKGSQIFVKDLEGRWHCLQFVSSCVSGSELKERLESSLGVPAGIQRLVTGTREVENETLLVGSDDMCDNDEELGYGGGGGFYDDDEELGYGGGGFGPVLLPSCTLLLRLLGGKGGFGSLLRGAATKAGQKKTTNFDACRDMSGRRLRHVNAEKKLKEWQRDGKQRELEKAALQFLRKTERERTVEVGRNVDLAKLREESAEARDMVVDAVASGLEAAKENKRRQRMENAAKEQAGEGSPKRIRMLEMLEAVEESDEEDSEYKEHEDKSDGAGTSGSAGSEDEGSGYNSSPRGPLGDGPFASSPAQSTDGSRGESHEEGGVYSSQRLSTGAESGGVEPVADNCAVITIAHDVCEGGSGHSAGEDASNRSPSLPSDNPSALKDRRGVNSVATGSGCINGHSSSASVAEKSMSGTSSPISVDASISADGESLCFGNFNSAKDLEVLGLDRLKAELQKRGLKCGGSLEERAARLFLLKLTPLNKLDKKHFARPLVKKG*
``` 

Using NCBI blastp, identify the genes from your Orthogroup. 

You may simply copy/paste the sequence into the query window on the blast website. 

Remember, I want you to do this for all three species!

Set the following options:

> Database: "UniprotKB/Swiss-Prot(swissprot)"
> Algorithm: blastp

Download the highest scoring blast alignment each time, so that you can compare them all at the end!

I want you to research the gene/genes you've identified, and then describe how those genes pertain to the in-vivo physiology of the organisms.

## Do a Multiple Sequence Alignment with MUSCLE

First we need to concatenate our _orthos.pep.fasta files!

```
$ cat species_1_orthos.pep.fasta species_2_orthos.pep.fasta species_3_orthos.pep.fasta > allspecs_orthos.pep.fasta
```

Then, go to https://www.ebi.ac.uk/Tools/msa/muscle/ and use the 'upload' button to add the allspecs_orthos.pep.fasta file.

Use ClustalW format in step 2.

Submit in step 3. 

- Explore the output, download the alignment and the resulting phylogenetic tree. 

### Extra: Kallisto data? Plot a histogram of relative expression for each gene.  

If I think that there will be time for this, I'll update this section. 
 

 
