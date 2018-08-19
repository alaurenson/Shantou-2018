## Very basic data visualization with R

Here, I'll list the steps to read some assembly data into R, and we'll make three plots.

### Pre-processing data

In your terminal, navigate to the spades assembly folder. 

It should look like this:
```
$ ls
before_rr.fasta  hard_filtered_transcripts.fasta  K49         soft_filtered_transcripts.fasta  transcripts.fasta
corrected        headers                          misc        spades.log                       transcripts.paths
dataset.info     input_dataset.yaml               params.txt  tmp
```

Look now at the hard_filtered_transcripts.fasta file
```
$ less hard_filtered_transcripts.fasta
>NODE_1_length_8049_cov_42.810250_g0_i0
TGCGCTGTGGCAGCGCTTGTCGCCGTTGTTGGCGGGTGCATGAAAGCATCTTAACCTTCC
CAAGATTGGGAGCTCCAGTCAAGGGGACTCAAGGACAAAAAAGCTAGGGGGAGCAAGGTC
TGTACAAGAGTTACCTAAGCCCCCACCCCCCTCCTAGAACGCTGGGAAGGAAAGCGGGCT
CCCAAACCACTGCAATGCATTGCGTGCCTTTGGCTTCGGTGGCGGCATCCTCACTGCCTC
ACAGAGCGCATCAGAGTCTGCGAGCTCAAGGCCTTCATTTGATACATGGACTTGCTTGCA
TCATCATCACGGCTCCTCTCGAAATTGCTTCCGAAGACCTTCTCCTGAGCCTCTCGCTCG
CGCATGAAGCCATCGAGCTTTTCAGCTTGCACGATGAAAGCCAAGTAGGCCTCTTGCTGT
TCACTGCTTCGCATTCCACGCTGGAGCAGACGGCACGTTGATACCAGGCTACTCCTGGCT...
```

We want to obtain a list of the fasta "headers" the lines beginning with ">". Remember 'grep'?

The following line will pull all of the headers and put them in a new file called 'fasta_headers.txt'
```
$ grep ">" hard_filtered_transcripts.fasta > fasta_headers.txt
```

If you check it out, you'll see what I mean:
```
$ less fasta_headers.txt
>NODE_1_length_8049_cov_42.810250_g0_i0
>NODE_2_length_7760_cov_26.543769_g1_i0
>NODE_3_length_6761_cov_90.052741_g2_i0
>NODE_4_length_6504_cov_357.418435_g3_i0
>NODE_5_length_6454_cov_80.888681_g4_i0
>NODE_6_length_6433_cov_92.267857_g5_i0
>NODE_7_length_6426_cov_83.689039_g6_i0
>NODE_8_length_6371_cov_69.835495_g7_i0
>NODE_9_length_6336_cov_38.054398_g8_i0
>NODE_10_length_6308_cov_31.683975_g9_i0
>NODE_11_length_6297_cov_28.021767_g10_i0
>NODE_12_length_6290_cov_28.421888_g11_i0
```

Now, we want to adjust the format a little bit. R likes to use "comma separated value" (.csv) files, among others. We're going to turn our file into a csv by swapping _ for , and then sending that output to a new file called fasta_headers.csv. 
```
$ sed 's/_/,/g' fasta_headers.txt > fasta_headers.csv
```

We're ready for R. 

### Rank-order plot of contig length

Open Rstudio (or R, if you don't have Rstudio). 

In the console, do this (matching your own path, not mine):
```
> data <- read.csv(file = "C:/Users/Charles/Desktop/fasta_headers.csv", header = F)

> head(data)

    V1 V2     V3   V4  V5        V6 V7 V8
1 NODE  1 length 8049 cov  42.81025 g0 i0
2 NODE  2 length 7760 cov  26.54377 g1 i0
3 NODE  3 length 6761 cov  90.05274 g2 i0
4 NODE  4 length 6504 cov 357.41843 g3 i0
5 NODE  5 length 6454 cov  80.88868 g4 i0
6 NODE  6 length 6433 cov  92.26786 g5 i0
```

You can see that R took in the data, and made each column based on where the commas were. Here, V4 is length, and V6 is coverage. 

Try this:
```
> plot(data$V4)
```

### Contig length relative distribution
```
> plot(density(data$V4))
```

This uses the same data, but it gives us different information - can you tell what the difference is?

### Distribution of coverage

```
> plot(density(data$V6), xlim = c(0,1000)
```

