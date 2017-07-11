# [Docker](https://www.docker.com)

- [第一个docker化的java应用](http://www.imooc.com/learn/824)
- [docker常用管理命令](http://seanlook.com/2014/10/31/docker-command-best-use-1/)
- [MySQL 官方Docker镜像的使用](https://itbilu.com/linux/docker/EyP7QP86M.html)
- [在windows10里使用docker](http://www.59m59s.com/blog/zai-windows10li-shi-yong-docker/)
- [Docker学习笔记（容器篇）](http://www.jianshu.com/p/8b46e98e596c)

## 仓库
负责分发镜像
hub.docker.com 速度慢  
c.163.com  
http://hub.daocloud.io/  

2014发布Docker 1.0

LXC Linux支持的轻量级的容器虚拟化技术

docker compose多容器管理工具

## CentOS7安装Docker
参考[官方教程](https://docs.docker.com/engine/installation/linux/docker-ce/centos/)

### 安装repository
1. 安装需要的包  
sudo yum install yum-utils device-mapper-persistent-data lvm2
2. 安装stable repository  
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
3. 可选操作，启用edge和testing repositories，默认关闭  
sudo yum-config-manager --enable docker-ce-edge  
sudo yum-config-manager --enable docker-ce-testing

### 安装Docker CE
1. 更新yum包索引  
sudo yum makecache fast
2. 安装最新Docker CE  
sudo yum install docker-ce
3. 在生产环境，指定版本安装，而不是每次安装最新版本，通过一下命令查看所有docker版本  
yum list docker-ce.x86_64  --showduplicates | sort -r  
sudo yum install docker-ce-<VERSION>
4. 启动Docker  
sudo systemctl start docker  
设置开机启动  
sudo systemctl enable docker
5. 运行hello-image镜像验证docker安装成功  
sudo docker run hello-world

### 卸载Docker CE
sudo yum remove docker-ce
sudo rm -rf /var/lib/docker

## 启用/关闭hyper-v
1. 已管理员运行命令行
2. 执行以下命令关闭或启用
bcdedit /set hypervisorlaunchtype off
bcdedit /set hypervisorlaunchtype auto
3. 重启
bcdedit /copy {current} /d “Windows10 no Hyper-V

bcdedit /set {508730cd-5f3d-11e7-9ff3-bc5ff47729fc} hypervisorlaunchtype OFF
解决的问题
1. 统一环境
2. 服务器资源合理分配，隔离
3. 快速扩展弹性伸缩

- Docker镜像
联合文件系统unfs



自己搭建仓库

- 容器

docker version
service docker start 启动服务

查看docker进程
docker ps
docker ps -a

启动关闭容器
docker start/stop <container id>

删除容器
docker rm <container id>

修改image名
docker tag imageid name:tag

## MySQL
简单启动MySQL实例
docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:latest

This image can also be used as a client for non-Docker or remote MySQL instances:
docker run -it --rm mysql mysql -hlocalhost -uroot -p

The following command line will give you a bash shell inside your mysql container
docker exec -it mysql bash

```
# 需要指定密码，否则容器启动失败
docker run --name bnade-mysql -v J:/data/mysql:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:latest
docker exec -it bnade-mysql bash
参考
我跑 Docker 一般是建一个 subnet

每个服务分配一个内网 ip

直接用内网 Ip+端口访问

以 mysql 为例，大概是这样

docker run --network=vps --ip=10.1.1.2 --name mysql -v /dockers/mysql/data:/var/lib/mysql -v /dockers/mysql/conf:/etc/mysql -e MYSQL_ROOT_PASSWORD=123456 -d --restart always mysql
```

## Redis
docker runs -p 6379:6379 --name some-redis -d redis
