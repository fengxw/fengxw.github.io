---
title: 运行docker命令不加sudo 
author: fengxw
---

---

1. 如果还没有docker group就添加一个：

```
sudo groupadd docker
```

2. 将用户加入该group内。然后退出并重新登录就生效啦。

```
sudo gpasswd -a ${USER} docker
```

3. 重启docker

```
sudo service docker restart
```

4. 如果是ssh, 退出ssh再重新登录
