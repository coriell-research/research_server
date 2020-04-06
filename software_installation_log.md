# Software Installation Log

---

**WARNING:** Before installing **R packages**, you need to go into `root`'s `.bash_profile` and uncomment the line `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/programs/anaconda3/lib/` and comment the line `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ROOTSYS/lib`. This allows root `R` to find the libssl path correctly. **DONT' FORGET** to go back into the `.bash_profile` and swap it back when you're done!!!

---

*2020-03-13* Install **RSeQC** for in-depth RNA-seq quality analysis

```bash
[kkeith]$ su
[root]# conda create --name rseqc
[root]# conda activate rseqc
(rseqc)[root]# conda install -c bioconda rseqc
(rseqc)[root]# conda deactivate
[root]# exit
# test program as normal user
[kkeith]$ conda activate rseqc
[kkeith]$ bam_stat.py
Usage: bam_stat.py [options]

Summarizing mapping statistics of a BAM or SAM file. 



Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -i INPUT_FILE, --input-file=INPUT_FILE
                        Alignment file in BAM or SAM format.
  -q MAP_QUAL, --mapq=MAP_QUAL
                        Minimum mapping quality (phred scaled) to determine
                        "uniquely mapped" reads. default=30
```

*2020-02-03* Install Bioconductor R package **epihet** for methylation heterogeneity analysis.

```bash
[kkeith]$ su
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]# R
> Biocmanager::install("epihet")
>
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
```

*2020-01-10* Install Bioconductor R package **PuerCN** for copy number analysis for partial genome sequencing

```bash
[kkeith]$ su
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]# R
> BiocManager::install("PureCN")
> library(PureCN)
> q()
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
```

*2020-01-08* Install CNVkit for copy number analysis

```bash
[kkeith]$ su
[root]# conda install -c bioconda cnvkit
UnsatisfiableError: The following specifications were found to be incompatible with each other:

# put it in it's own environment
[root]# conda create --name cnvkit
[root]# conda activate cnvkit
(cnvkit)[root]# conda install -c bioconda cnvkit
UnsatisfiableError: The following specifications were found to be incompatible with each other:

# install with pip
[root]# pip install cnvkit
```

*2020-01-06* Install MultiQC for quality control report aggregating

```bash
[kkeith]$ su
[root]# conda install -c bioconda multiqc
UnsatisfiableError: The following specifications were found                                                              
to be incompatible with the existing python installation in your environment:

Specifications:

  - multiqc -> python[version='2.7.*|3.5.*']
  - multiqc -> python[version='>=2.7,<2.8.0a0|>=3.5,<3.6.0a0']

Your python: python=3.7

If python is on the left-most side of the chain, that's the version you've asked for.
When python appears to the right, that indicates that the thing on the left is somehow
not available for the python version you are constrained to. Note that conda will not
change your python version to a different minor version unless you explicitly specify
that.

The following specifications were found to be incompatible with each other:



Package ca-certificates conflicts for:
python=3.7 -> openssl[version='>=1.0.2p,<1.0.3a'] -> ca-certificates
multiqc -> python=3.5 -> ca-certificates
Package wheel conflicts for:
multiqc -> python=3.5 -> pip -> wheel
python=3.7 -> pip -> wheel
Package pip conflicts for:
multiqc -> python=3.5 -> pip
python=3.7 -> pip
Package setuptools conflicts for:
python=3.7 -> pip -> setuptools
multiqc -> setuptools
Package certifi conflicts for:
python=3.7 -> pip -> setuptools -> certifi[version='>=2016.09|>=2016.9.26']

# SOLUTION: install MutliQC in its own 
[root]# conda create --name multiqc
[root]# conda activate multiqc
[root]# conda install -c bioconda multiqc
[root]# conda deactive multiqc
[root]# exit
```

-

*2019-12-18* Install R package **caret** for machine learning

```bash
[kkeith]$ su
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]# R
> install.packages('caret')
> q()
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
```

*2019-12-17* Install **xclip** and **xsel** for copying to clipboard

```bash
[kkeith]$ sudo yum install xclip
[kkeith]$ sudo yum install xsel
```

*2019-12-06* Install R Bioconductor package **liftOver** for translating genomic coordinates to other genomes.

```bash
> BiocManager::install("liftOver")
```

*2019-12-06* Install R package **vroom** for fast reading of rectangular data

```bash
> install.packages('vroom')
```

*2019-12-04* Install **ANNOVAR**

Downloaded ANNOVAR from the program website <http://annovar.openbioinformatics.org/en/latest/user-guide/download/>. I filled out the form at the link as directed and got an emailed link to download ANNOVAR. The folder was uploaded to my home directory on the server using Macfusion, then installed using the code below. ANNOVAR also requires annotation databases to work with; I downloaded the suggested databases to start with, but a full list of the available databases is at the link <http://annovar.openbioinformatics.org/en/latest/user-guide/download/>

```bash
[kkeith]$ pwd
/home/kkeith
[kkeith]$ cd /usr/local/programs/
[kkeith]$ sudo chown -R root:root annovar

### download databases for ANNOVAR; these are the ones suggested in the getting started documentation but more are available
[kkeith]$ sudo perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar refGene humandb/
[kkeith]$ sudo perl annotate_variation.pl -buildver hg19 -downdb cytoBand humandb/
[kkeith]$ sudo perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar exac03 humandb/ 
[kkeith]$ sudo perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar avsnp147 humandb/ 
[kkeith]$ sudo perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar dbnsfp30a humandb/

# install genocode annotations instead
[kkeith]$ sudo perl annotate_variation.pl -buildver hg19 -downdb -webfrom annovar ensGene humandb/
```

*2019-11-21* Install R package **dbplyr** for using tidyverse syntax to query SQL tables

```bash
[kkeith]$ su
# went and edited root's .bash_profile as noted above
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]$ R
> install.packages('dbplyr')
> q()
Save workspace image? [y/n/c]: n
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]# exit
```

*2019-11-21* Install R package **dtplyr** for faster data processing using tidyverse syntax with data.tables

