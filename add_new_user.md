## Make a New User

Add the new user

```bash
# log in as root
su

# add the user
useradd -g <groupname> <username>
useradd -g research jjelinek

# let the user put their password in
passwd <username>
```
Set up the user's directory

```bash
# make a data folder and an ncbi folder for the user on the data disks
# still be root
cd /mnt/data
mkdir data_<userinitials>
# example: mkdir data_jj
mkdir data_<userinitials>/ncbi
# example: mkdir data_jj/ncbi

# change user, group and permissions for the new folders
chown -R <username>:<groupname> data_<userinitials>
# example: chown -R jmadzo:research data_jm
chmod -R 775 data_<userinitials>
# example: chmod -R 775 data_jm

#####

# soft link the data folders from the user's home directory
# still be root
cd /home/<username>
ln -s /mnt/data/data_<userinitals>/ data
# example: ln -s /mnt/data/data_jj/ data
ln -s /mnt/data/data_<userinitials>/ncbi/ ncbi
# example: ln -s /mnt/data/data_jj/ncbi/ ncbi

# change owner, group for soft links
chown -R <username>:<groupname> *
# example: chown -R jmadzo:research *

# make sure all /home/<username> permissions are 775 for easy collaboration
cd /home
chmod -R 775 <username>
# example: chmod -R 775 kkeith 
```