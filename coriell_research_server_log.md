# Coriell Research Server
IP address: 10.1.105.11

### Add New Users
*2019-10-28* Added **Woonbok Chung** as a user

```bash
sudo useradd -g research wchung
sudo passwd wchung
mkdir /mnt/data/data_wc
mkdir /mnt/data/data_wc/ncbi
ln -s /mnt/data/data_wc/ /home/wchung/data
ln -s /mnt/data/data_wc/ncbi/ /home/wchung/ncbi
sudo chown -R wchung:research /home/wchung/
sudo chmod -R 775 /home/wchung/
sudo chown -R wchung:research /mnt/data/data_wc/
sudo chmod -R 775 /mnt/data/data_wc/
```

*2019-10-28* Added **Hugh Huang** as a user

```bash
sudo useradd -g research hhuang
sudo passwd hhuang
mkdir /mnt/data/data_hh
mkdir /mnt/data/data_hh/ncbi
ln -s /mnt/data/data_hh/ /home/hhuang/data
ln -s /mnt/data/data_hh/ncbi/ /home/hhuang/ncbi
sudo chown -R hhuang:research /home/hhuang/
sudo chmod -R 775 /home/hhuang/
sudo chown -R hhuang /mnt/data/data_hh
sudo chmod -R 775 /mnt/data/data_hh
```

*2019-10-28* Added **Hye Seon Jeong** as a user

```bash
sudo useradd -g research hsjeong
sudo passwd hsjeong 
mkdir /mnt/data/data_hsj
mkdir /mnt/data/data_hsj/ncbi
sudo ln -s /mnt/data/data_hsj /home/hsjeong/data
ln -s /mnt/data/data_hsj/ncbi/ /home/hsjeong/ncbi
sudo chown -R hsjeong:research /home/hsjeong
sudo chmod -R 775 /home/hsjeong/
sudo chown -R hsjeong /mnt/data/data_hsj
sudo chmod -R 775 /mnt/data/data_hsj/
```

*2019-10-28* Added **Gennaro Calendo** as a user

```bash
sudo useradd -g research gcalendo
sudo passwd gcalendo
cd /mnt/data/
mkdir data_gc
mkdir data_pp/ncbi
sudo chown -R gcalendo:research data_gc
sudo chmod -R 775 data_gc/
cd /home/
sudo chmod -R 775 gcalendo/
cd gcalendo/
ln -s /mnt/data/data_gc/ data
ln -s /mnt/data/data_gc/ncbi/ ncbi
sudo chown -R gcalendo:research *
sudo chmod -R 775 *
```

*2019-03-25*, Added **Peace Park** as a user

```bash
useradd -g research ppark
passwd ppark
cd /mnt/data/
mkdir data_pp
mkdir data_pp/ncbi
chown -R ppark:research data_pp
chmod -R 775 data_pp
cd /home/ppark/
ln -s /mnt/data/data_pp data
ln -s /mnt/data/data_pp/ncbi ncbi
chown -R ppark:research *
chmod -R 775 ppark
```

*2019-03-25*, Added **Shohag Panjarian** as a user

```bash
useradd -g research spanjarian
passwd spanjarian
cd /mnt/data/
mkdir data_sp
mkdir data_sp/ncbi
chown -R spanjarian:research data_sp
chmod -R 775 data_sp
cd /home/spanjarian/
ln -s /mnt/data/data_sp data
ln -s /mnt/data/data_sp/ncbi ncbi
chown -R spanjarian:research *
chmod -R 775 spanjarian
```

*2019-03-25*, Added **Dara Kusic** as a user

```bash
su
useradd -g permed dkusic
passwd dkusic
cd /mnt/data/
mkdir data_dk
mkdir data_dk/ncbi
chown -R dkusic:permed data_dk
chmod -R 775 data_dk
cd /home/dkusic
ln -s /mnt/data/data_dk data
ln -s /mnt/data/data_dk/ncbi ncbi
chown -R dkusic:permed *
cd ..
chmod -R 775 dkusic
```

*2019-03-18*, Added **Sandra Deliard** as a user

```bash
su
useradd -g research sdeliard
passwd sdeliard
mkdir /mnt/data/data_sd
mkdir /mnt/data/data_sd/ncbi
chown -R sdeliard:research /mnt/data/data_sd
chmod -R 775 /mnt/data/data_sd
cd /home
ln -s /mnt/data/data_sd sdeliard/data
ln -s /mnt/data/data_sd/ncbi sdeliard/ncbi
chown -R sdeliard:research sdeliard/
chmod -R 775 sdeliard
```

*2019-03-14*, Added **Laura Scheinfeldt** as a user

```bash
su
groupadd permed
useradd -g permed lscheinfeldt
passwd lscheinfeldt
mkdir /mnt/data/data_ls
mkdir /mnt/data/data_ls/ncbi
chown -R lscheinfeldt:permed data_ls
chmod -R 775 data_ls
cd /home/lscheinfeldt
ln -s /mnt/data/data_ls data
ln -s /mnt/data/data_ls ncbi
chown -R lscheinfeldt:permed *
chmod -R 775 *
cd ../
chmod 775 lscheinfeldt
```

*2019-03-13*, Added **Himani Vaidya** as a user

```bash
su
useradd -g research hvaidya
passwd hvaidya # had Himani type her password in
cd /mnt/data/
mkdir data_hv
mkdir data_hv/ncbi
chown -R hvaidya:research data_hv
chmod -R 775 data_hv
cd /home/hvaidya/
ln -s /mnt/data/data_hv data
ln -s /mnt/data/data_hv/ncbi ncbi
chown -R hvaidya:research *
chmod -R 775 *
cd ../
chmod 775 hvaidya
```

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
