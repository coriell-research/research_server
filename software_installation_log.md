# Software Installation Log

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

