## Updating Anaconda to the March 2019 Release

### Why Re-install conda?

We were getting errors (examples below) when attempting to use conda and also when using some programs installed using conda, so re-downloaded the execution file and re-installed.

-

Example errors

```bash
# example
OSError: /lib64/libstdc++.so.6: version `CXXABI_1.3.8' not found (required by /usr/local/programs/anaconda3/lib/././libicuuc.so.58)
```
Example 1 could be resolved by softlinking some libraries that (apparently) conda's attempts to update kept breaking

```bash
[root]# ln -s /usr/local/programs/anaconda3/lib/libstdc++.so.6.0.25 /usr/local/programs/anaconda3/lib/libstdc++.so
[root]# ln -s /usr/local/programs/anaconda3/lib/libstdc++.so.6.0.25 /usr/local/programs/anaconda3/lib/libstdc++.so.6
```
-

Attempts to update or fix conda were not successful.

```bash
# warning at the start of update attempt
[root]# conda update conda
WARNING conda.base.context:use_only_tar_bz2(632): Conda is constrained to only using the old .tar.bz2 file format because you have conda-build installed, and it is <3.18.3.  Update or remove conda-build to get smaller downloads and faster extractions.

#######

# error at the end of update attempt
ERROR conda.core.link:_execute(637): An error occurred while installing package 'None'.
AssertionError()
Attempting to roll back.

Rolling back transaction: done

AssertionError()
()
AssertionError()
```
-

Save list of installed programs for reference.

```bash
# from /usr/local/programs
[root]# conda list > 2019-07-15_installed_programs.txt
```
-

### Re-install Anaconda

#### Re-install the main program

The python3.7 distribution of Anaconda was download from <https://www.anaconda.com/distribution/> and uploaded to the server as root at `/usr/local/programs` using Macfusion

```bash
# from /usr/local/programs
[root]# bash Anaconda3-2019.03-Linux-x86_64.sh
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
installation finished.
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
[no] >>> yes
WARNING: The conda.compat module is deprecated and will be removed in a future release.
no change     /usr/local/programs/anaconda3/condabin/conda
no change     /usr/local/programs/anaconda3/bin/conda
no change     /usr/local/programs/anaconda3/bin/conda-env
no change     /usr/local/programs/anaconda3/bin/activate
no change     /usr/local/programs/anaconda3/bin/deactivate
no change     /usr/local/programs/anaconda3/etc/profile.d/conda.sh
no change     /usr/local/programs/anaconda3/etc/fish/conf.d/conda.fish
no change     /usr/local/programs/anaconda3/shell/condabin/Conda.psm1
no change     /usr/local/programs/anaconda3/shell/condabin/conda-hook.ps1
no change     /usr/local/programs/anaconda3/lib/python3.7/site-packages/xonsh/conda.xsh
no change     /usr/local/programs/anaconda3/etc/profile.d/conda.csh
modified      /root/.bashrc

==> For changes to take effect, close and re-open your current shell. <==

If you'd prefer that conda's base environment not be activated on startup, 
   set the auto_activate_base parameter to false: 

conda config --set auto_activate_base false

Thank you for installing Anaconda3!
```
Turned off activating the conda environment by default

```bash
[root]# conda config --set auto_activate_base false
```
#### Re-install programs installed with conda

```bash
# reinstall tmux first so I can run stuff without worrying about crashing
[root]# conda install -c conda-forge tmux

# the stupid file I save from conda list earlier is not tab-delimited, but has a variable number of spaces, so need to fix that first
[root]# cat 2019-07-15_installed_programs.txt | sed -n 's/ \+/\t/gp' > 2019-07-15_installed_programs.tsv

# reinstall programs in a loop
for i in $(cut -f1 2019-07-15_installed_programs.tsv); do conda install $i --yes; done
# The bioconda packages couldn't be found? So did loop again with the bioconda channel
for i in $(cut -f1 2019-07-15_installed_programs.tsv); do conda install -c bioconda $i --yes; done

# update everything to latest version
[root]# conda update conda
```
**Note to Self:** Next time, add a print statement in the loop, so you can tell what the problem is if progress stalls.

#### Re-install programs installed in special conda environments
*2019-07-17*

```bash
[root]# conda create --name python2.7 python=2.7
[root]# conda activate python2.7
(python2.7)[root]# conda install -c bioconda macs2
(python2.7)[root]# macs2
usage: macs2 [-h] [--version]
             {callpeak,bdgpeakcall,bdgbroadcall,bdgcmp,bdgopt,cmbreps,bdgdiff,filterdup,predictd,pileup,randsample,refinepeak}
             ...
