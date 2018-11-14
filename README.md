卸载老版本docker
```
[vagrant@localhost ~]$  sudo yum remove docker \
>                   docker-client \
>                   docker-client-latest \
>                   docker-common \
>                   docker-latest \
>                   docker-latest-logrotate \
>                   docker-logrotate \
>                   docker-selinux \
>                   docker-engine-selinux \
>                   docker-engine
Loaded plugins: fastestmirror
No Match for argument: docker
No Match for argument: docker-client
No Match for argument: docker-client-latest
No Match for argument: docker-common
No Match for argument: docker-latest
No Match for argument: docker-latest-logrotate
No Match for argument: docker-logrotate
No Match for argument: docker-selinux
No Match for argument: docker-engine-selinux
No Match for argument: docker-engine
No Packages marked for removal
[vagrant@localhost ~]$
```
安装组件包
```
[vagrant@localhost ~]$ sudo yum install -y yum-utils \
>   device-mapper-persistent-data \
>   lvm2
Loaded plugins: fastestmirror
Determining fastest mirrors
 * base: mirrors.cn99.com
 * extras: mirrors.cn99.com
 * updates: mirrors.cn99.com
base                                                                                             | 3.6 kB  00:00:00     
extras                                                                                           | 3.4 kB  00:00:00     
updates                                                                                          | 3.4 kB  00:00:00     
(2/4): base/7/x86_64/primary_db               0% [                                    ]  0.0 B/s |    0 B  --:--:-- ETA (1/4): extras/7/x86_64/primary_db                                                                | 205 kB  00:00:00     
(3/4): base/7/x86_64/primary_db               2% [-                                   ]  0.0 B/s | 330 kB  --:--:-- ETA (2/4): base/7/x86_64/group_gz                                                                    | 166 kB  00:00:00     
(4/4): updates/7/x86_64/primary_db            10% [===-                               ] 1.6 MB/s | 1.3 MB  00:00:07 ETA (4/4): updates/7/x86_64/primary_db            15% [=====                              ] 1.6 MB/s | 1.9 MB  00:00:06 ETA (3/4): base/7/x86_64/primary_db               19% [======-                            ] 1.6 MB/s | 2.4 MB  00:00:06 ETA (3/4): base/7/x86_64/primary_db               24% [========-                          ] 1.6 MB/s | 3.1 MB  00:00:05 ETA (3/4): base/7/x86_64/primary_db               29% [==========                         ] 1.6 MB/s | 3.6 MB  00:00:05 ETA (3/4): base/7/x86_64/primary_db               34% [===========-                       ] 1.6 MB/s | 4.2 MB  00:00:04 ETA (4/4): updates/7/x86_64/primary_db            38% [=============-                     ] 1.6 MB/s | 4.8 MB  00:00:04 ETA (4/4): updates/7/x86_64/primary_db            43% [===============                    ] 1.6 MB/s | 5.4 MB  00:00:04 ETA (4/4): updates/7/x86_64/primary_db            48% [================-                  ] 1.7 MB/s | 5.9 MB  00:00:03 ETA (3/4): updates/7/x86_64/primary_db                                                               | 6.0 MB  00:00:04     
base/7/x86_64/primary_db       FAILED
(4/4): base/7/x86_64/primary_db               48% [================-                  ] 1.7 MB/s | 5.9 MB  00:00:03 ETA http://mirrors.zju.edu.cn/centos/7.5.1804/os/x86_64/repodata/03d0a660eb33174331aee3e077e11d4c017412d761b7f2eaa8555e7898e701e0-primary.sqlite.bz2: [Errno 12] Timeout on http://113.215.26.196/files/52490000000016B0/mirror.bit.edu.cn/centos/7.5.1804/os/x86_64/repodata/03d0a660eb33174331aee3e077e11d4c017412d761b7f2eaa8555e7898e701e0-primary.sqlite.bz2: (28, 'Connection timed out after 30996 milliseconds')
Trying other mirror.
(4/4): base/7/x86_64/primary_db               58% [====================               ]  46 kB/s | 7.2 MB  00:01:53 ETA (4/4): base/7/x86_64/primary_db               63% [======================             ] 162 kB/s | 7.8 MB  00:00:28 ETA (4/4): base/7/x86_64/primary_db               67% [=======================-           ] 269 kB/s | 8.3 MB  00:00:14 ETA (4/4): base/7/x86_64/primary_db               71% [========================-          ] 333 kB/s | 8.8 MB  00:00:10 ETA (4/4): base/7/x86_64/primary_db               77% [===========================        ] 460 kB/s | 9.5 MB  00:00:06 ETA (4/4): base/7/x86_64/primary_db               81% [============================-      ] 550 kB/s |  10 MB  00:00:04 ETA (4/4): base/7/x86_64/primary_db               86% [==============================     ] 637 kB/s |  11 MB  00:00:02 ETA (4/4): base/7/x86_64/primary_db               91% [===============================-   ] 713 kB/s |  11 MB  00:00:01 ETA (4/4): base/7/x86_64/primary_db               95% [=================================- ] 775 kB/s |  12 MB  00:00:00 ETA (4/4): base/7/x86_64/primary_db                                                                  | 5.9 MB  00:00:03     
Package yum-utils-1.1.31-46.el7_5.noarch already installed and latest version
Resolving Dependencies
--> Running transaction check
---> Package device-mapper-persistent-data.x86_64 0:0.7.3-3.el7 will be installed
--> Processing Dependency: libaio.so.1(LIBAIO_0.4)(64bit) for package: device-mapper-persistent-data-0.7.3-3.el7.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.1)(64bit) for package: device-mapper-persistent-data-0.7.3-3.el7.x86_64
--> Processing Dependency: libaio.so.1()(64bit) for package: device-mapper-persistent-data-0.7.3-3.el7.x86_64
---> Package lvm2.x86_64 7:2.02.177-4.el7 will be installed
--> Processing Dependency: lvm2-libs = 7:2.02.177-4.el7 for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: liblvm2app.so.2.2(Base)(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: libdevmapper-event.so.1.02(Base)(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: liblvm2app.so.2.2()(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: libdevmapper-event.so.1.02()(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Running transaction check
---> Package device-mapper-event-libs.x86_64 7:1.02.146-4.el7 will be installed
---> Package libaio.x86_64 0:0.3.109-13.el7 will be installed
---> Package lvm2-libs.x86_64 7:2.02.177-4.el7 will be installed
--> Processing Dependency: device-mapper-event = 7:1.02.146-4.el7 for package: 7:lvm2-libs-2.02.177-4.el7.x86_64
--> Running transaction check
---> Package device-mapper-event.x86_64 7:1.02.146-4.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

========================================================================================================================
 Package                                    Arch                Version                         Repository         Size
========================================================================================================================
Installing:
 device-mapper-persistent-data              x86_64              0.7.3-3.el7                     base              405 k
 lvm2                                       x86_64              7:2.02.177-4.el7                base              1.3 M
Installing for dependencies:
 device-mapper-event                        x86_64              7:1.02.146-4.el7                base              185 k
 device-mapper-event-libs                   x86_64              7:1.02.146-4.el7                base              184 k
 libaio                                     x86_64              0.3.109-13.el7                  base               24 k
 lvm2-libs                                  x86_64              7:2.02.177-4.el7                base              1.0 M

Transaction Summary
========================================================================================================================
Install  2 Packages (+4 Dependent packages)

Total download size: 3.1 M
Installed size: 7.8 M
Downloading packages:
(2/6): device-mapper-event-libs-1.02.146-4.el 0% [                                    ]  0.0 B/s |    0 B  --:--:-- ETA warning: /var/cache/yum/x86_64/7/base/packages/device-mapper-event-1.02.146-4.el7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID f4a80eb5: NOKEY
Public key for device-mapper-event-1.02.146-4.el7.x86_64.rpm is not installed
(1/6): device-mapper-event-1.02.146-4.el7.x86_64.rpm                                             | 185 kB  00:00:00     
(2/6): libaio-0.3.109-13.el7.x86_64.rpm                                                          |  24 kB  00:00:00     
(4/6): device-mapper-persistent-data-0.7.3-3. 6% [==                                  ]  0.0 B/s | 209 kB  --:--:-- ETA (3/6): lvm2-libs-2.02.177-4.el7.x86_64.rpm                                                       | 1.0 MB  00:00:00     
(5/6): device-mapper-persistent-data-0.7.3-3. 63% [======================             ] 2.8 MB/s | 2.0 MB  00:00:00 ETA (4/6): lvm2-2.02.177-4.el7.x86_64.rpm                                                            | 1.3 MB  00:00:01     
(6/6): device-mapper-persistent-data-0.7.3-3. 87% [==============================-    ] 2.8 MB/s | 2.7 MB  00:00:00 ETA (5/6): device-mapper-event-libs-1.02.146-4.el 90% [===============================-   ] 2.6 MB/s | 2.8 MB  00:00:00 ETA (5/6): device-mapper-event-libs-1.02.146-4.el 94% [================================-  ] 2.5 MB/s | 2.9 MB  00:00:00 ETA (5/6): device-mapper-persistent-data-0.7.3-3.el7.x86_64.rpm                                      | 405 kB  00:00:02     
(6/6): device-mapper-event-libs-1.02.146-4.el 94% [================================-  ] 2.0 MB/s | 2.9 MB  00:00:00 ETA (6/6): device-mapper-event-libs-1.02.146-4.el 96% [=================================- ] 1.9 MB/s | 3.0 MB  00:00:00 ETA (6/6): device-mapper-event-libs-1.02.146-4.e 100% [===================================] 1.8 MB/s | 3.1 MB  00:00:00 ETA (6/6): device-mapper-event-libs-1.02.146-4.el7.x86_64.rpm                                        | 184 kB  00:00:03     
------------------------------------------------------------------------------------------------------------------------
Total                                                                                   775 kB/s | 3.1 MB  00:00:04     
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Importing GPG key 0xF4A80EB5:
 Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 Package    : centos-release-7-5.1804.4.el7.centos.x86_64 (@koji-override-1)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 7:device-mapper-event-libs-1.02.146-4.el7.x86_64                                                     1/6 
  Installing : 7:device-mapper-event-1.02.146-4.el7.x86_64                                                          2/6 
  Installing : 7:lvm2-libs-2.02.177-4.el7.x86_64                                                                    3/6 
  Installing : libaio-0.3.109-13.el7.x86_64                                                                         4/6 
  Installing : device-mapper-persistent-data-0.7.3-3.el7.x86_64                                                     5/6 
  Installing : 7:lvm2-2.02.177-4.el7.x86_64                                                                         6/6 
  Verifying  : device-mapper-persistent-data-0.7.3-3.el7.x86_64                                                     1/6 
  Verifying  : 7:lvm2-2.02.177-4.el7.x86_64                                                                         2/6 
  Verifying  : 7:device-mapper-event-1.02.146-4.el7.x86_64                                                          3/6 
  Verifying  : 7:device-mapper-event-libs-1.02.146-4.el7.x86_64                                                     4/6 
  Verifying  : 7:lvm2-libs-2.02.177-4.el7.x86_64                                                                    5/6 
  Verifying  : libaio-0.3.109-13.el7.x86_64                                                                         6/6 

Installed:
  device-mapper-persistent-data.x86_64 0:0.7.3-3.el7                    lvm2.x86_64 7:2.02.177-4.el7

Dependency Installed:
  device-mapper-event.x86_64 7:1.02.146-4.el7              device-mapper-event-libs.x86_64 7:1.02.146-4.el7             
  libaio.x86_64 0:0.3.109-13.el7                           lvm2-libs.x86_64 7:2.02.177-4.el7                            

Complete!
[vagrant@localhost ~]$
```
添加docker稳定版本库
```
[vagrant@localhost ~]$ sudo yum-config-manager \
>     --add-repo \
>     https://download.docker.com/linux/centos/docker-ce.repo
Loaded plugins: fastestmirror
adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
repo saved to /etc/yum.repos.d/docker-ce.repo
```

