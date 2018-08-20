## Annotation of Assembled Data
Once you've built assemblies, you're ready to begin predicting protein coding regions, identifying genes, estimating expression, finding orthologs, and comparing sequences. The follow links are tools that allow for steps like this. 

We don't have time in this class for us to really delve into the inner workings of these programs - but know that they are available, and if you ever want to use them, their documentation is far more thorough than anything I could provide. 

For this course, I've performed the following analyses already, and I'll provide you with the output files for your final project.  

----

### [TransDecoder](https://github.com/TransDecoder/TransDecoder)
 
Predict 'Open Reading Frames' (ORFs) in your datasets - these will provide us with the most likely protein-coding sequences. This software operates with Hidden Markov Models. There are optional steps to further identify gene function by comparing your data to the PfamA database.

----

### [OrthoFinder](https://github.com/davidemms/OrthoFinder)

Whether working with one species, or performing a metagenomic analysis, you might want to identify homology. This program does that by using internal reciprocal best blast hits.

----

### [MUSCLE](https://www.ebi.ac.uk/Tools/msa/muscle/)

This is a black-box website that performs multiple sequence alignment - this allows you to visually compare sequences, and to make phylogenetic gene trees. Best for small datasets - larger trees require more sophisticated software.

----

### [Kallisto](https://github.com/pachterlab/kallisto)

Kallisto uses a unique algorithm to estimate gene expression based on RNAseq data. Among all options for estimating expression, this is my favorite - it's extremely fast, and the accuracy is comparable to heavier programs.