```bash
[kkeith]$ su
# went and edited root's .bash_profile as noted above
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]$ R
> install.packages('dtplyr')
> q()
Save workspace image? [y/n/c]: n
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]# exit
```

*2019-11-21* Install R package **data.table** for faster data processing

```bash
[kkeith]$ su
# went and edited root's .bash_profile as noted above
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]$ R
> install.packages('data.table')
> q()
Save workspace image? [y/n/c]: n
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]# exit
```

*2019-11-12* Install Bioconductor package **ChAMP** for 450K array normalization and analysis

```bash
[kkeith]$ su
# went and edited root's .bash_profile as noted above
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]$ R
> BiocManager::install("ChAMP")
> q()
Save workspace image? [y/n/c]: n
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile
[root]# exit
```

*2019-11-07* Install Bioconductor package **TCGAbiolinks** for downloading TCGA data

```bash
[kkeith]$ su
[root]# R
> BiocManager::install("TCGAbiolinks")
```

*2019-11-01* Install Bioconductor gene annotation packages

```bash
[kkeith]$ su
[root]# R
# human
> BiocManager::install("TxDb.Hsapiens.UCSC.hg19.knownGene")
> BiocManager::install("TxDb.Hsapiens.UCSC.hg38.knownGene")
# mouse
> BiocManager::install("TxDb.Mmusculus.UCSC.mm9.knownGene")
> BiocManager::install("TxDb.Mmusculus.UCSC.mm10.knownGene")
```

*2019-11-01* Updated all Bioconductor packages to version 3.9. This was required because the R version on the server is 3.6 and Bioconductor 3.8 only works up to R 3.5.

```bash
[kkeith]$ su
[root]# R
> BiocManager::install(version = "3.9")
```

*2019-10-22* Install **seqtk** with conda.

```bash
[kkeith]$ su
[root]# conda install -c bioconda seqtk
[root]# y
[root]# exit
```

#### Install all the UCSC Tools in Their Own `conda` environment
*2019-10-15*

Because of compatibility issues with other software / `conda` stuff, many of the UCSC tools weren't installling in the main environment, so they went into their own environment.

```bash
[kkeith]$
[root]# su

### make the new conda environment
(ucsc_tools)[root]# conda create --name ucsc_tools
(ucsc_tools)[root]# conda activate ucsc_tools

### install all the UCSC tools
(ucsc_tools)[root]# conda install -c mvdbeek ucsc_tools

### test installation
(ucsc_tools)[root]# bigWigToBedGraph 
bigWigToBedGraph: error while loading shared libraries: libssl.so.1.0.0: cannot open shared object file: No such file or directory

### fix issue (as I have before) by making a softlink for libssl.so.1.0.0 to the most currect version of the library
(ucsc_tools)[root]# cd /usr/local/programs/anaconda3/envs/ucsc_tools/lib/
(ucsc_tools)[root]# ln -s libssl.so.1.1 libssl.so.1.0.0

### test again
(ucsc_tools)[root]# bigWigToBedGraph 
bigWigToBedGraph: error while loading shared libraries: libcrypto.so.1.0.0: cannot open shared object file: No such file or directory

### softlink libcrypto now
(ucsc_tools)[root]# ln -s libcrypto.so.1.1 libcrypto.so.1.0.0

### test again
bigWigToBedGraph 
bigWigToBedGraph - Convert from bigWig to bedGraph format.
usage:
   bigWigToBedGraph in.bigWig out.bedGraph
options:
   -chrom=chr1 - if set restrict output to given chromosome
   -start=N - if set, restrict output to only that over start
   -end=N - if set, restict output to only that under end
   -udcDir=/dir/to/cache - place to put cache for remote bigBed/bigWigs

### Now that works as root, test again as normal user, not root
(ucsc_tools)[root]# conda deactivate
[root]# exit
[kkeith]$ conda activate ucsc_tools
(ucsc_tools)[kkeith]$ bigWigToBedGraph 
bigWigToBedGraph - Convert from bigWig to bedGraph format.
usage:
   bigWigToBedGraph in.bigWig out.bedGraph
options:
   -chrom=chr1 - if set restrict output to given chromosome
   -start=N - if set, restrict output to only that over start
   -end=N - if set, restict output to only that under end
   -udcDir=/dir/to/cache - place to put cache for remote bigBed/bigWigs 
```

-

*2019-10-09* Install R package **viridis**

```bash
[kkeith]$ su
[root]# R
> install.packages('viridis')
```

*2019-10-09* Install R package **mclust**

```bash
[kkeith]$ su
[root]# R
> install.packages('mclust')
```

*2019-10-09* Install R package **cowplot**

```bash
[kkeith]$ su
[root]# R
> install.packages('cowplot')
```

*2019-10-09* Install R package **Seurat**

```bash
[kkeith]$ su
[root]# R
> install.packages('Seurat')
```

*2019-09-30* Install R package **pvclust**

```bash
[kkeith]$ su
[root]# R

R version 3.5.2 (2018-12-20) -- "Eggshell Igloo"
Copyright (C) 2018 The R Foundation for Statistical Computing
Platform: x86_64-redhat-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> install.packages('pvclust')
Installing package into ‘/usr/lib64/R/library’
(as ‘lib’ is unspecified)
--- Please select a CRAN mirror for use in this session ---
trying URL 'https://cloud.r-project.org/src/contrib/pvclust_2.0-0.tar.gz'
Content type 'application/x-gzip' length 104057 bytes (101 KB)
==================================================
downloaded 101 KB

* installing *source* package ‘pvclust’ ...
** package ‘pvclust’ successfully unpacked and MD5 sums checked
** R
** data
** byte-compile and prepare package for lazy loading
** help
*** installing help indices
  converting help for package ‘pvclust’
    finding HTML links ... done
    lung                                    html  
    msfit                                   html  
    msplot                                  html  
    plot.pvclust                            html  
    print.pvclust                           html  
    pvclust                                 html  
    pvpick                                  html  
    seplot                                  html  
** building package indices
** testing if installed package can be loaded
* DONE (pvclust)
Making 'packages.html' ... done

The downloaded source packages are in
	‘/tmp/Rtmpui3ej5/downloaded_packages’
Updating HTML index of packages in '.Library'
Making 'packages.html' ... done
> q()
Save workspace image? [y/n/c]: n
[root@cbix uniq]# exit
exit
```

