## Coriell Bioinformatics Genome Log

### hg38
*2019-05-14*
Downloaded the Ensembl gene annotations in GFF3 format from the NCBI ftp site

```bash
[kkeith]$ cd /mnt/data/gdata/human/hg38
[kkeith]$ wget ftp://ftp.ensembl.org/pub/release-85/gff3/homo_sapiens/Homo_sapiens.GRCh38.85.gff3.gz
```

*2019-05-02* 
Used UCSC's fetchChromSizes to get the chromosome size file necessary for many of their tools

```bash
[kkeith]$ /mnt/data/gdata/human/hg38
[kkeith]$ fetchChromSizes hg38 > hg38.chrom.sizes

[kkeith]$ cd /mnt/data/gdata/human/hg38/hg38
[kkeith]$ gunzip Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz 
[kkeith]$ samtools faidx Homo_sapiens.GRCh38.dna.primary_assembly.fa
[kkeith]$ cut -f 1,2 Homo_sapiens.GRCh38.dna.primary_assembly.fa.fai > hg38.chrom.sizes
```

-

*2019-05-01*

See `2019-05-01_genome_directory_tree.txt` for the status of the genome directory before I started changing things

```bash
[kkeith]$ /mnt/data/gdata
[kkeith]$ tree * > 2019-05-01_genome_directory_tree.txt
```
-

```bash
# change group and permissions for everything so I can work with it
[kkeith]$ sudo chgrp -R research *
[kkeith]$ sudo chmod -R 775 *

# get hg38 genomes/annotations
[kkeith]$ cd /mnt/data/gdata/human/
[kkeiht]$ cd hg38
[kkeith]$ mkdir hg38
[kkeith]$ cd hg38_soft_masked/
[kkeith]$ wget ftp://ftp.ensembl.org/pub/release-85/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz
[kkeith]$ cd ..
[kkeith]$ wget ftp://ftp.ensembl.org/pub/release-85/gtf/homo_sapiens/Homo_sapiens.GRCh38.85.gtf.gz
[kkeith]$ cd hg38
[kkeith]$ wget ftp://ftp.ensembl.org/pub/release-85/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz

# make indices
[kkeith]$ mkdir bt2_index_hg38
[kkeith]$ bowtie2-build --threads 16 Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz bt2_index_hg38/bt2_index_hg38
```

### Stuff Transferred from Fels

:woman_shrugging: