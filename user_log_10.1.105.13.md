## Users 10.1.105.13

### Groups

```bash
[root]# groupadd research
[root]# groupadd bre
```

### Users

#### Main Bioinformatics Users

*2020-07-19* Jaroslav Jelinek

```bash
### Jaroslav Jelinek
[root]# useradd -g research jjelinek
[root]# passwd jjelinek
[root]# cd /mnt/data/
[root]# mkdir data_jj
[root]# chown -R jjelinek:research data_jj
[root]# cd /home/jjelinek/
[root]# ln -s /mnt/data/data_jj/ data
```
*2020-07-19* Jozef Madzo

```bash
### Jozef Madzo
[root]# useradd -g research jmadzo
[root]# passwd jmadzo
[root]# cd /mnt/data/
[root]# mkdir data_jm
[root]# chown -R jmadzo:research data_jm
[root]# cd /home/jmadzo/
[root]# ln -s /mnt/data/data_jm/ data
```
*2020-07-19* Kelsey Keith

```bash
### Kelsey Keith
[root]# useradd -g research kkeith
[root]# passwd kkeith
[root]# cd /mnt/data/
[root]# mkdir data_kk
[root]# chown -R kkeith:research data_kk
[root]# cd /home/kkeith/
[root]# ln -s /mnt/data/data_kk/ dat
```
*2020-07-19* Gennaro Calendo

```bash
### Gennaro Calendo
[root]# useradd -g research gcalendo
[root]# passwd gcalendo
[root]# cd /mnt/data/
[root]# mkdir data_gc
[root]# chown -R gcalendo:research data_gc
[root]# cd /home/gcalendo/
[root]# ln -s /mnt/data/data_gc/ data
```
#### 2020 Bioinformatics Research Experience Users
*2020-07-19*

```bash
### Joao Ferreira
useradd -g bre jferreira
passwd jferreira

### Josh Paulos
useradd -g bre jpaulos
passwd jpaulos

### Luisa Taverna
useradd -g bre ltaverna
passwd ltaverna

### Hosen Arman
useradd -g bre harman
passwd harman

### Robert Hughes
useradd -g bre rhughes
passwd rhughes

### Ivy Tran
useradd -g bre itran
passwd itran
```