#### Adding Packages to the Python2.7 Anaconda Environment
*2019-09-20*

Needed additional packages in the python2.7 environment to run the DREAM script

```bash
[kkeith]$ su
[root]# conda activate python2.7
(python2.7)[root]# conda activate python2.7
(python2.7)[root]# conda install -c bioconda pysam
(python2.7)[root]# pip install timex
```
-

And install `timex` in the normal environment as well, should allow me to run the python3 version of the script.

```bash
### install same packages in the normal environment as well
(python2.7)[root]# conda deactivate
[root]# pip install timex
```

*2019-09-20* Organize DREAM folder in `/usr/local/programs`

```bash
[kkeith]$ cd /usr/local/programs/
[kkeith]$ sudo mkdir dream
[kkeith]$ sudo mv count_SmaI_CH3* dream/
[kkeith]$ sudo cp /mnt/data/bix_server/disk36t/data_jj/dream/tools/dream_python/hg19c9eyhhv_smai_sites.txt ./
[kkeith]$ ll dream
total 12204
-rwxrwxr-x. 1 root root    14520 Apr 22  2014 count_SmaI_CH3.py
-rwxrwxr-x. 1 root root    14571 Mar 27 18:15 count_SmaI_CH3_py3.py
-rw-r--r--. 1 root root 12462024 Sep 20 11:15 hg19c9eyhhv_smai_sites.txt
[kkeith]$ sudo cp /mnt/data/bix_server/disk36t/data_jj/dream/tools/dream_r_human/print_stats_awk.sh /usr/local/programs/dream/
[kkeith]$ sudo chmod 755 /usr/local/programs/dream/print_stats_awk.sh 
```

*2019-09-06* Installed R packages for working with/downloading GEO data **GEOmetadb**, **GEOquery**, and **SRAdb**

```bash
[kkeith]$ su
[root]# R
```
```r
R version 3.5.2 (2018-12-20) -- "Eggshell Igloo"
Copyright (C) 2018 The R Foundation for Statistical Computing
Platform: x86_64-redhat-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.
> BiocManager::install("GEOmetadb")
> BiocManager::install("GEOquery")
> BiocManager::install("SRAdb")
> sessionInfo()
R version 3.5.2 (2018-12-20)
Platform: x86_64-redhat-linux-gnu (64-bit)
Running under: CentOS Linux 7 (Core)

Matrix products: default
BLAS/LAPACK: /usr/lib64/R/lib/libRblas.so

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
 [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
 [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
 [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
 [9] LC_ADDRESS=C               LC_TELEPHONE=C            
[11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

loaded via a namespace (and not attached):
[1] BiocManager_1.30.4 compiler_3.5.2     tools_3.5.2 
```

*2019-08-26* Installed UCSC's **bedClip** using conda

```bash
[kkeith]$ su
[root]# conda install -c bioconda ucsc-bedclip
```
---

*2019-08-16* JJ changed hostname from localhost to **cbix**

added the following line to /etc/sysconfig/network

```bash
    HOSTNAME=cbix
```

edited /etc/hosts
by changing the first line

```bash
    127.0.0.1       cbix
    ::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
```

issued a command

```bash
    sudo hostname cbix
```
---

*2019-08-03* Tried to install **CNVkit** using conda

```bash
[kkeith]$ su
[root]# conda create --name cnvkit
[root]# conda activate cnvkit
(cnvkit)[kkeith]$ conda install -c bioconda cnvkit
Solving environment: failed

# >>>>>>>>>>>>>>>>>>>>>> ERROR REPORT <<<<<<<<<<<<<<<<<<<<<<

    Traceback (most recent call last):
      File "/usr/local/programs/anaconda3/lib/python3.7/site-packages/conda/exceptions.py", line 1049, in __call__
        return func(*args, **kwargs)
      File "/usr/local/programs/anaconda3/lib/python3.7/site-packages/conda/cli/main.py", line 84, in _main
        exit_code = do_call(args, p)
      File "/usr/local/programs/anaconda3/lib/python3.7/site-packages/conda/cli/conda_argparse.py", line 82, in do_call
        exit_code = getattr(module, func_name)(args, parser)
      File "/usr/local/programs/anaconda3/lib/python3.7/site-packages/conda/cli/main_install.py", line 20, in execute
        install(args, parser, 'install')
      File "/usr/local/programs/anaconda3/lib/python3.7/site-packages/conda/cli/install.py", line 319, in install
        handle_txn(unlink_link_transaction, prefix, args, newenv)
    UnboundLocalError: local variable 'unlink_link_transaction' referenced before assignment

`$ /usr/local/programs/anaconda3/bin/conda install -c bioconda cnvkit`
An unexpected error has occurred. Conda has prepared the above report.

### 2019-08-13; sucessfully installed with pip
[root]# pip install cnvkit

### remove now unnecessary conda environment
[root]# conda env remove --name cnvkit

Remove all packages in environment /usr/local/programs/anaconda3/envs/cnvkit:
```
---

*2019-07-31* Install **imagemagick** using conda

```bash
[kkeith]$ su
[root]# conda new --name imagemagick
[root]# conda activate imagemagick
[root]# conda install -c conda-forge imagemagick
[root]# magick
Error: Invalid argument or not enough arguments

Usage: magick tool [ {option} | {image} ... ] {output_image}
Usage: magick [ {option} | {image} ... ] {output_image}
       magick [ {option} | {image} ... ] -script {filename} [ {script_args} ...]
       magick -help | -version | -usage | -list {option}

[root]# exit
```
---

*2019-07-29* Install **refgenie** using pip

```bash
[kkeith]$ su
[root]# pip install refgenie
```
---

