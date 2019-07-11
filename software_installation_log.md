# Software Installation Log

### Weird Java Error
*2019-07-11*

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

*2019-06-25* Install **Gencove API** to download data using pip.

```bash
[kkeith]$ su
[root]# pip install gencove
```

*2019-06-22* Install **libiconv** using conda, which MEME needs to run

```bash
[kkeith]$ conda install -c conda-forge libiconv
[root]# conda install -c conda-forge libiconv
```
-

*2019-06-21* Install **epic2** using conda

```bash
[kkeith]$ su
[root]# conda install -c bioconda epic2 
```

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
-

Install **bedops** using conda for cut&run pipeline

```bash
[root]# conda install -c bioconda bedops
```
-

Install **MEME** using conda for cut&run pipeline

```bash
[root]# conda install -c bioconda meme
```
-

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

*2019-05-02* Re-installed **qiime2** using conda and the qiime2 documentation's suggest commands after I broke Anaconda

```bash
[root]# cd /usr/local/programs
[root]# wget https://data.qiime2.org/distro/core/qiime2-2019.1-py36-linux-conda.yml
[root]# conda env create -n qiime2-2019.1 --file qiime2-2019.1-py36-linux-conda.yml
[root]# rm qiime*
```

*2019-05-02* Install UCSC's **bedSort** to sort my bed files

```bash
[root]# conda install -c bioconda ucsc-bedsort
```

*2019-05-02* Install UCSC's **fetchChromSizes** with conda. Need it to get the chromosome sizes for bedGraphtoBigWig

```bash
[root]# conda install -c bioconda ucsc-fetchchromsizes
```
-

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
-

*2019-05-02* Install **macs2** with conda, because previous attempt with pip failed. After killing conda a reinstalling all packages, installed it again in the python2.7 conda environment

```bash
[kkeith]$ su
[root]# source activate python2.7
[root]# conda install -c bioconda macs2
```
-

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
-

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
-

*2019-04-12* Added aliases for all users so it's not necessary to call the entire path for **methclone** and **gdc-client**

```bash
[kkeith]$ su
[root]# nano /etc/profile.d/aliases.sh
alias methclone='/usr/local/programs/methclone-master/bin/methclone'
alias gdc-client='/usr/local/programs/tcga_gdc-client/gdc-client'
```

-

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

*2019-03-28* Install R package **gplots** with R

```bash
[root]# R
> install.packages("gplots")
> q()
```

*2019-03-28* Install R package **pvclust** with R

```bash
[root]# R
> install.packages('pvclust')
> q()
```

*2019-03-26* Install **Salmon** with conda

```bash
[kkeith]$ su
[root]# conda install -c bioconda salmon
```

*2019-03-25* Install **perl**  and **perl-env** using yum

**NOTE:** Exporting the LD_LIBRARY_PATH which is necessary for running R, prevents yum from working correctly. Solved the problem by logging in as root, commenting out the line exporting LD_LIBRARY_PATH in `/etc/profile.d/anaconda.sh`, exiting, then re-sshing in as root.

```bash
[kkeith]$ su
[root]# yum install perl-Env
```

*2019-03-21* Install **bismark** using conda

```bash
[kkeith]$ su
[root]# conda install -c bioconda bismark
```

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

-

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

-

Install **scipy** using conda

```bash
conda install -c anaconda scipy
```

-

Install **numpy** using conda

```bash
conda install -c anaconda numpy
```

### Install Software
*2019-03-12*

Installed software from the bix2 software installation log to get the server up and running. Everything installed as root.

-

Install **RSEM** with conda

```bash
conda install -c bioconda rsem
```

-

Install **IGV** with conda

```bash
conda install -c bioconda igv
```

-

Install **majiq** with C-lang (c compiler) and pip (as I did on bix2)

```bash
yum install zlib-devel
conda install -c conda-forge clangdev
pip install git+https://bitbucket.org/biociphers/majiq_stable.git#egg=majiq
```
-

Install **git** using conda

```bash
conda install -c anaconda git 
```
-

Installed the **SRA Toolkit** using conda

```bash
conda install -c bioconda sra-tools
```

-

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
-

Installed **BLAS** and **LAPACK** using yum

```bash
yum install lapack
```

---

Installed **subread** using conda

```bash
conda install -c bioconda subread
```

-

Installed **UMI-tools** using conda

```bash
conda install -c bioconda -c conda-forge umi_tools
```

-

Installed **numpy** using conda

```bash
conda install -c anaconda numpy
```
- 

Installed **scipy** using conda

```bash
conda install -c anaconda scipy
```

-

Installed **matplotlib** using conda

```bash
conda install matplotlib
```

-

Installed **pyyaml** using conda

```bash
conda install -c anaconda pyyaml
```

-

Installed **pysam** using conda

```bash
conda install -c bioconda pysam
```

-

Installed **pyfasta** using conda

```bash
conda install -c bioconda pyfasta
```

-

Installed **STAR** using conda

```bash
conda install -c bioconda star
```

-

Installed **fastqc** using conda

```bash
conda install -c bioconda fastqc
```

-

Installed **trim_galore** using conda

```bash
conda install -c bioconda trim-galore
```

-

Installed **bowtie2** using conda

```bash
conda install -c bioconda bowtie2
```

-

Installed **trimmomatic** using conda

```bash
conda install -c bioconda trimmomatic
```

-

Installed **vcftools** using conda

```bash
conda install -c bioconda vcftools
```

-

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

-

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

