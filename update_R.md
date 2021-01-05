## Update R

### Update R

So you can just copy/paste the following commands, first set the environment variable `R_VERSION`

```bash
export R_VERSION=4.0.3
```

Download the latest version of R through RStudio

```bash
curl -O https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm
```
Install with `yum`

```bash
sudo yum install R-${R_VERSION}-1-1.x86_64.rpm
```
Verify R installation by checking the version

```bash
/opt/R/${R_VERSION}/bin/R --version
```
#### Make Sure Soft Links Are Corrent

You need to soft-link R to `/usr/local/bin` so the system can find it; both of the links below should be to the latest R version in `/opt/R/${R_VERSION}/`

```bash
### example
ll /usr/local/bin/R
ll /usr/local/bin/Rscript
```

If they're not the most current version, relink the softlinks

```bash
sudo unlink /usr/local/bin/R
sudo unlink /usr/local/bin/Rscript
sudo ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R
sudo ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript
```

### Restart RStudio Server

RStudio Server needs to be re-launched so it changes to the latest version of R. (For reference <https://support.rstudio.com/hc/en-us/articles/200532327-Managing-the-Server>.) Make sure to suspend active sessions first. Also you may have to delete your `~/.rstudio` folder.

```bash
### suspend sessions
sudo rstudio-server suspend-all
# or if you have to force suspend
sudo rstudio-server force-suspend-all

### restart
sudo rstudio-server restart
```

### Re-Install All Packages

See `r_packages.csv` for a list of all packages to re-install.