# Linux
## 常用
- 仓库配置目录 /etc/yum.repos.d
- 修改目录的用户和用户组 sudo chown user:group -R directory
- 启动栏app /usr/share/applications

## 软件安装
- 查看rpm包安装路径 rpm -qpl xxx.rpm
- 查看yum安装的软件路径 1. 查看软件完整的名称 rpm -qa|grep tomcat 2. 查看路径 rpm -ql xxx

### rpm
rpm -i 需要安装的包文件名

## iptables
- 查看定义规则的详细信息  
iptables -L -n -v
- 开发3306端口  
iptables -I INPUT -p tcp --dport 3306 -j ACCEPT
- 只允许指定ip连接指定端口
iptables -I INPUT -p tcp --dport 8080 -j DROP
iptables -I INPUT -s 127.0.0.1 -p tcp --dport 8080 -j ACCEPT

## 用户管理
创建用户 useradd luis

设置密码 passwd luis

删除用户 userdel luis

切换用户 su luis

### 用户添加sudo权限
1. 使用root账户使用以下命令为sudoers添加写权限 chmod u+w /etc/sudoers
2. 添加 <user> ALL=(ALL) ALL
3. 去掉文件写权限 chmod u-w /etc/sudoers
