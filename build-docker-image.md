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