查看所有可装版本
```
[vagrant@localhost ~]$ yum list docker-ce --showduplicates | sort -r

 * updates: mirrors.cn99.com
Loaded plugins: fastestmirror
 * extras: mirrors.cn99.com
docker-ce.x86_64            3:18.09.0-3.el7                     docker-ce-stable
docker-ce.x86_64            18.06.1.ce-3.el7                    docker-ce-stable
docker-ce.x86_64            18.06.0.ce-3.el7                    docker-ce-stable
docker-ce.x86_64            18.03.1.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            18.03.0.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.12.1.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.12.0.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.09.1.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.09.0.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.06.2.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.06.1.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.06.0.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.03.3.ce-1.el7                    docker-ce-stable
docker-ce.x86_64            17.03.2.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.03.1.ce-1.el7.centos             docker-ce-stable
docker-ce.x86_64            17.03.0.ce-1.el7.centos             docker-ce-stable
Determining fastest mirrors
 * base: mirrors.cn99.com
Available Packages
[vagrant@localhost ~]$

安装docker
[vagrant@localhost ~]$ sudo yum install docker-ce
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.cn99.com
 * extras: mirrors.cn99.com
 * updates: mirrors.cn99.com
Resolving Dependencies
--> Running transaction check
---> Package docker-ce.x86_64 3:18.09.0-3.el7 will be installed
--> Processing Dependency: container-selinux >= 2.9 for package: 3:docker-ce-18.09.0-3.el7.x86_64
--> Processing Dependency: containerd.io for package: 3:docker-ce-18.09.0-3.el7.x86_64
--> Processing Dependency: docker-ce-cli for package: 3:docker-ce-18.09.0-3.el7.x86_64
--> Running transaction check
---> Package container-selinux.noarch 2:2.68-1.el7 will be installed
--> Processing Dependency: policycoreutils-python for package: 2:container-selinux-2.68-1.el7.noarch
---> Package containerd.io.x86_64 0:1.2.0-3.el7 will be installed
---> Package docker-ce-cli.x86_64 1:18.09.0-3.el7 will be installed
--> Running transaction check
---> Package policycoreutils-python.x86_64 0:2.5-22.el7 will be installed
--> Processing Dependency: setools-libs >= 3.3.8-2 for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libsemanage-python >= 2.5-9 for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: audit-libs-python >= 2.1.3-4 for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: python-IPy for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libqpol.so.1(VERS_1.4)(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libqpol.so.1(VERS_1.2)(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libcgroup for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libapol.so.4(VERS_4.0)(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: checkpolicy for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libqpol.so.1()(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libapol.so.4()(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Running transaction check
---> Package audit-libs-python.x86_64 0:2.8.1-3.el7_5.1 will be installed
---> Package checkpolicy.x86_64 0:2.5-6.el7 will be installed
---> Package libcgroup.x86_64 0:0.41-15.el7 will be installed
---> Package libsemanage-python.x86_64 0:2.5-11.el7 will be installed
---> Package python-IPy.noarch 0:0.75-6.el7 will be installed
---> Package setools-libs.x86_64 0:3.3.8-2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

========================================================================================================================
 Package                            Arch               Version                       Repository                    Size
========================================================================================================================
Installing:
 docker-ce                          x86_64             3:18.09.0-3.el7               docker-ce-stable              19 M
Installing for dependencies:
 audit-libs-python                  x86_64             2.8.1-3.el7_5.1               updates                       75 k
 checkpolicy                        x86_64             2.5-6.el7                     base                         294 k
 container-selinux                  noarch             2:2.68-1.el7                  extras                        36 k
 containerd.io                      x86_64             1.2.0-3.el7                   docker-ce-stable              22 M
 docker-ce-cli                      x86_64             1:18.09.0-3.el7               docker-ce-stable              14 M
 libcgroup                          x86_64             0.41-15.el7                   base                          65 k
 libsemanage-python                 x86_64             2.5-11.el7                    base                         112 k
 policycoreutils-python             x86_64             2.5-22.el7                    base                         454 k
 python-IPy                         noarch             0.75-6.el7                    base                          32 k
 setools-libs                       x86_64             3.3.8-2.el7                   base                         619 k

Transaction Summary
========================================================================================================================
Install  1 Package (+10 Dependent packages)

Total size: 56 M
Installed size: 241 M
Is this ok [y/d/N]: y
Downloading packages:
warning: /var/cache/yum/x86_64/7/docker-ce-stable/packages/docker-ce-18.09.0-3.el7.x86_64.rpm: Header V4 RSA/SHA512 Signature, key ID 621e9f35: NOKEY
Retrieving key from https://download.docker.com/linux/centos/gpg
Importing GPG key 0x621E9F35:
 Userid     : "Docker Release (CE rpm) <docker@docker.com>"
 Fingerprint: 060a 61c5 1b55 8a7f 742b 77aa c52f eb6b 621e 9f35
 From       : https://download.docker.com/linux/centos/gpg
Is this ok [y/N]: y
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : containerd.io-1.2.0-3.el7.x86_64                                                                    1/11 
  Installing : 1:docker-ce-cli-18.09.0-3.el7.x86_64                                                                2/11 
  Installing : audit-libs-python-2.8.1-3.el7_5.1.x86_64                                                            3/11 
  Installing : python-IPy-0.75-6.el7.noarch                                                                        4/11 
  Installing : checkpolicy-2.5-6.el7.x86_64                                                                        5/11 
  Installing : libcgroup-0.41-15.el7.x86_64                                                                        6/11 
  Installing : setools-libs-3.3.8-2.el7.x86_64                                                                     7/11 
  Installing : libsemanage-python-2.5-11.el7.x86_64                                                                8/11 
  Installing : policycoreutils-python-2.5-22.el7.x86_64                                                            9/11 
  Installing : 2:container-selinux-2.68-1.el7.noarch                                                              10/11 
  Installing : 3:docker-ce-18.09.0-3.el7.x86_64                                                                   11/11 
  Verifying  : libsemanage-python-2.5-11.el7.x86_64                                                                1/11 
  Verifying  : 3:docker-ce-18.09.0-3.el7.x86_64                                                                    2/11 
  Verifying  : setools-libs-3.3.8-2.el7.x86_64                                                                     3/11 
  Verifying  : policycoreutils-python-2.5-22.el7.x86_64                                                            4/11 
  Verifying  : libcgroup-0.41-15.el7.x86_64                                                                        5/11 
  Verifying  : 2:container-selinux-2.68-1.el7.noarch                                                               6/11 
  Verifying  : checkpolicy-2.5-6.el7.x86_64                                                                        7/11 
  Verifying  : 1:docker-ce-cli-18.09.0-3.el7.x86_64                                                                8/11 
  Verifying  : python-IPy-0.75-6.el7.noarch                                                                        9/11 
  Verifying  : containerd.io-1.2.0-3.el7.x86_64                                                                   10/11 
  Verifying  : audit-libs-python-2.8.1-3.el7_5.1.x86_64                                                           11/11 

Installed:
  docker-ce.x86_64 3:18.09.0-3.el7                                                                                      

Dependency Installed:
  audit-libs-python.x86_64 0:2.8.1-3.el7_5.1                 checkpolicy.x86_64 0:2.5-6.el7
  container-selinux.noarch 2:2.68-1.el7                      containerd.io.x86_64 0:1.2.0-3.el7
  docker-ce-cli.x86_64 1:18.09.0-3.el7                       libcgroup.x86_64 0:0.41-15.el7
  libsemanage-python.x86_64 0:2.5-11.el7                     policycoreutils-python.x86_64 0:2.5-22.el7
  python-IPy.noarch 0:0.75-6.el7                             setools-libs.x86_64 0:3.3.8-2.el7

Complete!
[vagrant@localhost ~]$
```
安装指定版本docker
```
$ sudo yum install docker-ce-<VERSION STRING>
```

