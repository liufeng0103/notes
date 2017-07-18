## tomcat
### 安装tomcat
1. 使用yum安装tomcat  
yum install tomcat tomcat-webapps tomcat-admin-webapps
2. 启动  
service tomcat start
service tomcat restart
service tomcat stop

### tomcat目录
- centos7自动安装的tomcat安装路径
/usr/share/tomcat
- Tomcat的部署包存放的路径
/var/lib/tomcat/webapps/
- Tomcat的配置文件路径
/etc/tomcat/
- Tomcat的Jar包存放的路径
/usr/share/java/tomcat
- Tomcat中的Servlet API包存放的路径
/usr/share/java/apache-tomcat-apis/

### tomcat日志
Tomcat的log目录/var/log/tomcat
有3种log文件:
- catalina.yyyy-mm-dd.log
错误log信息
- catalina.out
- localhost_access_log.yyyy-mm-dd.txt
请求的资源信息以及返回状态码


### tomcat7管理页面用户配置
- 修改tomcat配置文件路径下的server-user.xml
<role rolename="admin-gui"/>
<role rolename="manager-gui"/>
<user username="admin" password="" roles="admin-gui,manager-gui"/>

### 添加一个端口的映射
tomcat默认访问端口是8080.现在我想做到当用户访问80端口的时候就能访问到tomcat了.
只需要在root用户下执行命令,把80端口的tcp转发到8080端口
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080
删除转发规则
iptables -t nat -F

### 修改tomcat监听端口
找到tomcat的主目录，打开conf文件夹，找到并打开server.xml文件，在<Service></Service>标签中添加：
<Connector port="9090" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />

### tomcat启用gzip
打开conf/server.xml文件, 要使用gzip压缩功能，可以在Connector实例中加上如下属性:   
1. compression="on" 打开压缩功能  
2. compressionMinSize="2048" 启用压缩的输出内容大小，这里面默认为2KB  
3. noCompressionUserAgents="gozilla, traviata" 对于以下的浏览器，不启用压缩&<60;  
4. compressableMimeType="text/html,text/xml" 压缩类型  
<Connector
port="8080"               maxHttpHeaderSize="8192"
               maxThreads="150" minSpareThreads="25" maxSpareThreads="75"
               enableLookups="false" redirectPort="8443" acceptCount="100"
               connectionTimeout="20000" disableUploadTimeout="true"
      compression="on"
compressionMinSize="2048"
noCompressionUserAgents="gozilla,traviata"
compressableMimeType="text/html,text/xml,text/javascript,text/css,text/plain,application/javascript,application/json" />
