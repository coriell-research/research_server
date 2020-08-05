## 10.1.105.13 Software Installation Log

### Install R Packages

*2020-07-19* Having issues because bioconductor packages won't install without package `XML` and `XML` won't install 

```bash
cd /usr/local/programs
sudo yum localinstall libxml2-devel-2.9.1-6.el7.4.i686.rpm 
wget http://mirror.centos.org/centos/7/os/x86_64/Packages/libxml2-devel-2.9.1-6.el7.4.i686.rpm
```

```bash
### softlink shit
cd /usr/local/programs/anaconda3/lib
ln -s libcrypto.so.1.1 libcrypto.so.1.0.0
ln -s libssl.so.1.1 libssl.so.1.0.0
# maybe need to do but it looks fine ln -s ibstdc++.so.6.0.25 libstdc++.so
```

Setup up a configuration file `anaconda.sh` in `/etc/profile.d/` as on the other server

```bash
[root]# nano /etc/profile.d/anaconda.sh
[root]# more /etc/profile.d/anaconda.sh
# export anaconda path to all users
export PATH="$PATH:/usr/local/programs/anaconda3/bin"

# export libxml2 path for R to use
#export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/programs/anaconda3/lib/

# export package configuration path for R to use
export PKG_CONFIG_PATH="/usr/local/programs/anaconda3/lib/pkgconfig/"
```

```bash
[root]# nano ~/.bash_profile
[root]# source ~/.bash_profile 
[root]# R
> install.packages('tidyverse')
> install.packages('viridis')
> install.packages('broom')
> install.packages('devtools')
> install.packages('BiocManager')
> install.packages('pheatmap')
> install.packages('vroom')
> ### Bioconductor packages
> BiocManager::install("plyranges")
> BiocManager::install("DESeq2")

```

### Install Basic Bioinformatics Software with `conda`
*2020-07-19*

```bash
[root]# conda install -c bioconda bedtools
[root]# conda install -c bioconda samtools
[root]# conda install -c bioconda trimmomatic
[root]# conda install -c bioconda trim-galore
[root]# conda install -c bioconda bowtie2
[root]# conda install -c bioconda STAR
[root]# conda install -c bioconda bismark
[root]# conda install -c bioconda fastqc
[root]# conda install -c bioconda subread
[root]# conda install -c anaconda git
[root]# conda install -c bioconda deeptools
[root]# conda install -c bioconda sra-tools
[root]# conda install -c conda-forge tmux
[root]# conda install -c bioconda macs2
[root]# conda install -c anaconda libxml2
```

### Set Up a Python2.7 Environment to Run Legacy Software
*2020-07-19*

Set up an environment that will run python2.7 for running legacy software

```bash
conda create --name python2.7 python=2.7
```

### Install linear algebra libraries for UNIX to speed up computations
*2020-07-19*

```bash
[root]# yum install lapack
[root]# yum install atlas
```

### Set up root's `.bash_profile` so `yum`, `conda`, and `R` can play at nicely together
*2020-07-19*

```bash
### this is copied directly from the first server's (10.1.105.11) root's .bash_profile, but with more and cleaner comments
[root]# more ~/.bash_profiles
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs

PATH=$PATH:$HOME/bin
# sometimes you	need to	give root the anaconda path, so	if necessary, uncomment, save, then source ~/.bash_profile
#PATH="/usr/local/programs/anaconda3/bin:$PATH"

export PATH

### playing nicely with R
# The LD_LIBRARY_PATH R	needs is through Anaconda, but using this path messes up yum installation (yum uses the	path below)
# So when you need to install an R package, uncomment this LD_LIBRARY_PATH, comment the	one below, then	source ~/.bash_profile
#export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/programs/anaconda3/lib/

# set the ROOT environment variables and paths
export ROOTSYS=/usr/local/programs/root
export PATH=$PATH:$ROOTSYS/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ROOTSYS/lib
```

### Install Conda
*2020-07-19*

```bash
### Download Anaconda installation file to local machine from https://www.anaconda.com/products/individual#linux
[kelsey:Downloads]$ sftp root@10.1.105.13
sftp> put Anaconda3-2020.02-Linux-x86_64.sh
sftp> exit

[root]# 

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

[/root/anaconda3] >>> /usr/local/programs/anaconda3
Preparing transaction: done
Executing transaction: done
installation finished.
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
[no] >>> yes
==> For changes to take effect, close and re-open your current shell. <==

If you'd prefer that conda's base environment not be activated on startup, 
   set the auto_activate_base parameter to false: 

conda config --set auto_activate_base false

Thank you for installing Anaconda3!

===========================================================================

Anaconda and JetBrains are working together to bring you Anaconda-powered
environments tightly integrated in the PyCharm IDE.

PyCharm for Anaconda is available at:
https://www.anaconda.com/pycharm
[root]$ exit
[kelsey]$ ssh -Y root@10.1.105.13
root@10.1.105.13's password:
(base)[root]# conda config --set auto_activate_base false
(base)[root]# exit
[kelsey]$ ssh -Y root@10.1.105.13
root@10.1.105.13's password:
[root]#
```

### Install R/RStudio Server

