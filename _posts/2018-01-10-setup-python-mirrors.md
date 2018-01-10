---
layout: post
title: pip设置国内镜像
modified: 2018-01-10
tags: [python, pip, mirrors]
image:
  feature: abstract-5.jpg
---

### 设置方法

- #### 配置全局源

    在用户目录下创建pip.conf配置文件
    ```console
    $ mkdir ~/.pip && vim ~/.pip/pip.conf
    ```
    
    加入如下配置, pip安装需要使用的https加密, 所以在此需要添加trusted-host

    ```
    [global]
    trusted-host = mirrors.aliyun.com
    index-url = http://mirrors.aliyun.com/pypi/simple
    ```

- #### 手动指定源

    ```console
    $ pip -i http://mirrors.aliyun.com/pypi/simple install lxml
    ```

### pip常用国内镜像

```
http://pypi.douban.com/ 豆瓣
http://pypi.sdutlinux.org/ 山东理工大学
http://pypi.mirrors.ustc.edu.cn/ 中国科学技术大学
http://mirrors.aliyun.com/pypi/simple/ 阿里云
https://pypi.tuna.tsinghua.edu.cn/simple/ 清华大学
```