启动docker
```
[vagrant@localhost ~]$ sudo systemctl start docker
[vagrant@localhost ~]$ ps ax | grep docker
 2782 ?        Ssl    0:00 /usr/bin/dockerd -H unix://
 2796 ?        Ssl    0:00 containerd --config /var/run/docker/containerd/containerd.toml --log-level info
 2942 pts/0    S+     0:00 grep --color=auto docker
[vagrant@localhost ~]$
```
docker运行实例镜像
```
[vagrant@localhost ~]$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
d1725b59e92d: Pull complete
Digest: sha256:0add3ace90ecb4adbf7777e9aacf18357296e799f81cabc9fde470971e499788
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

docker运行实例镜像
```
[vagrant@localhost ~]$ sudo docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
473ede7ed136: Pull complete
c46b5fa4d940: Pull complete
93ae3df89c92: Pull complete
6b1eed27cade: Pull complete
Digest: sha256:29934af957c53004d7fb6340139880d23fb1952505a15d69a03af0d1418878cb
Status: Downloaded newer image for ubuntu:latest
root@e92bbf2bf6e9:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@e92bbf2bf6e9:/#
root@e92bbf2bf6e9:/#
root@e92bbf2bf6e9:/# getcpuinfo
bash: getcpuinfo: command not found
root@e92bbf2bf6e9:/# getsysinfo
bash: getsysinfo: command not found
root@e92bbf2bf6e9:/# uname -a
Linux e92bbf2bf6e9 3.10.0-862.14.4.el7.x86_64 #1 SMP Wed Sep 26 15:12:11 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
root@e92bbf2bf6e9:/# lsb_release -a
bash: lsb_release: command not found
root@e92bbf2bf6e9:/# cat /etc/issue
Ubuntu 18.04.1 LTS \n \l

