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
```
**Note to Self:** Next time, add a print statement in the loop, so you can tell what the problem is if progress stalls.





