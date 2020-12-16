## Monthly Server Restart and Update

### Restart the Server

```bash
sudo reboot
```

#### Remount the Data Drive after Restart

```bash
# for cbix/10.1.105.11 only
sudo mount /dev/md0 /mnt/data
```

### Update the Server

Update `yum` and `conda` and R packages

```bash
su
### update yum
yum update
### update conda
conda update conda
conda update --all
### update R packages
R
update.packages() # may want to include ask = F, so you don't have to approve every package update
```