root@e92bbf2bf6e9:/#
```
docker的卸载
```
1/卸载程序包
sudo yum remove docker-ce
2/删除相关文件
sudo rm -rf /var/lib/docker
```
```
[vagrant@localhost ~]$ docker version
Client:
 Version:           18.09.0
 API version:       1.39
 Go version:        go1.10.4
 Git commit:        4d60db4
 Built:             Wed Nov  7 00:48:22 2018
 OS/Arch:           linux/amd64
 Experimental:      false
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/version: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$
```
```
[vagrant@localhost ~]$ sudo docker version
Client:
 Version:           18.09.0
 API version:       1.39
 Go version:        go1.10.4
 Git commit:        4d60db4
 Built:             Wed Nov  7 00:48:22 2018
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.0
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.4
  Git commit:       4d60db4
  Built:            Wed Nov  7 00:19:08 2018
  OS/Arch:          linux/amd64
  Experimental:     false
[vagrant@localhost ~]$
```
```
[vagrant@localhost ~]$ docker-machine version
-bash: docker-machine: command not found
```
解决办法<br>
https://github.com/docker/machine/releases<br>
```
curl -L https://github.com/docker/machine/releases/download/v0.16.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
    chmod +x /tmp/docker-machine &&
    sudo cp /tmp/docker-machine /usr/local/bin/docker-machine

