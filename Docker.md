# [Docker](https://www.docker.com)

[第一个docker化的java应用](http://www.imooc.com/learn/824)
[docker常用管理命令](http://seanlook.com/2014/10/31/docker-command-best-use-1/)
[MySQL 官方Docker镜像的使用](https://itbilu.com/linux/docker/EyP7QP86M.html)

2014发布Docker 1.0

LXC Linux支持的轻量级的容器虚拟化技术

解决的问题
1. 统一环境
2. 服务器资源合理分配，隔离
3. 快速扩展弹性伸缩

- Docker镜像
联合文件系统unfs

- 仓库
负责分发镜像
hub.docker.com 速度慢
c.163.com

自己搭建仓库

- 容器

docker version
service docker start 启动服务

查看docker进程
docker ps

启动关闭容器
docker start/stop <container id>

删除容器
docker rm <container id>

修改image名
docker tag imageid name:tag

## MySQL
简单启动MySQL实例
docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:latest

This image can also be used as a client for non-Docker or remote MySQL instances:
docker run -it --rm mysql mysql -hlocalhost -uroot -p

The following command line will give you a bash shell inside your mysql container
docker exec -it mysql bash