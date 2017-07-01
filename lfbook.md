
## Windows脚本

[Windows批处理(cmd/bat)使用小记](https://www.zybuluo.com/yangfch3/note/338252)

## tomcat在接收中文参数的URL时的乱码问题
当访问带中文参数的url，或者提交get方法到后台包含中文参数的时候，可能后台接收到的是乱码，解决：
1. 修改tomcat目录下的service.xml文件
```xml
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" URIEncoding="UTF-8" />
```
加上URIEncoding="UTF-8"的编码属性这样配置后，tomcat接收url请求后就会以utf-8解码传递的中文参数，也就能解决乱码问题

# SpringBoot

idea快捷键
- Ctrl+Alt+L 格式化代码
- Ctrl+Enter 导入包，自动修正
- Ctrl+Alt+O 优化导入的类和包
- Shift+F6 重命名
- Alt+Insert 可以生成构造器/Getter/Setter等
- Ctrl+Shift+T 创建或跳转到测试类
- Ctrl+Alt+left 返回上次浏览

Idea有自带的Http调试工具，快捷键Ctrl+Shift+A，然后输入REST Client
火狐浏览器可以用HttpRequester插件

maven打包跳过测试
mvn clean package -Dmaven.test.skip=true

[Restful API 的设计规范](http://novoland.github.io/%E8%AE%BE%E8%AE%A1/2015/08/17/Restful%20API%20%E7%9A%84%E8%AE%BE%E8%AE%A1%E8%A7%84%E8%8C%83.html)








