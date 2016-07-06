---
title: Docker搭建开发环境   ------Windows and Mac
author: fengxw
---

在windows和mac上以docker为基础搭建开发环境

---

### Docker安装
* 登录daocloud.io下载docker toolbox工具包并安装
* 运行Docker Quickerstart Terminal快捷方式启动虚拟机。*第一次启动，会自动下载最新版本的boot2docker镜像，并生成名为default的虚拟机*
* 运行命令`docker-machine ssh default`进入docker虚拟机

 ***tips:*** 虚拟机会自动映射宿主机的个人文件目录
    - windows: c:\Users\feng ---> /c/Users/feng 
    - mac: /Users/feng ---> /Users/feng
* `sudo -i` 登录root账户，安装docker-compose。

        # curl -L get.daocloud.io/docker/compose/releases/download/1.4.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
        # chmod +x /usr/local/bin/docker-compose
*由于docker虚拟机只会持久化容器，虚拟机内的操作如果需要保留，需要保存或生成snapshot，否则关闭虚拟机后会丢失。*
* `exit` 退出root账户，安装daocloud加速器（国内用户）

        $ curl -sSL https://get.daocloud.io/daomonit/install.sh | sh -s a702bb3c4b4f7bec72df4776fa2c54effb76a3f1
至此，docker基本运行环境搭建完毕。

### 搭建开发环境
下面以php的web开发环境为例，搭建docker下的开发环境

* 在宿主机的映射的共享目录中创建Dockerfiles文件夹，保存事先准备好的dockerfile文件。至于如何配置dockerfile文件，可以参考[dockerfile文件配置](http://)。

        docker run -d -p 8086:80 nginx //左边是外部端口，右边是容器内部暴露端口
* 使用docker-compose 管理多个容器
  * 在Dockerfiles文件夹中创建dockerfile.yml文件，并配置好需要被管理的容器，配置方法可以参考[这里]()。
  * 定位到Dockerfiles文件夹内，运行`docker-compose up`，拉取镜像；若配置无误，该命令会自动初始化，并启动镜像。
  * 也可以使用命令`docker-compose build`拉取，`docker-compose start` 在后台运行镜像。 

至此docker开发环境搭建完毕。
