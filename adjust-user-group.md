添加用户到docker分组
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
上面的操作仍然不能直接运行命令，这是需要推出，重新登陆即可。
