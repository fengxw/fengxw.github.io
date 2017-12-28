---
layout: post
title: Mongodb Setup User and Password
modified: 2017-12-25
tags: [mongodb, docker, linux]
image:
  feature: abstract-3.jpg
---

1. start container with auth

    ```
    docker run --restart=always --name demo_db -itd -v /home/albert/workspace/tanku/data/mongo/db:/data/db  -p 27017:27017 mongo:3 --auth
    ```

2. login the database inside docker, user and pwd is unnecessary.

    ```
    docker exec -it demo_db /bin/sh
    mongo
    ```

3. add user as admin

    ```
    use admin //administrator db
    db.createUser({user: "root", pwd: "demo#$%!", roles: [ {role: "userAdminAnyDatabase", db: "admin"} ] }) // add user 'root'
    ```

4. exit, and login with the user 'root' and pwd

    ```
    mongo -u "root" -p "demo#$%!" --authenticationDatabase "admin"
    ```

5. authorize

    ```
    db.auth("root", "demo#$%!")
    ```

6. add user for bussness db

    ```
    use test_db
    db.createUser({user: "test", pwd: "Test", roles: [ { role: "readWrite", db: "test_db" } ]}) //为但前数据库添加用户，并分配读写权限
    ```

7. exit, login with the new user and pwd

    ```
    mongo -u "test" -p "Test" --authenticationDatabase "test_db"
    ```

8. authorize again

    ```
    use test_db
    db.auth("test", "Test")
    ```

9. finish and quit.


10. if using mongoose to access the encrypted db

    ```
    mongoose.connect('mongodb://username:password@host:port/database?options...');
    ```

