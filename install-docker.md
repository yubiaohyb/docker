### 卸载老版本docker
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
### 预装依赖包
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
### yum添加docker稳定版本库
```
[vagrant@localhost ~]$ sudo yum-config-manager \
>     --add-repo \
>     https://download.docker.com/linux/centos/docker-ce.repo
Loaded plugins: fastestmirror
adding repo from: https://download.docker.com/linux/centos/docker-ce.repo
grabbing file https://download.docker.com/linux/centos/docker-ce.repo to /etc/yum.repos.d/docker-ce.repo
repo saved to /etc/yum.repos.d/docker-ce.repo
```

### 查看所有可装版本
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
```
### 安装docker
```
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
### 安装指定版本docker
```
$ sudo yum install docker-ce-<VERSION STRING>
```

### 启动docker
```
[vagrant@localhost ~]$ sudo systemctl start docker
[vagrant@localhost ~]$ ps ax | grep docker
 2782 ?        Ssl    0:00 /usr/bin/dockerd -H unix://
 2796 ?        Ssl    0:00 containerd --config /var/run/docker/containerd/containerd.toml --log-level info
 2942 pts/0    S+     0:00 grep --color=auto docker
[vagrant@localhost ~]$
```
### 查看验证启动成功
