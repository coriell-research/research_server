# Software Installation Log

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

Install **macs2** using pip, as recommended in the macs2 installation guide

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

