---
title: VPS部署Ghost 
author: fengxw
---

本文基础环境为DigitalOcean Droplet下的centos
---

### 安装Ghost

ghost的安装方法，请点击[这里](http://support.ghost.org/installing-ghost-linux/)。本文将ghost安装在nginx默认根目录 /home/wwwroot/ghost

### 让 Ghost 一直运行

前面提到的启动 Ghost 使用 npm start 命令。这是一个在开发模式下启动和测试的不错的选择，但是通过这种命令行启动的方式有个缺点，即当你关闭终端窗口或者从 SSH 断开连接时，Ghost 就停止了。为了防止 Ghost 停止工作，有多种方式解决这个问题。本文采用pm2。

```
npm install pm2 -g //安装pm2
NODE_ENV=production pm2 start index.js --name "ghost" //将production写入环境变量，将服务命名为ghost
pm2 startup centos pm2 save //随系统一块启动
pm2 kill ghost //杀掉所有名为ghost的进程
pm2 start ghost
pm2 stop ghost
pm2 status ghost 查看ghost进程状态
```

### 配置 Ghost 域名

如果你已经让 Ghost 在后台运行了，你也可以设置一个代理服务器让你的博客可以使用域名访问。以下的示例使用 Nginx 作为你的Web服务器。

### 安装 nginx

```
$ sudo apt-get install nginx
```

这个命令将会安装nginx并且设定好所有必需的目录和基础配置。

### 配置你的站点

在 /usr/local/nginx/conf/vhost 创建一个 ghost.conf 文件 使用文本编辑器打开这个文件 (e.g. sudo vim /usr/local/nginx/conf/vhost/ghost.conf) 把以下内容复制进这个文件

```
server {
listen 80;
server_name example.com;
location / {
    proxy_set_header   X-Real-IP $remote_addr;
    proxy_set_header   Host      $http_host;
    proxy_pass         http://127.0.0.1:2368;
    }
access_log /home/wwwlogs/access.example.com.log  access;
}
```

将 server_name 的值改为你的域名

重启 nginx

```
$ sudo service nginx restart
```

### 更改默认数据库

ghost默认数据库为sqlite3，我们可以替其换成更安全的mysql来存储数据。

## 安装 mysql
```
yum install -y mysql-server mysql mysql-devel
```
在mysql内新建一个名为ghost的数据库

在ghost根目录找到config.js,将production下的database替换成以下内容：

```
  database: {
    client: 'mysql',
    connection: {
        host: 'localhost',
        user: 'root',
        password: 'your password',
        database: 'ghost',
        charset: 'utf8'
    },
```
tips:
前面提到的nginx和mysql都可以利用lnmp包一键安装，可以点击这里查看

### 参考文章
[http://docs.ghost.org/zh/installation/deploy/#开始-ghost-之旅-](http://docs.ghost.org/zh/installation/deploy/#开始-ghost-之旅-)
