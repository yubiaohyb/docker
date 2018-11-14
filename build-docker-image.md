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
