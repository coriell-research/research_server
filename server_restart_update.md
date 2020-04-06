## Monthly Server Restart and Update

### Restart the Server

```bash
sudo reboot
```

#### Remount the Data Drive after Restart

```bash
sudo mount /dev/md0 /mnt/data
```

### Update the Server

Update `yum` and `conda`

```bash
### update yum
sudo yum update
### update conda
sudo conda update conda
```