*2019-07-25*
Install **lumpy-sv** using conda

```bash
[root]# conda create --name lumpy
[root]# conda activate lumpy
(lumpy)[root]# conda install -c bioconda lumpy-sv
(lumpy)[root]# lumpy

Program: ********** (v 0.2.13)
Author:  Ryan Layer (rl6sf@virginia.edu)
Summary: Find structural variations in various signals.

Usage:   ********** [OPTIONS] 

Options: 
	-g	Genome file (defines chromosome order)
	-e	Show evidence for each call
	-w	File read windows size (default 1000000)
	-mw	minimum weight for a call
	-msw	minimum per-sample weight for a call
	-tt	trim threshold
	-x	exclude file bed file
	-t	temp file prefix, must be to a writeable directory
	-P	output probability curve for each variant
	-b	output BEDPE instead of VCF
	-sr	bam_file:<file name>,
		id:<sample name>,
		back_distance:<distance>,
		min_mapping_threshold:<mapping quality>,
		weight:<sample weight>,
		min_clip:<minimum clip length>,
		read_group:<string>

	-pe	bam_file:<file name>,
		id:<sample name>,
		histo_file:<file name>,
		mean:<value>,
		stdev:<value>,
		read_length:<length>,
		min_non_overlap:<length>,
		discordant_z:<z value>,
		back_distance:<distance>,
		min_mapping_threshold:<mapping quality>,
		weight:<sample weight>,
		read_group:<string>

	-bedpe	bedpe_file:<bedpe file>,
		id:<sample name>,
		weight:<sample weight>
(lumpy)[root]# conda deactivate
```
---

*2019-07-25*
Install bioconductor package **QDNAseq**

```bash
[root]# R
> if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

> BiocManager::install("QDNAseq")
> q()
```

### Install CNVnator
*2019-07-25*

**NOTE:** NOT INSTALLED

ATTEMPT to install **CNVnator**, first you have to install **ROOT**, a data analysis framework. I downloaded the CentOS binaries to my computer and uploaded them to the server as root using Macfusion to `/usr/local/programs`

```bash
# from /usr/local/programs
# unpack the binaries
[root]# tar -xvzf root_v6.16.00.Linux-centos7-x86_64-gcc4.8.tar.gz
```
Edited my `.bash_profile` only, `/home/kkeith/.bash_profile` to include the ROOT PATH as directed in the ROOT installation as a test. Then I installed CNVnator as directed in the CNVnator GitHub README installation instructions <https://github.com/abyzovlab/CNVnator>

```bash
# from /usr/local/programs
[root]# git clone https://github.com/abyzovlab/CNVnator.git
[root]# cd CNVnator/
[root]# ln -s /usr/local/programs/anaconda3/bin/samtools samtools

unzip CNVnator_v0.4.zip
tar -xzvf samtools-1.9.tar.bz2 
cd samtools
make
cd CNVnator_v0.4/
ln -s /usr/local/programs/samtools samtools
make
```
```bash
rpm -Uvh alien-8.90-3.el7.nux.noarch.rpm 
```
---

*2019-07-24*
Jozef installed **magicblast**


```bash
cd /usr/local/programs/
sudo wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/magicblast/LATEST/ncbi-magicblast-1.4.0-x64-linux.tar.gz
sudo tar -xzvf ncbi-magicblast-1.4.0-x64-linux.tar.gz
rm ncbi-magicblast-1.4.0-x64-linux.tar.gz

sudo nano /etc/profile.d/magic_blast.sh
```
---

*2019-07-24*
Install **bwa** using conda

```bash
[kkeith]$
[root]# su
[root]# tmux new -s bwa
[root]# conda install -c bioconda bwa
[detached (from session bwa)]
[root]# bwa

Program: bwa (alignment via Burrows-Wheeler transformation)
Version: 0.7.17-r1188
Contact: Heng Li <lh3@sanger.ac.uk>

Usage:   bwa <command> [options]

Command: index         index sequences in the FASTA format
         mem           BWA-MEM algorithm
         fastmap       identify super-maximal exact matches
         pemerge       merge overlapping paired ends (EXPERIMENTAL)
         aln           gapped/ungapped alignment
         samse         generate alignment (single ended)
         sampe         generate alignment (paired ended)
         bwasw         BWA-SW for long queries

         shm           manage indices in shared memory
         fa2pac        convert FASTA to PAC format
         pac2bwt       generate BWT from PAC
         pac2bwtgen    alternative algorithm for generating BWT
         bwtupdate     update .bwt to the new format
         bwt2sa        generate SA from BWT and Occ

Note: To use BWA, you need to first index the genome with `bwa index'.
      There are three alignment algorithms in BWA: `mem', `bwasw', and
      `aln/samse/sampe'. If you are not sure which to use, try `bwa mem'
      first. Please `man ./bwa.1' for the manual.
[root]# tmux kill-session -t bwa
[root]# exit
```

### Install GATK
*2019-07-22*

```bash
[kkeith]$ su
[root]# conda config
[root]# tmux new -s gatk
[root]# conda create --name gatk
[root]# conda activate gatk
(gatk)[root]# conda install gatk
(gatk)[root]# gatk GATK jar file not found. Have you run "gatk-register"?
(gatk)[root]# gatk-register
  It looks like GATK has not yet been installed.

  Usage: gatk-register /path/to/GenomeAnalysisTK[-3.8.tar.bz2|.jar]

  Due to license restrictions, this recipe cannot distribute 
  and install GATK directly. To fully install GATK, you must 
  download a licensed copy of GATK from the Broad Institute: 
    https://www.broadinstitute.org/gatk/download/ 
  and run (after installing this package):
    gatk-register /path/to/GenomeAnalysisTK[-3.8.tar.bz2|.jar], 
   This will copy GATK into your conda environment.
```
Went to the link, downloaded the file, and transferred the file to `/usr/local/programs/` and unzipped the file using Macfusion

---