macs2: error: too few arguments
(python2.7)[root]# conda deactivate
[root]# cd /usr/local/programs/
[root]# wget https://data.qiime2.org/distro/core/qiime2-2019.4-py36-linux-conda.yml
[root]# conda env create -n qiime2 --file qiime2-2019.4-py36-linux-conda.yml
[root]# conda activate qiime2
(qiime2)[root]# qiime --version
q2cli version 2019.4.0
Run `qiime info` for more version details
[root]# conda deactivate
```
### Error Resolution
*2019-07-22*

Got the following error when trying to run `bedGraphtoBigWig`:

```bash
bedGraphToBigWig: error while loading shared libraries: libssl.so.1.0.0: cannot open shared object file: No such file or directory
```
Based on Googling (and my memory of this happening before), mainly this StackExchange post <https://askubuntu.com/questions/339364/libssl-so-10-cannot-open-shared-object-file-no-such-file-or-directory>, made a softlink with the name from the error in the anaconda3 library.

```bash
[kkeith]$ ll /usr/local/programs/anaconda3/lib/libssl*
-rw-rw-r--. 2 root root 1237640 Mar  7 10:42 /usr/local/programs/anaconda3/lib/libssl.a
lrwxrwxrwx. 1 root root      13 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libssl.so -> libssl.so.1.1
-rwxrwxr-x. 2 root root  695960 Mar  7 10:42 /usr/local/programs/anaconda3/lib/libssl.so.1.1
[kkeith]$ sudo ln -s /usr/local/programs/anaconda3/lib/libssl.so /usr/local/programs/anaconda3/lib/libssl.so.1.0.0
[kkeith]$ ll /usr/local/programs/anaconda3/lib/libssl*
-rw-rw-r--. 2 root root 1237640 Mar  7 10:42 /usr/local/programs/anaconda3/lib/libssl.a
lrwxrwxrwx. 1 root root      13 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libssl.so -> libssl.so.1.1
lrwxrwxrwx. 1 root root      43 Jul 22 11:00 /usr/local/programs/anaconda3/lib/libssl.so.1.0.0 -> /usr/local/programs/anaconda3/lib/libssl.so
-rwxrwxr-x. 2 root root  695960 Mar  7 10:42 /usr/local/programs/anaconda3/lib/libssl.so.1.1
```
-
After resolving the error above, got a very similar error.

```bash
bedGraphToBigWig: error while loading shared libraries: libcrypto.so.1.0.0: cannot open shared object file: No such file or directory
```
Resolved it by softlink as well

```bash
[kkeith]$ ll /usr/local/programs/anaconda3/lib/libcrypto*
-rw-rw-r--. 1 root root 6708332 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libcrypto.a
lrwxrwxrwx. 1 root root      16 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libcrypto.so -> libcrypto.so.1.1
-rwxrwxr-x. 1 root root 3452736 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libcrypto.so.1.1
[kkeith]$ sudo ln -s /usr/local/programs/anaconda3/lib/libcrypto.so.1.1 /usr/local/programs/anaconda3/lib/libcrypto.so.1.0.0
[kkeith]$ ll /usr/local/programs/anaconda3/lib/libcrypto*
-rw-rw-r--. 1 root root 6708332 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libcrypto.a
lrwxrwxrwx. 1 root root      16 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libcrypto.so -> libcrypto.so.1.1
lrwxrwxrwx. 1 root root      50 Jul 22 11:03 /usr/local/programs/anaconda3/lib/libcrypto.so.1.0.0 -> /usr/local/programs/anaconda3/lib/libcrypto.so.1.1
-rwxrwxr-x. 1 root root 3452736 Jul 15 12:48 /usr/local/programs/anaconda3/lib/libcrypto.so.1.1
```
#### deepTools didn't reinstall

Re-installed deepTools using conda

```bash
[kkeith]$ su
[root]# tmux new -s deeptools
[root]# conda install -c bioconda deeptools
```
That didn't work because there's some sort of dependency conflict, so re-installed deeptools in its own conda environment.

```bash
[kkeith]$ su
[root]# conda create --name deeptools
[root]# conda activate deeptools
(deeptools)[root]# conda install -c bioconda deeptools
```
