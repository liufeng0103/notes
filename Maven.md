# Maven

## 安装
CentOS直接通过yum install maven安装

配置文件路径 /etc/maven/settings.xml 设置阿里云镜像
```xml
<mirror>
  <id>alimaven</id>
  <name>aliyun maven</name>
  <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
  <mirrorOf>central</mirrorOf>        
</mirror>
```

打包，不运行测试
mvn clean package -Dmaven.test.skip=true

获取所有依赖jar
mvn dependency:copy-dependencies
