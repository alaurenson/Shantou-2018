### Using BLAST

1. Open the official [NCBI BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) page

2. Click "protein blast"

3. Copy the following TransDecoder output sequence into the query window:
```
>CL_NODE_6803_length_2874_cov_53458231_g4381_i0Telomere_Sde2_2|PF13297.5|2.8e-24
MAKGSQIFVKDLEGRWHCLQFVSSCVSGSELKERLESSLGVPAGIQRLVTGTREVENETLLVGSDDMCDNDEELGYGGGGGFYDDDEELGYGGGGFGPVLLPSCTLLLRLLGGKGGFGSLLRGAATKAGQKKTTNFDACRDMSGRRLRHVNAEKKLKEWQRDGKQRELEKAALQFLRKTERERTVEVGRNVDLAKLREESAEARDMVVDAVASGLEAAKENKRRQRMENAAKEQAGEGSPKRIRMLEMLEAVEESDEEDSEYKEHEDKSDGAGTSGSAGSEDEGSGYNSSPRGPLGDGPFASSPAQSTDGSRGESHEEGGVYSSQRLSTGAESGGVEPVADNCAVITIAHDVCEGGSGHSAGEDASNRSPSLPSDNPSALKDRRGVNSVATGSGCINGHSSSASVAEKSMSGTSSPISVDASISADGESLCFGNFNSAKDLEVLGLDRLKAELQKRGLKCGGSLEERAARLFLLKLTPLNKLDKKHFARPLVKKG*
```

4. For database, choose "UniProtKB/Swiss-Prot(swissprot) 

5. For Algorithm, choose blastp

6. Click "Blast" - You may have to wait a minute for results!

Pretty easy right? 

When the result shows up, I want you to explore it and see what you can figure out. 

----

### Using MUSCLE

1. Go to the [MUSCLE](https://www.ebi.ac.uk/Tools/msa/muscle/) website.

2. Download [this](https://github.com/chazgoo/Shantou-2018/blob/master/Identification/test_MSA.pep.fasta) sample fasta file, and upload it to MUSCLE by using the "browse" button.

3. Use ClustalW, don't change the output format.

4. Click Submit. 

----

#### If you finish, I want you to BLAST the other genes in the test_MSA.pep.fasta file. 

----

#### If you finish that too, read the following section:

### Selecting an arbitrary number of sequences from a fasta file

This is an example of a very powerful language called awk - the following line allows you to arbitratily select a number of sequences from the top of a fasta file. 

Awk is fantastic. And hard to read.

```
awk "/^>/ {n++} n>10 {exit} {print}" assembly_file.fasta > sample_file.fasta
```

An awk script consists of one or more statements of the form: **pattern {actions}**. The input is read line-by-line, and if the current line matches the pattern, the corresponding actions are executed.

Our script consists of 3 such statements:

1. /^>/ {n++} increments the counter each time a new sequence is started. /.../ denotes a regular expression pattern, and ^> is a regular expression that matches the > sign at the beginning of a line. An uninitialized variable in awk has the value 0, which is exactly what we want here. If we needed some other initial value (say, 1), we could have added a BEGIN pattern like this: BEGIN {n=1}.

2. n>$NSEQS {exit} aborts processing once the counter reaches the desired number of sequences.

3. {print} is an action without a pattern (and thus matching every line), which prints every line of the input until the script is aborted by exit.

**The exercise**

1. Download [this](https://github.com/chazgoo/Shantou-2018/blob/master/Identification/Tsue.pep.fasta). 

2. Use the above command to arbitrarily choose the top 3 sequences

```
$ awk "/^>/ {n++} n>3 {exit} {print}" Tsue.pep.fasta > Tsue.sample.fasta
```

3. BLAST it. 
