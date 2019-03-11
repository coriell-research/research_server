# Coriell Research Server
*2019.03.11*

```bash
adduser kkeith
passwd kkeith

groupadd admin
usermod -g admin kkeith
usermod -g admin jmadzo

useradd -g research jjelinek
passwd jjelinek

chmod -R 775 jmadzo
chmod -R 775 kkeith

cd /mnt/data
mkdir data_kk
mkdir data_jm
mkdir data_jj
chown -R jmadzo:research data_jm
chown -R kkeith:research data_kk
chown -R jjelinek:research data_jj
chmod -R 775 data_jj
chmod -R 775 data_jm
chmod -R 775 data_kk

# soft link data folders for everyone
cd /home/jjelinek
ln -s /mnt/data/data_jj/ data
chown -R jjelinek:research data
chown -R jjelinek:research /mnt/data/data_jj/ncbi/
chmod -R 775 /mnt/data/data_jj/ncbi/
ln -s /mnt/data/data_jj/ncbi/ ncbi
chown -R jjelinek:research ncbi

cd ../jmadzo/
ln -s /mnt/data/data_jm/ data
mkdir /mnt/data/data_jm/ncbi
ln -s /mnt/data/data_jm/ncbi/ ncbi
chown -R jmadzo:research *

cd ../kkeith/
ln -s /mnt/data/data_kk/ data
mkdir /mnt/data/data_kk/ncbi
ln -s /mnt/data/data_kk/ncbi/ ncbi

### make sure all file ownership/permissions is correct
cd /home/jjelinek/
chown -R jjelinek:research *
chmod -R 775 *
cd /mnt/data/data_jj
chown -R jjelinek:research *
chmod -R 775 *

cd /home/jmadzo
chown -R jmadzo:research *
chmod -R 775 *
cd /mnt/data/data_jm/
chown -R jmadzo:research *
chmod -R 775 *

cd /home/kkeith
chown -R kkeith:research *
chmod -R 775 *
cd /mnt/data/data_kk/
chown -R kkeith:research *
chmod -R 775 *

### edit /etc/sudoers so we have sudo permissions
nano /etc/sudoers
# added lines for our user accounts under root
## Allow root to run any commands anywhere
root    ALL=(ALL)	ALL
jjelinek ALL=(ALL)	ALL
jmadzo	ALL=(ALL)	ALL
kkeith	ALL=(ALL)	ALL
```