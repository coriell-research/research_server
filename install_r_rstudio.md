## Installing R/RStudio

```bash
cd /usr/local/programs
su

# instal the Extra Packages for Enterprise Linux (EPEL)
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

# install R from source
yum-builddep R
yum install R

# install RStudio server
wget https://download2.rstudio.org/rstudio-server-rhel-1.1.463-x86_64.rpm
yum install rstudio-server-rhel-1.1.463-x86_64.rpm
```