None of the files I tried worked for `conda`, so I downloaded the file to `/usr/local/progams/` and unzipped it. GATK is ready to go then, you just need to export the path and set up an alias

```bash
# remove conda environment because we don't need that now
[root]# conda remove --name gatk --all

# exported gatk path to everyone's ~/.bash_profile
[kkeith]$ for i in /home/*/.bash_profile; do echo 'export PATH=$PATH:/usr/local/programs/gatk-4.1.2.0/gatk' >> $i; done
-bash: /home/hvaidya/.bash_profile: Permission denied
-bash: /home/lscheinfeldt/.bash_profile: Permission denied
[kkeith]$ su
[root]# echo 'export PATH=$PATH:/usr/local/programs/gatk-4.1.2.0/gatk' >> /home/hvaidya/.bash_profile
[root]# echo 'export PATH=$PATH:/usr/local/programs/gatk-4.1.2.0/gatk' >> /home/lscheinfeldt/.bash_profile

# added alias for gatk to alias file
[kkeith]$ su
[root]# nano /etc/profile.d/aliases.sh
[root]# less /etc/profile.d/aliases.sh
alias methclone='/usr/local/programs/methclone-master/bin/methclone'

alias gdc-client='/usr/local/programs/tcga_gdc-client/gdc-client'

alias methclone2='/usr/local/programs/methclone2/bin/methclone'

alias gatk='/usr/local/programs/gatk-4.1.2.0/gatk'
```

### Weird Java Error
*2019-07-11*

*2019-07-19* **NOTE:** Ended up reinstalling conda and all programs, see `update_conda_to_2019-03.md`

When I tried to run `fastqc`, I got a weird error

```bash
[kkeith]$ fastqc
Exception in thread "main" java.lang.NullPointerException
```
Tried updating/installing openjdk, but that didn't work

```bash
[root]# su -c "yum install java-1.8.0-openjdk"
```
Tried to update fastqc (which was installed using conda) and got another weird error (below, only showing relevant line).

```bash
[root]# conda update fastqc
OSError: /lib64/libstdc++.so.6: version `CXXABI_1.3.8' not found (required by /usr/local/programs/anaconda3/lib/././libicuuc.so.58
```
Turned out the softlink in the anaconda library was broken. Fixed the issue by adding the following soft links

```bash
[root]# ln -s /usr/local/programs/anaconda3/lib/libstdc++.so.6.0.25 /usr/local/programs/anaconda3/lib/libstdc++.so
[root]# ln -s /usr/local/programs/anaconda3/lib/libstdc++.so.6.0.25 /usr/local/programs/anaconda3/lib/libstdc++.so.6
```
---

*2019-06-25* Install **jq** to parse json files Gencove API returns on the commandline

```bash
[kkeith]$ su
[root]# conda install -c conda-forge jq
```
---

*2019-06-25* Install **Gencove API** to download data using pip.

```bash
[kkeith]$ su
[root]# pip install gencove
```
---

*2019-06-22* Install **libiconv** using conda, which MEME needs to run

```bash
[kkeith]$ conda install -c conda-forge libiconv
[root]# conda install -c conda-forge libiconv
```
---

*2019-06-21* Install **epic2** using conda

```bash
[kkeith]$ su
[root]# conda install -c bioconda epic2 
```
---

*2019-06-19* Install **perl-GDGraph** using yum

```bash
[jjelinek]$ su
[root]# yum install perl-GDGraph
```

### Install cut&run pipeline
*2019-06-06*

#### Install the dependencies not alread present on the server
*2019-06-06* Install **atactk**, following the instructions on its GitHub README, for cut&run pipeline

```bash
### install dependencies
# pysam already installed
[root]# conda install -c conda-forge python-levenshtein
[root]# conda install -c conda-forge sexpdata

### install atactk
[root]# cd /usr/local/programs
[root]# git clone https://github.com/ParkerLab/atactk

### test installation using atactk command make_cut_matrix
[root]# make_cut_matrix
usage: make_cut_matrix [-h] (-a | -d) -b BINS [-F EXCLUDE_FLAGS]
                       [-f INCLUDE_FLAGS] [-o CUT_POINT_OFFSET] [-p PARALLEL]
                       [-q QUALITY] [-r EXTENSION] [-v] [--version]
                       BAM-file-of-aligned-reads BED-file-of-motifs
make_cut_matrix: error: the following arguments are required: -b/--bins, BAM-file-of-aligned-reads, BED-file-of-motifs
```
---

Install **bedops** using conda for cut&run pipeline

```bash
[root]# conda install -c bioconda bedops
```
---

Install **MEME** using conda for cut&run pipeline

```bash
[root]# conda install -c bioconda meme
```
---

Install **picard** using conda for cut&run pipeline

```bash
[root]# conda install -c bioconda picard
```
---

*2019-05-07* Install R package **MethylCal** using R

```bash
[kkeith]$ su
[root]# R
```

```R
> install.packages("INLA", repos = c(getOption("repos"), INLA = "https://inla.r-inla-download.org/R/stable"), dep = TRUE)
> devtools::install_github("lb664/MethylCal", build_opts = c("--no-resave-data", "--no-manual"))
> library(MethylCal)
Loading required package: INLA
Loading required package: Matrix
Loading required package: sp
This is INLA_18.07.12 built 2019-05-07 13:40:28 UTC.
See www.r-inla.org/contact-us for how to get help.
To enable PARDISO sparse library; see inla.pardiso()
Loading required package: lattice
Loading required package: latticeExtra
Loading required package: RColorBrewer
```
---

*2019-05-02* Re-installed **qiime2** using conda and the qiime2 documentation's suggest commands after I broke Anaconda

```bash
[root]# cd /usr/local/programs
[root]# wget https://data.qiime2.org/distro/core/qiime2-2019.1-py36-linux-conda.yml
[root]# conda env create -n qiime2-2019.1 --file qiime2-2019.1-py36-linux-conda.yml
[root]# rm qiime*
```
---

*2019-05-02* Install UCSC's **bedSort** to sort my bed files

```bash
[root]# conda install -c bioconda ucsc-bedsort
```
---

*2019-05-02* Install UCSC's **fetchChromSizes** with conda. Need it to get the chromosome sizes for bedGraphtoBigWig

```bash
[root]# conda install -c bioconda ucsc-fetchchromsizes
```
---

*2019-05-02* Install UCSC's **bedGraphtoBigWig** with conda

```bash
[root]# conda install -c bioconda ucsc-bedgraphtobigwig
```
When I tried to use it, bedGraphtoBigWig gave the following error:

```
bedGraphToBigWig: error while loading shared libraries: libssl.so.1.0.0: cannot open shared object file: No such file or directory
```
bedGraphtoBigWig needs an old Solved the problem by softlinking the library Anaconda had softlinked to libssl.so.1.0.0 (as suggested also in this Stack Exchange post <https://askubuntu.com/questions/339364/libssl-so-10-cannot-open-shared-object-file-no-such-file-or-directory>)

```bash
[kkeith]$ cd /usr/local/programs/anaconda3/lib
[kkeith]$ sudo ln -s libssh2.so.1.0.1 libssl.so.1.0.0
```
---

*2019-05-02* Install **macs2** with conda, because previous attempt with pip failed. After killing conda a reinstalling all packages, installed it again in the python2.7 conda environment

```bash
[kkeith]$ su
[root]# source activate python2.7
[root]# conda install -c bioconda macs2
```
---

*2019-04-28* - *2019-05-02* Install Bioconductor package **dmrseq** with R

```bash
[root]# R
```
```R
> BiocManager::install("dmrseq")
> Warning messages:
1: In install.packages(pkgs = doing, lib = lib, repos = repos, ...) :
  installation of package ‘doRNG’ had non-zero exit status
