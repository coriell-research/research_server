*2019-08-16* JJ changed hostname from localhost to **cbix**

added the following line to /etc/sysconfig/network

```bash
HOSTNAME=cbix2
```

edited /etc/hosts
by changing the first line

```bash
more /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
sudo nano /etc/hosts
more /etc/hosts
127.0.0.1   cbix2
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6


    127.0.0.1       cbix
    ::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
```

issued a command

```bash
 sudo hostname cbix
    ```