[vagrant@localhost ~]$ docker-machine -v
docker-machine version 0.16.0, build 702c267f
[vagrant@localhost ~]$
```
查看服务器上所有镜像
```
[vagrant@localhost ~]$ sudo docker image ls

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              4ab4c602aa5e        2 months ago        1.84kB
```
docker获取镜像的三种方式：
1-通过dockerfile构建；
2-通过registry拉取：
```
[vagrant@localhost ~]$ sudo docker pull ubuntu:14.04
14.04: Pulling from library/ubuntu
027274c8e111: Pull complete
d3f9339a1359: Pull complete
872f75707cf4: Pull complete
dd5eed9f50d5: Pull complete
Digest: sha256:e6e808ab8c62f1d9181817aea804ae4ba0897b8bd3661d36dbc329b5851b5637
Status: Downloaded newer image for ubuntu:14.04
[vagrant@localhost ~]$
```
添加用户到docker分组下
```
[vagrant@localhost ~]$ docker image ls

Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$
[vagrant@localhost ~]$
[vagrant@localhost ~]$ docker image ls
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$ sudo groupadd docker
groupadd: group 'docker' already exists
[vagrant@localhost ~]$ sudo gpasswd -a vagrant docker
Adding user vagrant to group docker
[vagrant@localhost ~]$ docker image ls
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$
[vagrant@localhost ~]$ sudo service docker restart
Redirecting to /bin/systemctl restart docker.service
[vagrant@localhost ~]$ docker image ls
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$ exit
```
自定义基本镜像
```
[vagrant@localhost sayhi]$ cat sayhi.c
#include<stdio.h>
int main(){
        printf("Hi!\n");
}
[vagrant@localhost sayhi]$
[vagrant@localhost sayhi]$ gcc -static sayhi.c -o sayhi
[vagrant@localhost sayhi]$ ls
sayhi  sayhi.c
[vagrant@localhost sayhi]$ ./sayhi
Hi!
[vagrant@localhost sayhi]$ cat Dockerfile
FROM scratch
ADD sayhi /
CMD ["/sayhi"]
[vagrant@localhost sayhi]$
[vagrant@localhost sayhi]$ docker build -t yubiaohyb/sayhi .
Sending build context to Docker daemon  864.8kB
Step 1/3 : FROM scratch
 --->
