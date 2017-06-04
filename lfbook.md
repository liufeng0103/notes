
## Windows脚本

[Windows批处理(cmd/bat)使用小记](https://www.zybuluo.com/yangfch3/note/338252)

@echo off 从本行开始关闭回显。一般批处理第一行都是这个

title 设置cmd窗口的标题

rem 和 ::
注释命令
注释行不执行操作

pause
暂停命令

## tomcat在接收中文参数的URL时的乱码问题
当访问带中文参数的url，或者提交get方法到后台包含中文参数的时候，可能后台接收到的是乱码，解决：
1. 修改tomcat目录下的service.xml文件
```xml
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" URIEncoding="UTF-8" />
```
加上URIEncoding="UTF-8"的编码属性这样配置后，tomcat接收url请求后就会以utf-8解码传递的中文参数，也就能解决乱码问题