2: In install.packages(pkgs = doing, lib = lib, repos = repos, ...) :
  installation of package ‘bumphunter’ had non-zero exit status
3: In install.packages(pkgs = doing, lib = lib, repos = repos, ...) :
  installation of package ‘dmrseq’ had non-zero exit status
```

The `dmrseq` dependency `bumphunter` wouldn't install because its dependency `doRNG` wouldn't install because its dependency `rngtools` wasn't installed, which wouldn't install because its (A) not in CRAN and (B) the latest version needs R 3.6, and (C) doesn't appear to be stable or have documentation. Installed previous version of `rngtools`, 1.2.4, from source (downloaded from <https://cran.r-project.org/src/contrib/Archive/rngtools/>). Then I installed one version back from source of `doRNG`, 1.6.6 (downloaded from <https://cran.r-project.org/src/contrib/Archive/doRNG/>), so it would be compatible with the older version of rngtools. Then `dmrseq` installed and was able to install `bumphunter` with itself. All source archives were downloaded from CRAN repositories to my local computer and uploaded to the server using Macfusion.

```R
> # 2019-05-02
> install.packages('/usr/local/programs/R_package_sources/rngtools_1.2.4.tar.gz', repos = NULL)
> install.packages('/usr/local/programs/R_package_sources/doRNG_1.6.6.tar.gz', repos = NULL)
> BiocManager::install("dmrseq")
```
---

*2019-04-12* Installed QIIME and QIIME2 using conda and according to the instructions on the QIIME website. Each version was installed into its own anaconda environment as suggested in the QIIME documentation <https://docs.qiime2.org/2018.11/install/native/>. **2019-05-02 NOTE:** After I broke Anaconda, had to reinstall Qiime. Ended up updating to a later version because the earlier version downloaded was broken. See further up the file at this date for latest Qiime installation commands.

```bash
[kkeith]$ su

# install qiime1
[root]# conda create -n qiime1 python=2.7 qiime matplotlib=1.4.3 mock nose -c bioconda

# test the qiime1 environment
[root]# conda activate qiime1
(qiime1)[root]# deactivate qiime1

# install qiime2
[root]# wget https://data.qiime2.org/distro/core/qiime2-2018.11-py35-linux-conda.yml
[root]# conda env create -n qiime2 --file qiime2-2018.11-py35-linux-conda.yml

