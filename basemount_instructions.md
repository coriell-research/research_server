## Basemount Instructions

### Setup

1. Make a directory for basespace to mount to

```bash
[kkeith]$ mkdir /mnt/data/data_kk/basespace
```
2. Mount basespace

```bash
[kkeith]$ basemount basespace
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount basespace
From:
    /home/kkeith/data

Starting authentication.

You need to authenticate by opening this URL in a browser:
  https://basespace.illumina.com/oauth/device?code=WqZAc
```
3. Paste the URL into a browser window, log into Illumina Basespace, and then hit Accept. Then in your terminal you should see a message saying it worked.

```bash
It worked!
Your identification has been saved.

Mounting BaseSpace account.
To unmount, run: basemount --unmount /mnt/data/data_kk/basespace
```
4. When you're finished using basespace, unmount it

```bash
[kkeith]$ basemount --unmount basespace
```

#### Setup Multiple Accounts

After you setup the first account, go to `~/.basespace` and rename the configuration file.

```bash
[kkeith]$ cd ~/.basespace/
[kkeith]$ ll
total 4
-rw-------. 1 kkeith research 157 Mar 27 13:45 default.cfg
[kkeith]$ mv default.cfg temple_kkeith.cfg
[kkeith]$ ll
total 4
-rw-------. 1 kkeith research 157 Mar 27 13:45 temple_kkeith.cfg

```
Now you can mount basespace specifying the configuration using `--config` and the configuration file name (without the .cfg)

```bash
[kkeith]$ cd /mnt/data/data_kk/
[kkeith]$ basemount --config temple_kkeith basespace
```
To set up the next account, unmount basespace and repeat steps 2-4 above. Make sure you are **LOGGED OUT** of basespace in your browser.

```bash
[kkeith]$ basemount --unmount basespace/
[kkeith]$ basemount basespace
basemount basespace/
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount basespace/
From:
    /home/kkeith/data

Starting authentication.

You need to authenticate by opening this URL in a browser:
  https://basespace.illumina.com/oauth/device?code=qUMtO
...
It worked!
Your identification has been saved.

Mounting BaseSpace account.
To unmount, run: basemount --unmount /mnt/data/data_kk/basespace
[kkeith]$ basemount --unmount basespace/
```
Now go back to `~/.basespace` and rename the new `default.cfg` file

```bash
[kkeith]$ cd ~/.basespace
[kkeith]$ ll
total 8
-rw-------. 1 kkeith research 157 Mar 27 13:45 default.cfg
-rw-------. 1 kkeith research 157 Mar 14 09:15 temple_kkeith.cfg
[kkeith]$ mv default.cfg coriell_kkeith.cfg
[kkeith]$ ll
total 8
-rw-------. 1 kkeith research 157 Mar 27 13:45 coriell_kkeith.cfg
-rw-------. 1 kkeith research 157 Mar 14 09:15 temple_kkeith.cfg
```
You can now log into either account by specifying the correct configuration

```bash
[kkeith]$ cd /mnt/data/data_kk/
[kkeith]$ basemount --config temple_kkeith basespace/
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount --config temple_kkeith basespace/
From:
    /mnt/data/data_kk

Api Server: https://api.basespace.illumina.com/

Mounting BaseSpace account.
To unmount, run: basemount --unmount /mnt/data/data_kk/basespace

[kkeith]$ ll basespace/Projects/
[kkeith]$ basemount --unmount basespace/
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount --unmount basespace/
From:
    /mnt/data/data_kk

* Soft unmounting of /mnt/data/data_kk/basespace
Launching: fusermount -u /mnt/data/data_kk/basespace

/mnt/data/data_kk/basespace was succesfully unmounted.
[kkeith]$ basemount --config coriell_kkeith basespace/
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount --config coriell_kkeith basespace/
From:
    /mnt/data/data_kk

Api Server: https://api.basespace.illumina.com/

Mounting BaseSpace account.
To unmount, run: basemount --unmount /mnt/data/data_kk/basespace

[kkeith]$ ll basespace/Projects/
total 0
[kkeith]$ basemount --unmount basespace/
,-----.                        ,--.   ,--.                         ,--.   
|  |) /_  ,--,--. ,---.  ,---. |   `.'   | ,---. ,--.,--.,--,--, ,-'  '-. 
|  .-.  \' ,-.  |(  .-' | .-. :|  |'.'|  || .-. ||  ||  ||      \'-.  .-'
|  '--' /\ '-'  |.-'  `)\   --.|  |   |  |' '-' ''  ''  '|  ||  |  |  |  
`------'  `--`--'`----'  `----'`--'   `--' `---'  `----' `--''--'  `--' 
Illumina BaseMount v0.15.96.2155 public  2018-06-04 16:24

Command called:
    basemount --unmount basespace/
From:
    /mnt/data/data_kk

* Soft unmounting of /mnt/data/data_kk/basespace
Launching: fusermount -u /mnt/data/data_kk/basespace

/mnt/data/data_kk/basespace was succesfully unmounted.
``` 
### Normal Usage

To mount, optionally specify the config (account) to use, and the directory to mount to.

```bash
[kkeith]$ basemount --config coriell_kkeith /mnt/data/data_kk/basespace
```
To unmount:

```bash
[kkeith]$ basemount --unmount /mnt/data/data_kk/basespace
```