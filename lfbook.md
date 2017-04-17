# lfbook
把平时常用的和一些学习笔记记录下来，方便以后查看

## Linux
### 常用
- 仓库配置目录 /etc/yum.repos.d
- 修改目录的用户和用户组 sudo chown <user>:<group> -R <directory>


## WebSphere Application Server(WAS)
### 常用(rhel7)
- 安装目录 /opt/ibm/WebSphere/AppServer
- 启动was sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/startServer.sh server1 -profileName AppSrv01
- 关闭was sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/stopServer.sh server1 -profileName AppSrv01 -username xxx -password xxx
- was控制台 https://localhost:9043/ibm/console/login.do
- was profile管理工具 /opt/ibm/WebSphere/AppServer/bin/ProfileManagement/pmt.sh
- 查看所有profiles sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -listProfiles
- 删除profile sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -delete -profileName AppSrv01