# test the qiime2 environment
[root]# conda activate qiime2
[root]# qiime --help
[root]# conda deactivate
```
---

*2019-04-12* Added aliases for all users so it's not necessary to call the entire path for **methclone** and **gdc-client**

```bash
[kkeith]$ su
[root]# nano /etc/profile.d/aliases.sh
alias methclone='/usr/local/programs/methclone-master/bin/methclone'
alias gdc-client='/usr/local/programs/tcga_gdc-client/gdc-client'
```

---

*2019-04-12* Install **methclone** according the instructions on the github repository <https://github.com/ShengLi/methclone>. Download the GitHub repository as a zip file and copied it onto the server to `/usr/local/programs/` using Macfusion as root.

```bash
[kkeith]$ su
[root]# cd /usr/local/programs/
[root]# unzip methclone-master.zip
[root]# cd methclone-master/src/utils/BamTools/
[root]# mkdir -p lib 
[root]# make
[root]# cd /usr/local/programs/methclone-master/src/utils/gzstream/
[root]# make
[root]# cd /usr/local/programs/methclone-master/src/
[root]# mkdir -p ../bin
[root]# makeme
```
The path to use methclone is `/usr/local/programs/methclone-master/bin/methclone`

*2019-04-05* Install the TCGA **gdc-client** by downloading and unzipping the binary distribution from the TCGA GDC website <https://gdc.cancer.gov/access-data/gdc-data-transfer-tool>. Downloaded the Ubuntu binary distribution `gdc-client_v1.4.0_Ubuntu_x64.zip` and copied it onto the server to `/usr/local/programs` using Macfusion as root.

```bash
[kkeith]$ su
[root]# cd /usr/local/programs/
[root]# unzip gdc-client_v1.4.0_Ubuntu_x64.zip
[root]# mkdir tcga_gdc-client
[root]# mv gdc* tcga_gdc-client/
```
The path to use methclone is `/usr/local/programs/tcga_gdc-client/gdc-client`

---

*2019-03-28* Install R package **gplots** with R

```bash
[root]# R
> install.packages("gplots")
> q()
```
---

*2019-03-28* Install R package **pvclust** with R

```bash
[root]# R
> install.packages('pvclust')
> q()
```
---

*2019-03-26* Install **Salmon** with conda

```bash
[kkeith]$ su
[root]# conda install -c bioconda salmon
```
---

*2019-03-25* Install **perl**  and **perl-env** using yum

**NOTE:** Exporting the LD_LIBRARY_PATH which is necessary for running R, prevents yum from working correctly. Solved the problem by logging in as root, commenting out the line exporting LD_LIBRARY_PATH in `/etc/profile.d/anaconda.sh`, exiting, then re-sshing in as root.

```bash
[kkeith]$ su
[root]# yum install perl-Env
```
---

*2019-03-21* Install **bismark** using conda

```bash
[kkeith]$ su
[root]# conda install -c bioconda bismark
```
---

*2019-03-18* Install R package **scde**

```bash
[kkeith]$ su
[root]# R
```
```R
> if (!requireNamespace("BiocManager", quietly = TRUE))
+    install.packages("BiocManager")
> BiocManager::install("scde", version = "3.8")
```
I forgot there are issues with the version of `scde` in Bioconductor, but remembered after getting an error running the error model. Removed scde install and reinstalled according to instructions on the scde website <http://hms-dbmi.github.io/scde/package.html>

```R
> remove.packages('scde')
> require(devtools)
> devtools::install_version('flexmix', '2.3-13')
> devtools::install_github('hms-dbmi/scde', build_vignettes = FALSE)
```
---

*2019-03-14* Install **tmux** using conda

```bash
[root]# conda install -c conda-forge tmux
```

### Installing R Packages
*2019-03-14*

Because the anaconda bin came first in the PATH, when you started R it was defaulting to anaconda R. I fixed by editing `/etc/profile.d/anaconda.sh` and `/root/.bashrc` to add anaconda to the end of the PATH instead of the beginning.

```bash
[kkeith]$ su
[root]# nano /etc/profile.d/anaconda.sh
export PATH="/usr/local/programs/anaconda3/bin:$PATH" -> export PATH="$PATH:/usr/local/programs/anaconda3/bin"
```
-

Issues installing packages

```bash
[kkeith]$ su
[root]# R
> install.packages('tidyverse')
# error message is abbreviated
ERROR: 
In install.packages("xml2") :
  installation of package ‘xml2’ had non-zero exit status
In install.packages("openssl") :
  installation of package ‘openssl’ had non-zero exit status
In install.packages("tidyverse") :
  installation of package ‘tidyverse’ had non-zero exit status
```
R had issues finding the paths to xml2 and openssl. On the advice of these GitHub/StackExchange posts, <https://github.com/r-lib/xml2/issues/219> and <https://askubuntu.com/questions/1087411/openssl-and-pkg-config-path-problems-while-configuring-mongolite-package-from-r?rq=1> respectively, I added the PATHS to both in `/etc/profile.d/anaconda.sh`

```bash
[root]# more /etc/profile.d/anaconda.sh
# export anaconda path to all users
export PATH="$PATH:/usr/local/programs/anaconda3/bin"

# export libxml2 path for R to use
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/programs/anaconda3/lib/

# export package configuration path for R to use
export PKG_CONFIG_PATH="/usr/local/programs/anaconda3/lib/pkgconfig/"
```
-

Install packages for everyone

```bash
[kkeith]$ su
[root]# R
> install.pacakges('tidyverse')
> install.packages('conflicted')
> install.packages('viridis')
> install.packages('broom')
> install.packages('modelr')
> install.packages('devtools')
> if (!requireNamespace("BiocManager", quietly = TRUE))
+    install.packages("BiocManager")
> BiocManager::install("methylKit", version = "3.8")
> BiocManager::install("plyranges", version = "3.8")
> install.packages('Rtsne')
> install.packages('umap')
> install.packages('cowplot')
> install.packages('ggdendro')
> install.packages('pheatmap')
```

### Install Illumina BaseMount
*2019-03-14*

Installing the program.

```bash
[kkeith]$ su
[root]# bash -c "$(curl -L https://basemount.basespace.illumina.com/install)"
[root]# mkdir /mnt/basespace
[root]# chmod 777 /mnt/basespace
[root]# exit
[kkeith]$ basemount /mnt/basespace/
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount /mnt/basespace/
From:
    /home

Starting authentication.

You need to authenticate by opening this URL in a browser:
  https://basespace.illumina.com/oauth/device?code=r5xk3
.........
It worked!
Your identification has been saved.

Mounting BaseSpace account.
To unmount, run: basemount --unmount /mnt/basespace
[kkeith]$ ll /mnt/basespace
total 1
drwxr-xr-x. 2 kkeith research   0 Mar 14 09:19 Projects
-r--r--r--. 1 kkeith research 598 Mar 14 09:19 README
drwxr-xr-x. 2 kkeith research   0 Mar 14 09:19 Runs
```
Setting up a user configuration file so multiple users can use BaseMount (hopefully)

```bash
[kkeith]$ basemount --unmount /mnt/basespace
[kkeith]$ mv ~/.basespace/default.cfg ~/.basespace/kkeith.cfg
[kkeith]$ basemount --config kkeith /mnt/basespace/
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount --config kkeith /mnt/basespace/
From:
    /home

Api Server: https://api.basespace.illumina.com/

Mounting BaseSpace account.
To unmount, run: basemount --unmount /mnt/basespace
[kkeith]$ ll /mnt/basespace/
total 1
drwxr-xr-x. 2 kkeith research   0 Mar 14 09:19 Projects
-r--r--r--. 1 kkeith research 598 Mar 14 09:19 README
drwxr-xr-x. 2 kkeith research   0 Mar 14 09:19 Runs
```

### Make conda path available to all users
*2019-03-12*

```bash
su

# on Anaconda's recommendation, soft link conda.sh in /etc/profile.d
ln -s /usr/local/programs/anaconda3/etc/profile.d/conda.sh