Step 2/3 : ADD sayhi /
 ---> 1a380afb9d12
Step 3/3 : CMD ["/sayhi"]
 ---> Running in 8a31a66738e4
Removing intermediate container 8a31a66738e4
 ---> 2b84f6b4e970
Successfully built 2b84f6b4e970
Successfully tagged yubiaohyb/sayhi:latest
[vagrant@localhost sayhi]$ docker image ls

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
yubiaohyb/sayhi     latest              2b84f6b4e970        3 minutes ago       861kB
ubuntu              14.04               f216cfb59484        3 weeks ago         188MB
hello-world         latest              4ab4c602aa5e        2 months ago        1.84kB
[vagrant@localhost sayhi]$ docker run yubiaohyb/sayhi
Hi!
[vagrant@localhost sayhi]$ ls -lh
total 852K
-rw-rw-r--. 1 vagrant vagrant   40 Nov 14 11:27 Dockerfile
-rwxrwxr-x. 1 vagrant vagrant 841K Nov 14 11:25 sayhi
-rw-rw-r--. 1 vagrant vagrant   50 Nov 14 11:08 sayhi.c
[vagrant@localhost sayhi]$ docker history 2b84f6b4e970
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
2b84f6b4e970        12 minutes ago      /bin/sh -c #(nop)  CMD ["/sayhi"]               0B
1a380afb9d12        12 minutes ago      /bin/sh -c #(nop) ADD file:ed2d8976b0c808c2b…   861kB
[vagrant@localhost sayhi]$
[vagrant@localhost sayhi]$ docker run yubiaohyb/sayhi
Hi!
[vagrant@localhost sayhi]$
```
gcc环境安装
```
yum groupinstall "Development Tools"
yum install -y glibc-static
```
查看yum已安装列表
```
[vagrant@localhost sayhi]$ yum list installed | grep gcc
gcc.x86_64                           4.8.5-28.el7_5.1          @updates
gcc-c++.x86_64                       4.8.5-28.el7_5.1          @updates
gcc-gfortran.x86_64                  4.8.5-28.el7_5.1          @updates
libgcc.x86_64                        4.8.5-28.el7_5.1          @koji-override-1
[vagrant@localhost sayhi]$
```
