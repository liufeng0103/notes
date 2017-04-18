## WebSphere Application Server(WAS)
### 常用(rhel7)
- 安装目录 /opt/ibm/WebSphere/AppServer
- 启动was sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/startServer.sh server1 -profileName AppSrv01
- 关闭was sudo /opt/ibm/WebSphere/AppServer/profiles/AppSrv01/bin/stopServer.sh server1 -profileName AppSrv01 -username xxx -password xxx
- was控制台 https://localhost:9043/ibm/console/login.do
- 查看所有profiles sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -listProfiles
- 删除profile sudo /opt/ibm/WebSphere/AppServer/bin/manageprofiles.sh -delete -profileName AppSrv01