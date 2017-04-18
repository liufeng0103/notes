# Linux
## 常用
- 仓库配置目录 /etc/yum.repos.d
- 修改目录的用户和用户组 sudo chown user:group -R directory
- 启动栏app /usr/share/applications
## 软件安装
- 查看rpm包安装路径 rpm -qpl xxx.rpm
- 查看yum安装的软件路径 1. 查看软件完整的名称 rpm -qa|grep tomcat 2. 查看路径 rpm -ql xxx