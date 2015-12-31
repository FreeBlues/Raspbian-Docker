# Raspbian-Docker
Use Docker on RaspberryPi with raspbian and Kano system


##  A solution of creating base image from a Linux system tar file.

-    Step1 Install docker.io with apt-get

```
apt-get install docker.io
```
the docker version is 1.3.3

-    Step2 Create base image with the [ArchLinux](http://212.187.212.74/bt/ab301ea7ea245c12ea9babf5235d75b04890bbd4/data/ArchLinuxARM-2014.10-rpi-rootfs.tar.gz), the command is:

```
pi@rpi ~/notebooks $ wget http://212.187.212.74/bt/ab301ea7ea245c12ea9babf5235d75b04890bbd4/data/ArchLinuxARM-2014.10-rpi-rootfs.tar.gz
--2015-12-30 17:02:23--  http://212.187.212.74/bt/ab301ea7ea245c12ea9babf5235d75b04890bbd4/data/ArchLinuxARM-2014.10-rpi-rootfs.tar.gz
Connecting to 212.187.212.74:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 220637379 (210M) [application/x-gzip]
Saving to: `ArchLinuxARM-2014.10-rpi-rootfs.tar.gz'

74% [================================================================================>                             ] 163,600,832 --.-K/s   in 55m 51s

2015-12-30 17:58:15 (47.7 KB/s) - Read error at byte 163600832/220637379 (Connection timed out). Retrying.

--2015-12-30 17:58:16--  (try: 2)  http://212.187.212.74/bt/ab301ea7ea245c12ea9babf5235d75b04890bbd4/data/ArchLinuxARM-2014.10-rpi-rootfs.tar.gz
Connecting to 212.187.212.74:80... connected.
HTTP request sent, awaiting response... 206 Partial Content
Length: 220637379 (210M), 57036547 (54M) remaining [application/x-gzip]
Saving to: `ArchLinuxARM-2014.10-rpi-rootfs.tar.gz'

100%[+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++============================>] 220,637,379  837K/s   in 79s

2015-12-30 17:59:36 (703 KB/s) - `ArchLinuxARM-2014.10-rpi-rootfs.tar.gz' saved [220637379/220637379]

pi@rpi ~/notebooks $
``` 

-    Step3 Import the base image with `car` and `docker import`, after that you can use the image:

```
pi@rpi ~/notebooks $ cat ArchLinuxARM-2014.10-rpi-rootfs.tar.gz |sudo  docker import - archlinux
46b927e18f3bb69337c58ae1e195f34eea7b17d0c71ef5dad63d6cbce102f844
pi@rpi ~/notebooks $ sudo docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
archlinux           latest              46b927e18f3b        5 minutes ago       445.6 MB
raring              latest              e0168fc30ed0        About an hour ago   0 B
alpine              3.3.0               0a0aa665bfa2        2 hours ago         85.02 MB
ubuntu              14.04               723d8ba23c53        4 hours ago         204.8 MB
pi@rpi ~/notebooks $ sudo docker run -ti archlinux /bin/bash
[root@d7e0d53e291c /]# ls
bin  boot  dev  etc  home  lib  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@d7e0d53e291c /]#
```

---

My Raspberry PI installed raspbian, the version:
```
pi@rpi ~ $ uname -a
Linux rpi 4.1.13-v7+ #826 SMP PREEMPT Fri Nov 13 20:19:03 GMT 2015 armv7l GNU/Linux
pi@rpi ~ $ 
```

Docker version and info:

```
pi@rpi ~ $ sudo docker --version
Docker version 1.3.3, build d344625
pi@rpi ~ $ sudo docker info
Containers: 0
Images: 5
Storage Driver: devicemapper
 Pool Name: docker-179:2-73614-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 1.203 GB
 Data Space Total: 107.4 GB
 Metadata Space Used: 1.286 MB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.90 (2014-09-01)
Execution Driver: native-0.2
Kernel Version: 4.1.13-v7+
Operating System: Raspbian GNU/Linux 8 (jessie)
WARNING: No swap limit support
pi@rpi ~ $ 
```
