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
