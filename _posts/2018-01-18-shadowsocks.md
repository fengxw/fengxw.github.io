---
layout: post
title: Ubuntu install shadowsocks and switchyOmega
modified: 2018-01-18
tags: [shadowsocks, switchyomega, ubuntu]
image:
  feature: abstract-2.jpg
---

## 1. Install shadowsocks-qt5 GUI
    
```bash
$ sudo add-apt-repository ppa:hzwhuang/ss-qt5
$ sudo apt-get update
$ sudo apt-get install shadowsocks-qt5
```

## 2. Configure shadowsocks

- ip: test.example.com
- port: 4443
- password: xxoo
- Encryption method: AES-256-CFB
<figure>
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011808.png" alt="set proxy">
</figure>
    
## 3. Install switchyOmega

open google chrome apps, search switchyomega and add to chrome
<figure>
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011805.png" alt="add switchomega">
</figure>

## 4. Configure switchyOmega

- **add socks server for proxy**
<figure>
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011801.png" alt="socks server">
</figure>

- **configure auto proxy**
<figure>
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011802.png" alt="auto proxy">
</figure>

> **Rule list URL:** https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt


## 5. Configure switch options in Interface

<figure>
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011803.png" alt="switch options">
</figure>

## 6. Enable switchOmega in chrome and enjoy

<figure>
    <img src="http://p2qcii88d.bkt.clouddn.com/2018011806.png" alt="enable switchOmeg">
</figure>
