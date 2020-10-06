## Coriell Server 10.1.105.13


### hg38 STAR Indices
*2020-07-22*

Because the first use of this server is for the 2020 Coriell Bioinformatics Research Experience, which is teaching the students RNA-seq, we needed STAR indices immediately for the course. Copied hg38 fasta and gft files from the original server (10.1.105.11) and tried to copy the STAR index files. 

```bash
# set up the genome folders
[kkeith]$ cd /mnt/data
[kkeith]$ sudo mkdir gdata
[kkeith]$ sudo chown kkeith:research gdata
[kkeith]$ cd gdata
[kkeith]$ mkdir human
[kkeith]$ mkdir human/hg38
[kkeith]$ mkdir human/hg38/chr21

# grab the mini chr21 genome files for demos from the other server
[kkeith]$ sftp kkeith@10.1.105.11
sftp> cd /mnt/data/gdata/human/hg38/chr21
sftp> get STAR_index/*
sftp> get homo_sapiens_hg38_chr21.fa
sftp> get homo_sapiens_hg38_chr21.gtf
sftp> exit

# rearrange the files
[kkeith]$ mv * human/hg38/chr21/
[kkeith]$ cd human/hg38/chr21/
[kkeith]$ mkdir STAR_index
[kkeith]$ mv * STAR_index/
[kkeith]$ cd STAR_index/
[kkeith]$ mv homo_sapiens_hg38_chr21.fa homo_sapiens_hg38_chr21.gtf ../

# grab the full hg38 fasta and GTF files (turns out there was no STAR index for them)
[kkeith]$ cd ..
[kkeith]$ ftp kkeith@10.1.105.11
sftp> cd /mnt/data/gdata/human/hg38
sftp> get Homo_sapiens.GRCh38.85.gtf
sftp> get Homo_sapiens.GRCh38.dna.primary_assembly.fa
sftp> get Homo_sapiens.GRCh38.dna.primary_assembly.fa.fai
sftp> exit
[kkeith]$ mv Homo_sapiens.GRCh38.* ../
```

However, when I tried aligning with the copied chr21 STAR index, STAR gave this error `EXITING because of FATAL ERROR: Genome version: 2.7.1a is INCOMPATIBLE with running STAR version: 2.7.5a
SOLUTION: please re-generate genome from scratch with running version of STAR, or with version: 2.7.4a`. The index needed to be deleted and the genome re-indexed. And also the chr21 "GTF" file turned out to be a copy of the fasta file, so I had to re-make that as well.

```bash
### STAR index the demo chr21 genome
[kkeith]$ tmux new -s indexing
[kkeith]$ pwd
/mnt/data/gdata/human/hg38/chr21
[kkeith]$ STAR --runMode genomeGenerate --genomeDir STAR_index --genomeFastaFiles homo_sapiens_hg38_chr21.fa --sjdbGTFfile homo_sapiens_hg38_chr21.gtf

### make a correctly-formatted GTf file from the full GTF file
[detached (from session indexing)]
[kkeith]$ pwd
/mnt/data/gdata/human/hg38/chr21
[kkeith]$ cd ../
[kkeith]$ grep '^21' Homo_sapiens.GRCh38.85.gtf > chr21/homo_sapiens_hg38_chr21.gtf

### and index the chr21 fasta file just in case
[kkeith]$ cd chr21
[kkeith]$ samtools faidx homo_sapiens_hg38_chr21.fa
```
Made a STAR index for the full hg38 genome as well

```bash
[kkeith]$ tmux new -s indexing
[kkeith]$ pwd
/mnt/data/gdata/human/hg38/chr21
[kkeith]$ cd ../
[kkeith]$ STAR --runMode genomeGenerate --runThreadN 16 --genomeDir star_index_hg38 --genomeFastaFiles Homo_sapiens.GRCh38.dna.primary_assembly.fa --sjdbGTFfile Homo_sapiens.GRCh38.85.gtf
```