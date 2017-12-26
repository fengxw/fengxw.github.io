---
layout: post
title: Clear docker
modified: 2017-12-25
tags: [docker, linux]
image:
  feature: abstract-6.jpg
---


1. 移除意外停止运行的container

    ```
    sudo docker rm -v $(sudo docker ps --filter status=exited -q)
    ```
    
2. 移除不在使用中的image

    ```
    sudo docker rmi $(sudo docker images --filter "dangling=true" -q --no-trunc) 
    ```

3. 移除不在使用中的volume

    ```
    sudo docker volume rm $(sudo docker volume ls -qf dangling=true)
    ```


4. 移除不在使用中的镜像(没运行容器的镜像)

    ```
    docker images | awk '{print $3}' | xargs docker rmi
    ```


5. 清除所有不再运行中的容器, 镜像, 挂载目录, 网络层(所有未运行中的, 包括有用的和dangling)

    ```
    docker container prune -a
    
    docker image prune -a
    
    docker network prune -a
    
    docker volume prune -a
    
    docker system prune -a
    ```