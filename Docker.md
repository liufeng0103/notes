# Docker

官网 http://www.docker.com

网易蜂巢的docker仓库 http://c.163.com

## 常用
```sh
# 查看本地镜像
docker images

# 下载镜像到本地仓库
docker pull xxxx

# 运行镜像
docker run

# 查看容器进程
docker ps

# 关闭容器
docker stop 容器id
```

Redis
安装
docker pull hub.c.163.com/library/redis:latest
启动一个redis实例
-d, --detach                                Run container in background and print container ID
docker run --name some-redis -d hub.c.163.com/library/redis
-i, --interactive                           Keep STDIN open even if not attached
-t, --tty                                   Allocate a pseudo-TTY
--link list                             Add link to another container (default [])
--rm                                    Automatically remove the container when it exits


docker run -it --link some-redis:redis --rm hub.c.163.com/library/redis redis-cli -h redis -p 6379

### CentOS7安装Docker

本来打算通过yum安装，后来发现网速太满，每次都安装超时，直接下载rpm包安装
[安装介绍](https://docs.docker.com/engine/installation/linux/centos/)
[rpm包下载地址](https://download.docker.com/linux/centos/7/x86_64/stable/Packages/)
由于使用sudo安装， 使用docker version是发现包Got permission denied while trying to connect to the Docker daemon socket这个错误，参考一下文章添加docker组
[免sudo使用docker命令](http://blog.csdn.net/baidu_36342103/article/details/69357438)
