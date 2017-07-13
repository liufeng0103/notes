#　Nginx

- [Nginx负载均衡配置](http://blog.csdn.net/xyang81/article/details/51702900)

启动 systemctl start nginx

平滑加载  
sudo systemctl reload nginx  
nginx -s reload

配置文件 /etc/nginx

日志
/var/log/nginx/error.log
/var/log/nginx/access.log

## 配置Let's Encrypt的SSL证书
参考[certbot文档](https://certbot.eff.org)  
[How to Install Let’s Encrypt on Nginx](https://www.upcloud.com/support/install-lets-encrypt-nginx/)

使用certbot下载证书之前，先配置nginx中的server域名与要下载的证书域名一致  
在nginx配置中添加localtion /.well-known用于域名验证

问题：  
1. CentOS7按照教程sudo certbot --nginx运行出现以下错误  
ImportError: 'pyOpenSSL' module missing required functionality. Try upgrading to v0.14 or newer.  
解决：自己手动下载安装了新的pyOpenSSL rpm包
2. sudo certbot --nginx提示超时，阿里云设置安全组 开放443端口

直接使用下面命令下载安装整数
sudo certbot certonly --webroot -w /usr/share/nginx/html -d api.bnade.com

查看当前证书 certbot certificates

## Nginx
### 安装
- [https://www.nginx.com/resources/wiki/start/topics/tutorials/install/](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/)
- 查看yum的nginx信息
`yum info nginx`
- 安装完毕看看都生成了哪些文件，配置文件都放在哪里
`rpm -ql nginx`

### 配置文件
1. 由上面的步骤，我们看到配置文件放置在/etc/nginx/目录下:
- 主要配置文件：/etc/nginx/nginx.conf
- 扩展配置文件：`/etc/nginx/conf.d/*.conf`

### nginx的权限问题(13: Permission denied)解决办法
1. 修改配置文件/etc/nginx/nginx.conf
2. 改成user root
3. 停止nginx -s stop
4. 重启nginx -c  nginx.conf
5. nginx -s reload #平滑重启
重启 systemctl restart nginx
kill掉80端口的程序 sudo fuser -k 80/tcp

### log
- 路径
/var/log/nginx
tail -f /var/log/nginx/access.log
tail -f /var/log/nginx/error.log

### gzip压缩
[http://www.php100.com/html/program/nginx/2013/0905/5526.html](http://www.php100.com/html/program/nginx/2013/0905/5526.html)

### goaccess
- 配置文件  
/etc/goaccess.conf
/usr/local/etc/goaccess.conf
/etc/letsencrypt/live/bnade.com/cert.pem
/etc/letsencrypt/live/bnade.com/privkey.pem
log-format %h %^[%d:%t %^] "%r" %s %b "%R" "%u" %^ %^ %T
log_format access '$remote_addr - $remote_user [$time_local] "$request" $status $body_bytes_sent "$http_referer" "$http_user_agent" $http_x_forwarded_for $request_time $upstream_response_time';
goaccess -f /var/log/nginx/access.log -a -d -o /home/lf/report.html --max-items=50 --date-spec=hr --hour-spec=min --html-prefs='{"theme":"bright","perPage":7}' --enable-panel=HOSTS --enable-panel=REFERRERS --enable-panel=REMOTE_USER --real-time-html --ws-url=wss://www.bnade.com --ssl-cert=/etc/letsencrypt/live/bnade.com/cert.pem --ssl-key=/etc/letsencrypt/live/bnade.com/privkey.pem

goaccess -f /var/log/nginx/access.log -a -d -o /home/lf/report.html --max-items=50 --date-spec=hr --hour-spec=min --html-prefs='{"theme":"bright","perPage":7}' --enable-panel=HOSTS --enable-panel=REFERRERS --enable-panel=REMOTE_USER

ln /home/lf/report.html /var/lib/tomcat/webapps/ROOT/report.html



--hour-spec=<hour|min>
time distribution panel使用
--date-spec=hr
