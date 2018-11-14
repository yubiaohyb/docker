构建docker镜像
```
[vagrant@localhost sayhi]$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS
         NAMES
4fc0c07c4d6        centos              "/bin/bash"         4 minutes ago       Exited (0) 8 seconds ago
         compassionate_bell
b51e3e022238        centos              "-it"               4 minutes ago       Created
         youthful_visvesvaraya
204c0027f71d        centos              "/bin/bash"         4 minutes ago       Exited (0) 4 minutes ago
         reverent_bhaskara
88616d419f07        centos              "/bin/bash"         5 minutes ago       Exited (0) 5 minutes ago
         condescending_dhawan
fedcea508e65        ubuntu              "/bin/bash"         7 minutes ago       Exited (127) 6 minutes ago
         flamboyant_heisenberg
d61cad31ffb8        ubuntu              "/bin/bash"         7 minutes ago       Exited (0) 7 minutes ago
         reverent_leakey
[vagrant@localhost sayhi]$ docker commit
"docker commit" requires at least 1 and at most 2 arguments.
See 'docker commit --help'.

Usage:  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

Create a new image from a container's changes
[vagrant@localhost sayhi]$ docker commit compassionate_bell yubiaohyb/centos-vim:init
sha256:c7e5473d14f3e41a736db2fb7974ae017decc0659b92654e34da07c8f6941933
[vagrant@localhost sayhi]$ docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
yubiaohyb/centos-vim   init                c7e5473d14f3        15 seconds ago      355MB
yubiaohyb/sayhi        latest              2b84f6b4e970        About an hour ago   861kB
ubuntu                 14.04               f216cfb59484        3 weeks ago         188MB
ubuntu                 latest              ea4c82dcd15a        3 weeks ago         85.8MB
centos                 latest              75835a67d134        5 weeks ago         200MB
hello-world            latest              4ab4c602aa5e        2 months ago        1.84kB
[vagrant@localhost sayhi]$ docker run yubiaohyb/centos-vim
Unable to find image 'yubiaohyb/centos-vim:latest' locally
docker: Error response from daemon: pull access denied for yubiaohyb/centos-vim, repository does not exist or may requir
e 'docker login'.
See 'docker run --help'.
[vagrant@localhost sayhi]$ docker run
"docker run" requires at least 1 argument.
See 'docker run --help'.

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container
[vagrant@localhost sayhi]$ docker run c7e5473d14f3
[vagrant@localhost sayhi]$ docker run -it  c7e5473d14f3
```

