
### Cat (concatenate) all raw reads into a single file:

```
cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ cat Akle_TTAGGC_L004_R1_* > Akle_raw_R1.fastq.gz

cagood@benthos:~/Shantou_2018/Seq_data/Amphidinium_klebsii/raw$ cat Akle_TTAGGC_L004_R2_* > Akle_raw_R2.fastq.gz
```


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
