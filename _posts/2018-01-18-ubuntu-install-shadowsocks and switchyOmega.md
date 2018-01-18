---
layout: post
title: Ubuntu install shadowsocks and switchyOmega
modified: 2018-01-10
tags: [shadowsocks, switchyomega, ubuntu]
image:
  feature: abstract-2.jpg
---

1. Install shadowsocks-qt5 GUI
    
    ```bash
    $ sudo add-apt-repository ppa:hzwhuang/ss-qt5
    $ sudo apt-get update
    $ sudo apt-get install shadowsocks-qt5
    ```

2. Configure shadowsocks

    - ip: test.example.com
    - port: 4443
    - password: xxoo
    - Encryption method: AES-256-CFB
    <figure class="half">
    	<img src="http://p2qcii88d.bkt.clouddn.com/2018011808.png" alt="set proxy"></a>
    </figure>
    
3. Install switchyOmega

    open google chrome apps, search switchyomega and add to chrome
    <figure class="half">
        <img src="http://p2qcii88d.bkt.clouddn.com/2018011805.png" alt="add switchomega"></a>
    </figure>

4. Configure switchyomega
    - add socks server for proxy
    <figure class="half">
        <img src="http://p2qcii88d.bkt.clouddn.com/2018011801.png" alt="socks server"></a>
    </figure>

    - configure auto proxy
    <figure class="half">
        <img src="http://p2qcii88d.bkt.clouddn.com/2018011802.png" alt="auto proxy"></a>
    </figure>

    > **Rule list URL:** https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
￼
5. Configure switch options in Interface
<figure class="half">
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011803.png" alt="switch options"></a>
</figure>

6. Enable switchOmega in chrome and enjoy
<figure class="half">
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011806.png" alt="enable switchOmeg"></a>
</figure>
