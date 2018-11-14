栗子1：
```
[vagrant@localhost sayhi]$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[vagrant@localhost sayhi]$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                        PORTS               NAMES
544ab3ccd7cd        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          festive_meninsky
b70dadb3148d        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          ecstatic_kare
d9efb6e0a7db        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          cocky_mccarthy
07ca244711a5        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          epic_meitner
68fb16adbd85        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          nostalgic_jackson
788d2b733964        ubuntu              "/bin/bash"         13 minutes ago      Exited (127) 12 minutes ago                       wizardly_northcutt
961381b9706a        ubuntu              "/bin/bash"         14 minutes ago      Exited (0) 14 minutes ago                         jovial_wu
a6ba52aa7056        ubuntu              "/bin/bash"         15 minutes ago      Exited (0) 15 minutes ago                         nostalgic_thompson
7e143e597006        yubiaohyb/sayhi     "/sayhi"            16 minutes ago      Exited (4) 16 minutes ago                         adoring_knuth
de1b83225feb        yubiaohyb/sayhi     "/sayhi"            42 minutes ago      Exited (4) 42 minutes ago                         affectionate_archimedes
9cd71337bed6        hello-world         "/hello"            3 hours ago         Exited (0) 3 hours ago                            relaxed_blackburn
[vagrant@localhost sayhi]$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                        PORTS               NAMES
544ab3ccd7cd        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          festive_meninsky
b70dadb3148d        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          ecstatic_kare
d9efb6e0a7db        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          cocky_mccarthy
07ca244711a5        yubiaohyb/sayhi     "/sayhi"            4 minutes ago       Exited (4) 4 minutes ago                          epic_meitner
68fb16adbd85        yubiaohyb/sayhi     "/sayhi"            5 minutes ago       Exited (4) 4 minutes ago                          nostalgic_jackson
788d2b733964        ubuntu              "/bin/bash"         13 minutes ago      Exited (127) 13 minutes ago                       wizardly_northcutt
961381b9706a        ubuntu              "/bin/bash"         14 minutes ago      Exited (0) 14 minutes ago                         jovial_wu
a6ba52aa7056        ubuntu              "/bin/bash"         15 minutes ago      Exited (0) 15 minutes ago                         nostalgic_thompson
7e143e597006        yubiaohyb/sayhi     "/sayhi"            16 minutes ago      Exited (4) 16 minutes ago                         adoring_knuth
de1b83225feb        yubiaohyb/sayhi     "/sayhi"            42 minutes ago      Exited (4) 42 minutes ago                         affectionate_archimedes
9cd71337bed6        hello-world         "/hello"            3 hours ago         Exited (0) 3 hours ago                            relaxed_blackburn
[vagrant@localhost sayhi]$
```
栗子2：
```
[vagrant@localhost sayhi]$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                         PORTS               NAMES
544ab3ccd7cd        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          festive_meninsky
b70dadb3148d        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          ecstatic_kare
d9efb6e0a7db        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          cocky_mccarthy
07ca244711a5        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          epic_meitner
68fb16adbd85        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          nostalgic_jackson
788d2b733964        ubuntu              "/bin/bash"         21 minutes ago      Exited (127) 20 minutes ago                        wizardly_northcutt
961381b9706a        ubuntu              "/bin/bash"         21 minutes ago      Exited (0) 21 minutes ago                          jovial_wu
a6ba52aa7056        ubuntu              "/bin/bash"         22 minutes ago      Exited (0) 22 minutes ago                          nostalgic_thompson
7e143e597006        yubiaohyb/sayhi     "/sayhi"            23 minutes ago      Exited (4) 23 minutes ago                          adoring_knuth
de1b83225feb        yubiaohyb/sayhi     "/sayhi"            About an hour ago   Exited (4) About an hour ago                       affectionate_archimedes
9cd71337bed6        hello-world         "/hello"            3 hours ago         Exited (0) 3 hours ago                             relaxed_blackburn
[vagrant@localhost sayhi]$ docker container rm 54
54
[vagrant@localhost sayhi]$ docker container ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                         PORTS               NAMES
b70dadb3148d        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          ecstatic_kare
d9efb6e0a7db        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          cocky_mccarthy
07ca244711a5        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          epic_meitner
68fb16adbd85        yubiaohyb/sayhi     "/sayhi"            12 minutes ago      Exited (4) 12 minutes ago                          nostalgic_jackson
788d2b733964        ubuntu              "/bin/bash"         21 minutes ago      Exited (127) 20 minutes ago                        wizardly_northcutt
961381b9706a        ubuntu              "/bin/bash"         22 minutes ago      Exited (0) 22 minutes ago                          jovial_wu
a6ba52aa7056        ubuntu              "/bin/bash"         22 minutes ago      Exited (0) 22 minutes ago                          nostalgic_thompson
7e143e597006        yubiaohyb/sayhi     "/sayhi"            23 minutes ago      Exited (4) 23 minutes ago                          adoring_knuth
de1b83225feb        yubiaohyb/sayhi     "/sayhi"            About an hour ago   Exited (4) About an hour ago                       affectionate_archimedes
9cd71337bed6        hello-world         "/hello"            3 hours ago         Exited (0) 3 hours ago                             relaxed_blackburn
[vagrant@localhost sayhi]$
[vagrant@localhost sayhi]$ docker rm b7
b7
[vagrant@localhost sayhi]$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                         PORTS               NAMES
d9efb6e0a7db        yubiaohyb/sayhi     "/sayhi"            13 minutes ago      Exited (4) 13 minutes ago                          cocky_mccarthy
07ca244711a5        yubiaohyb/sayhi     "/sayhi"            13 minutes ago      Exited (4) 13 minutes ago                          epic_meitner
68fb16adbd85        yubiaohyb/sayhi     "/sayhi"            13 minutes ago      Exited (4) 13 minutes ago                          nostalgic_jackson
788d2b733964        ubuntu              "/bin/bash"         22 minutes ago      Exited (127) 22 minutes ago                        wizardly_northcutt
961381b9706a        ubuntu              "/bin/bash"         23 minutes ago      Exited (0) 23 minutes ago                          jovial_wu
a6ba52aa7056        ubuntu              "/bin/bash"         24 minutes ago      Exited (0) 24 minutes ago                          nostalgic_thompson
7e143e597006        yubiaohyb/sayhi     "/sayhi"            25 minutes ago      Exited (4) 25 minutes ago                          adoring_knuth
de1b83225feb        yubiaohyb/sayhi     "/sayhi"            About an hour ago   Exited (4) About an hour ago                       affectionate_archimedes
9cd71337bed6        hello-world         "/hello"            3 hours ago         Exited (0) 3 hours ago                             relaxed_blackburn
[vagrant@localhost sayhi]$
```
栗子3：
```
[vagrant@localhost sayhi]$ docker container ls -aq
d9efb6e0a7db
07ca244711a5
68fb16adbd85
788d2b733964
961381b9706a
a6ba52aa7056
7e143e597006
de1b83225feb
9cd71337bed6
[vagrant@localhost sayhi]$ docker container ls -a | awk {'print$1'}
CONTAINER
d9efb6e0a7db
07ca244711a5
68fb16adbd85
788d2b733964
961381b9706a
a6ba52aa7056
7e143e597006
de1b83225feb
9cd71337bed6
[vagrant@localhost sayhi]$ docker rm $(docker container ls -aq)
d9efb6e0a7db
07ca244711a5
68fb16adbd85
788d2b733964
961381b9706a
a6ba52aa7056
7e143e597006
de1b83225feb
9cd71337bed6
[vagrant@localhost sayhi]$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[vagrant@localhost sayhi]$
```
栗子4：
```
[vagrant@localhost sayhi]$ docker ps -f "status=exited"
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
51dcc9d46114        yubiaohyb/sayhi     "/sayhi"            31 seconds ago      Exited (4) 30 seconds ago                       gallant_mirzakhani
faee9a88de31        yubiaohyb/sayhi     "/sayhi"            32 seconds ago      Exited (4) 31 seconds ago                       unruffled_tesla
5054962f32b0        yubiaohyb/sayhi     "/sayhi"            33 seconds ago      Exited (4) 32 seconds ago                       relaxed_villani
cdb8bde87314        yubiaohyb/sayhi     "/sayhi"            34 seconds ago      Exited (4) 33 seconds ago                       practical_johnson
97e5739082b5        yubiaohyb/sayhi     "/sayhi"            36 seconds ago      Exited (4) 34 seconds ago                       infallible_fermi
[vagrant@localhost sayhi]$ docker ps -f "status=exited" -q
51dcc9d46114
faee9a88de31
5054962f32b0
cdb8bde87314
97e5739082b5
[vagrant@localhost sayhi]$ docker rm $(docker ps -f "status=exited" -q)
51dcc9d46114
faee9a88de31
5054962f32b0
cdb8bde87314
97e5739082b5
[vagrant@localhost sayhi]$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[vagrant@localhost sayhi]$
```
构建docker镜像
```
[vagrant@localhost sayhi]$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS
         NAMES
▒4fc0c07c4d6        centos              "/bin/bash"         4 minutes ago       Exited (0) 8 seconds ago
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
