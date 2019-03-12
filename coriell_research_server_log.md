# Coriell Research Server
IP address: 10.1.105.11

### Mounting the data disks
*2019-03-12*

Restarted the server to finish software installation, and the disk field does not automatically mount at start up. Mounted as root.

```bash
su
mount /dev/md0 /mnt/data/
df -h
Filesystem               Size  Used Avail Use% Mounted on
/dev/mapper/centos-root  500G   15G  485G   3% /
devtmpfs                 252G     0  252G   0% /dev
tmpfs                    252G     0  252G   0% /dev/shm
tmpfs                    252G   11M  252G   1% /run
tmpfs                    252G     0  252G   0% /sys/fs/cgroup
/dev/sda1               1014M  219M  796M  22% /boot
/dev/mapper/centos-home  1.3T   33M  1.3T   1% /home
tmpfs                     51G     0   51G   0% /run/user/1002
tmpfs                     51G     0   51G   0% /run/user/1001
/dev/md0                 189T   56K  179T   1% /mnt/data
```

### Software Installation
*2019-03-12*

For software installation documentation see `software_installation_log.md`

### Set up user accounts
*2019.03.11*

```bash
### add users and put them in the research group (Jozef added himself; not documented here)
[]# adduser kkeith
[]# passwd kkeith
[]# groupadd admin
[]# usermod -g research kkeith
[]# usermod -g research jmadzo
[]# useradd -g research jjelinek
[]# passwd jjelinek

### change permissions to 775 so group members can read, write, and execute each others files
[]# chmod -R 775 jmadzo
[]# chmod -R 775 kkeith
[]# chmod -R 775 jjelinek

### set up data directories on the data disks; basically everything will be stored here
[]# cd /mnt/data
[]# mkdir data_kk
[]# mkdir data_jm
[]# mkdir data_jj
[]# chown -R jmadzo:research data_jm
[]# chown -R kkeith:research data_kk
[]# chown -R jjelinek:research data_jj
[]# chmod -R 775 data_jj
[]# chmod -R 775 data_jm
[]# chmod -R 775 data_kk

### soft link data folders for everyone from their home directories to their data directories
# jjelinek
[]# cd /home/jjelinek
[]# ln -s /mnt/data/data_jj/ data
[]# chown -R jjelinek:research data
[]# chown -R jjelinek:research /mnt/data/data_jj/ncbi/
[]# chmod -R 775 /mnt/data/data_jj/ncbi/
[]# ln -s /mnt/data/data_jj/ncbi/ ncbi
[]# chown -R jjelinek:research ncbi
# jmadzo
cd ../jmadzo/
ln -s /mnt/data/data_jm/ data
mkdir /mnt/data/data_jm/ncbi
ln -s /mnt/data/data_jm/ncbi/ ncbi
chown -R jmadzo:research *
# kkeith
cd ../kkeith/
ln -s /mnt/data/data_kk/ data
mkdir /mnt/data/data_kk/ncbi
ln -s /mnt/data/data_kk/ncbi/ ncbi

### make sure all file ownership/permissions are correct
# jjelinek
cd /home/jjelinek/
chown -R jjelinek:research *
chmod -R 775 *
cd /mnt/data/data_jj
chown -R jjelinek:research *
chmod -R 775 *
# jmadzo
cd /home/jmadzo
chown -R jmadzo:research *
chmod -R 775 *
cd /mnt/data/data_jm/
chown -R jmadzo:research *
chmod -R 775 *
# kkeith
cd /home/kkeith
chown -R kkeith:research *
chmod -R 775 *
cd /mnt/data/data_kk/
chown -R kkeith:research *
chmod -R 775 *

### edit /etc/sudoers so we have all sudo permissions
nano /etc/sudoers
# added lines for our user accounts under root
## Allow root to run any commands anywhere
root    ALL=(ALL)	ALL
jjelinek ALL=(ALL)	ALL
jmadzo	ALL=(ALL)	ALL
kkeith	ALL=(ALL)	ALL
```