```bash
### check CentOS version
[root]# cat /etc/centos-release
[root]# CentOS Linux release 7.8.2003 (Core)

### Install R
### https://cloud.r-project.org/
### https://fedoraproject.org/wiki/EPEL
[root]# cd /usr/local/programs
[root]# yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
[root]# yum-builddep R
[root]# yum install R
[root]# R
R version 3.6.0 (2019-04-26) -- "Planting of a Tree"
Copyright (C) 2019 The R Foundation for Statistical Computing
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
> q()
Save workspace image? [y/n/c]: n


### Install RStudio Server
### Following RStudio's instructions from https://rstudio.com/products/rstudio/download-server/redhat-centos/
[root]# wget https://download2.rstudio.org/server/centos6/x86_64/rstudio-server-rhel-1.3.1056-x86_64.rpm
[root]# yum install rstudio-server-rhel-1.3.1056-x86_64.rpm
```

### Make the Folder to Install Software To
*2020-07-19*

```bash
[root]# mkdir /usr/local/programs
```

---

## Adventures in installing R 4.0.2

2020-08-04 GC

### Download newest version from CRAN and extract

```shell
curl -O https://cran.r-project.org/src/base/R-4/R-4.0.2.tar.gz
tar -xvzf R-4.0.2.tar.gz
cd R-4.0.2/
```

### Configure the installation

Since blas and lapack have already been installed set the flags in the config step.

```shell
# enable shared libs, blas and libpack
sudo ./configure --prefix=/opt/R/R-4.0.2 \
		 --enable-memory-profiling \
		 --enable-R-shlib \
		 --with-blas \
		 --with-lapack
# build
sudo make
sudo make install
```

## Test build 

```shell
make check  # --> all ..OK
/opt/R/R-4.0.2/bin/R --version  # 4.0.2
```

### Fix `yum`

`yum --help` returned an error due to the `export LD_LIBRARY_PATH` line in root's ~/.bash_profile. **Commented out the exports in /home/root/.bash_profile** and re-sourced. `yum` works as expected now. These lines could be deleted now but I'll leave them in in case I need to backtrack.

### Remove R 3.6.0

`sudo yum remove R -y`

Softlink new R version to old bin location.

`sudo ln -s /opt/R/R-4.0.2/bin/R /usr/local/bin/R`
`sudo ln -s /opt/R/R-4.0.2/bin/Rscript /usr/local/bin/Rscript`

Test the new version

`which R` --> "/usr/local/bin/R"

`R --version` --> "R version 4.0.2 (2020-06-22) -- "Taking Off Again"`

### Fix `sudo R --version`

`sudo R --version` was looking for the old R version in `/bin/R`. Remove the old binary and link to the new installation:

`sudo rm /bin/R /bin/Rscript`

`sudo ln -s /opt/R/R-4.0.2/bin/R /bin/R`

`sudo ln -s /opt/R/R-4.0.2/bin/Rscript /bin/Rscript` 

### Install open-ssl for R packages

Needed before `install.packages()` is run.

`sudo yum install openssl-devel -y`

### Install devtoolset-7 for R

`tidyverse` installation was throwing errors because of the cpp compiler used by centOS (an old version of gcc, 4.8.x). Install the newest `gcc` version, tell R where to look, and try again.

```shell
sudo yum install centos-release-scl
sudo yum install devtoolset-7
scl enable devtoolset-7 bash # to test gcc version
```

Now, edit the Makeconf file that R uses to pick compilers. Change the following lines in /opt/R/R-4.0.2/etc/Makeconf:

the link below was helpful:

[link](https://github.com/vspinu/mlvocab/blob/master/travis/before_install.sh#L8-L13)

```shell
CC = /opt/rh/devtoolset-7/root/bin/gcc -std=gnu99
CXX = /opt/rh/devtoolset-7/root/bin/g++ -std=gnu++11
CXX11 = /opt/rh/devtoolset-7/root/bin/g++ -std=c++11
```

I think this eliminates the need to mess with the LD_LIBRARY path as well.

### Install R packages

```shell
# following `sudo R`
install.packages('tidyverse')
install.packages('devtools')
install.packages('DBI')
install.packages('odbc')  # required sudo yum install unixODBC-devel first
install.packages('viridis')
install.packages('pheatmap')
install.packages('vroom')
install.packages('patchwork')
install.packages('lubridate')
install.packages('data.table')

# bio
install.packages('BiocManager')
BiocManager::install("plyranges")
BiocManager::install("DESeq2")
BiocManager::install("edgeR")
```

### Remove old .libPaths() directory

`sudo rm -r /usr/local/lib64/R`

### Create Renviron.site file for startup to find right location of libraries for all users

`sudo touch /opt/R/R-4.0.2/etc/Renviron.site`

Add the following lines to the Renviron.site file

```shell
R_LIBS=/opt/R/R-4.0.2/library
R_LIBS_USER=/opt/R/R-4.0.2/library
```

### Allow access to Rstudio server

Opened port through firewall

`sudo firewall-cmd --permanent --zone=public --add-port=8787/tcp`

Reload firewall to apply settings

`sudo firewall-cmd --reload`

Point web browser at http://cbix2_server_ip:8787/ to check --> SUCCESS