对比原镜像与新构建的镜像：
```
[vagrant@localhost sayhi]$ docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
yubiaohyb/centos-vim   init                c7e5473d14f3        13 minutes ago      355MB
yubiaohyb/sayhi        latest              2b84f6b4e970        2 hours ago         861kB
ubuntu                 14.04               f216cfb59484        3 weeks ago         188MB
ubuntu                 latest              ea4c82dcd15a        3 weeks ago         85.8MB
centos                 latest              75835a67d134        5 weeks ago         200MB
hello-world            latest              4ab4c602aa5e        2 months ago        1.84kB
[vagrant@localhost sayhi]$ docker history 75835a67d134
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
75835a67d134        5 weeks ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>           5 weeks ago         /bin/sh -c #(nop)  LABEL org.label-schema.sc…   0B
<missing>           5 weeks ago         /bin/sh -c #(nop) ADD file:fbe9badfd2790f074…   200MB
[vagrant@localhost sayhi]$ docker history c7e5473d14f3
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
c7e5473d14f3        14 minutes ago      /bin/bash                                       155MB
75835a67d134        5 weeks ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>           5 weeks ago         /bin/sh -c #(nop)  LABEL org.label-schema.sc…   0B
<missing>           5 weeks ago         /bin/sh -c #(nop) ADD file:fbe9badfd2790f074…   200MB
[vagrant@localhost sayhi]$
```
从Dockerfile构建：
```
[vagrant@localhost centos-vim-new]$ vi Dockerfile
[vagrant@localhost centos-vim-new]$ more D
D: No such file or directory
[vagrant@localhost centos-vim-new]$ more Dockerfile
FROM centos
RUN yum install -y vim
[vagrant@localhost centos-vim-new]$ ls
Dockerfile
[vagrant@localhost centos-vim-new]$
[vagrant@localhost centos-vim-new]$
[vagrant@localhost centos-vim-new]$ docker build -t yubiaohyb/centos-vim-new .
Sending build context to Docker daemon  2.048kB
Step 1/2 : FROM centos
 ---> 75835a67d134
Step 2/2 : RUN yum install -y vim
 ---> Running in 4ee89b7f23bd
Loaded plugins: fastestmirror, ovl
Determining fastest mirrors
 * base: mirrors.cn99.com
 * extras: mirrors.163.com
 * updates: mirrors.163.com
http://mirrors.huaweicloud.com/centos/7.5.1804/os/x86_64/repodata/03d0a660eb33174331aee3e077e11d4c017412d761b7f2eaa8555e7898e701e0-primary.sqlite.bz2: [Errno 12] Timeout on http://113.215.26.196/files/52490000000016B0/mirror.bit.edu.cn/centos/7.5.1804/os/x86_64/repodata/03d0a660eb33174331aee3e077e11d4c017412d761b7f2eaa8555e7898e701e0-primary.sqlite.bz2: (28, 'Connection timed out after 30961 milliseconds')
Trying other mirror.
Resolving Dependencies
--> Running transaction check
---> Package vim-enhanced.x86_64 2:7.4.160-4.el7 will be installed
--> Processing Dependency: vim-common = 2:7.4.160-4.el7 for package: 2:vim-enhanced-7.4.160-4.el7.x86_64
--> Processing Dependency: which for package: 2:vim-enhanced-7.4.160-4.el7.x86_64
...
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                     Arch        Version                Repository
                                                                           Size
================================================================================
Installing:
 vim-enhanced                x86_64      2:7.4.160-4.el7        base      1.0 M
Installing for dependencies:
 gpm-libs                    x86_64      1.20.7-5.el7           base       32 k
 ...
 which                       x86_64      2.20-7.el7             base       41 k

Transaction Summary
================================================================================
Install  1 Package (+32 Dependent packages)

Total download size: 19 M
Installed size: 63 M
Downloading packages:
warning: /var/cache/yum/x86_64/7/base/packages/gpm-libs-1.20.7-5.el7.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID f4a80eb5: NOKEY
Public key for gpm-libs-1.20.7-5.el7.x86_64.rpm is not installed
--------------------------------------------------------------------------------
Total                                              1.3 MB/s |  19 MB  00:14
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Importing GPG key 0xF4A80EB5:
 Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 Package    : centos-release-7-5.1804.4.el7.centos.x86_64 (@Updates)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 2:vim-filesystem-7.4.160-4.el7.x86_64                       1/33
  Installing : 2:vim-common-7.4.160-4.el7.x86_64                           2/33
  ...
  Verifying  : 2:vim-common-7.4.160-4.el7.x86_64                          33/33

Installed:
  vim-enhanced.x86_64 2:7.4.160-4.el7

Dependency Installed:
  gpm-libs.x86_64 0:1.20.7-5.el7
  ...
  perl-threads-shared.x86_64 0:1.43-6.el7
  vim-common.x86_64 2:7.4.160-4.el7
  vim-filesystem.x86_64 2:7.4.160-4.el7
  which.x86_64 0:2.20-7.el7

Complete!
Removing intermediate container 4ee89b7f23bd
 ---> 1c9ef8ec94a9
Successfully built 1c9ef8ec94a9
Successfully tagged yubiaohyb/centos-vim-new:latest
[vagrant@localhost centos-vim-new]$
```