# anaconda PATH was not exporting to users correctly, so added another bash file to /etc/profile.d to export the PATH to users at startup/login
cd /etc/profile.d
nano anaconda.sh
# export anaconda path to all users
export PATH="/usr/local/programs/anaconda3/bin:$PATH"
```
Also commented out the lines in root's .bashrc that were causing a conda environment to be launched at startup

### Set Up a Python2.7 Environment
*2019-03-12*

Set up an environment that will run python2.7 for running legacy software

```bash
conda create --name python2.7 python=2.7
```
Instructions for activating the environment from anaconda:

```bash
# To activate this environment, use
#
#     $ conda activate python2.7
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```
---

#### Install Software in the Python2.7 Environment
Install **ngsplot** for Sandra

```bash
# copied ngsplot to /user/local/programs using Macfusion
tar xzvf 

# install R dependencies for ngsplot
R
install.packages("doMC", dep=T)
install.packages("caTools", dep=T)
install.packages("utils", dep=T)
source("http://bioconductor.org/biocLite.R")
biocLite( "BSgenome" )
biocLite( "Rsamtools" )
biocLite( "ShortRead" )

# tried to set up PATH/environment, but it doesn't seem to be working correctly
nano /etc/profile.d/ngsplot.sh
# export the PATH
export NGSPLOT=/usr/local/programs/ngsplot/bin:$PATH

# set the environemtn variable
export NGSPLOT=/usr/local/programs/ngsplot
```

Install **macs2** using pip, as recommended in the macs2 installation guide. 2019-05-02 **EDIT** See sucessful installation instructions above.

```bash
pip install MACS2
```

---

Install **scipy** using conda

```bash
conda install -c anaconda scipy
```
---

Install **numpy** using conda

```bash
conda install -c anaconda numpy
```

### Install Software
*2019-03-12*

Installed software from the bix2 software installation log to get the server up and running. Everything installed as root.

---

Install **RSEM** with conda

```bash
conda install -c bioconda rsem
```

---

Install **IGV** with conda

```bash
conda install -c bioconda igv
```

---

Install **majiq** with C-lang (c compiler) and pip (as I did on bix2)

```bash
yum install zlib-devel
conda install -c conda-forge clangdev
pip install git+https://bitbucket.org/biociphers/majiq_stable.git#egg=majiq
```
---

Install **git** using conda

```bash
conda install -c anaconda git 
```
---

Installed the **SRA Toolkit** using conda

```bash
conda install -c bioconda sra-tools
```

---

Installed **deeptools** using conda

```bash
conda install -c bioconda deeptools
```

---

#### Install linear algebra libraries for UNIX to speed up computations

Installed **ATLAS** using yum

```bash
yum install atlas
```
---

Installed **BLAS** and **LAPACK** using yum

```bash
yum install lapack
```

---

Installed **subread** using conda

```bash
conda install -c bioconda subread
```

---

Installed **UMI-tools** using conda

```bash
conda install -c bioconda -c conda-forge umi_tools
```

---

Installed **numpy** using conda

```bash
conda install -c anaconda numpy
```
---

Installed **scipy** using conda

```bash
conda install -c anaconda scipy
```

---

Installed **matplotlib** using conda

```bash
conda install matplotlib
```

---

Installed **pyyaml** using conda

```bash
conda install -c anaconda pyyaml
```

---

Installed **pysam** using conda

```bash
conda install -c bioconda pysam
```

---

Installed **pyfasta** using conda

```bash
conda install -c bioconda pyfasta
```

---

Installed **STAR** using conda

```bash
conda install -c bioconda star
```

---

Installed **fastqc** using conda

```bash
conda install -c bioconda fastqc
```

---

Installed **trim_galore** using conda

```bash
conda install -c bioconda trim-galore
```

---

Installed **bowtie2** using conda

```bash
conda install -c bioconda bowtie2
```

---

Installed **trimmomatic** using conda

```bash
conda install -c bioconda trimmomatic
```

---

Installed **vcftools** using conda

```bash
conda install -c bioconda vcftools
```

---

Installed **samtools** using conda

```bash
conda install -c bioconda samtools
```
Issue running samtools

```bash
samtools: error while loading shared libraries: libcrypto.so.1.0.0: cannot open shared object file: No such file or directory
```
Softlinked libcrypto.so.1.0.0 to libcrypto.so.1.1 as suggested in this github thread: <https://github.com/bioconda/bioconda-recipes/issues/12100> and that fixed the issue

```bash
su
cd /usr/local/programs/anaconda3/lib
ln -s libcrypto.so.1.1 libcrypto.so.1.0.0
```

---

Installed **bedtools** using conda

```bash
conda install -c bioconda bedtools

cd /usr/local/programs/anaconda/lib
```

### Install Anaconda
*2019-03-12*

```bash
su
cd /usr/local/programs
bash Anaconda3-2018.12-Linux-x86_64.sh

In order to continue the installation process, please review the license
agreement.
Please, press ENTER to continue
>>> 
Do you accept the license terms? [yes|no]
>>> yes
Anaconda3 will now be installed into this location:
/root/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/root/anaconda3] >>> /usr/local/programs/anaconda
Do you wish the installer to initialize Anaconda3
in your /root/.bashrc ? [yes|no]
>>> yes

Initializing Anaconda3 in /root/.bashrc
A backup will be made to: /root/.bashrc-anaconda3.bak


For this change to become active, you have to open a new terminal.

Thank you for installing Anaconda3!

===========================================================================

Anaconda is partnered with Microsoft! Microsoft VSCode is a streamlined
code editor with support for development operations like debugging, task
running and version control.

To install Visual Studio Code, you will need:
  - Administrator Privileges
  - Internet connectivity

Visual Studio Code License: https://code.visualstudio.com/license

Do you wish to proceed with the installation of Microsoft VSCode? [yes|no]
>>> no
```

### Install R and RStudio Server
*2019-03-12*

See `install_r_studio.mdll`

