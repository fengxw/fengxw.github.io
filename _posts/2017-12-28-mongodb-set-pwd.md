---
layout: post
title: Mongodb Setup User and Password
modified: 2017-12-28
tags: [mongodb, docker, js]
image:
  feature: abstract-3.jpg
---

1. start container with auth

    ```console
    $ docker run --restart=always --name demo_db -itd -v /data/mongo/db:/data/db  -p 27017:27017 mongo:3 --auth
    ```

2. login the database inside docker, user and pwd is unnecessary.

    ```console
    $ docker exec -it demo_db /bin/sh
    $ mongo
    ```

3. add user as admin

    ```console
    //administrator db
    $ use admin
    
    // add user 'root'
    $ db.createUser({user: "root", pwd: "demo#$%!", roles: [ {role: "userAdminAnyDatabase", db: "admin"} ] })
    ```

4. exit, and login with the user 'root' and pwd

    ```console
    $ mongo -u "root" -p "demo#$%!" --authenticationDatabase "admin"
    ```

5. authorize

    ```console
    $ db.auth("root", "demo#$%!")
    ```

6. add user for bussness db

    ```console
    $ use test_db

    // add user for test_db and assign read and write permission
    $ db.createUser({user: "test", pwd: "Test", roles: [ { role: "readWrite", db: "test_db" } ]})
    ```

7. exit and login with the new user and pwd

    ```console
    $ mongo -u "test" -p "Test" --authenticationDatabase "test_db"
    ```

8. authorize again

    ```console
    $ use test_db
    $ db.auth("test", "Test")
    ```

9. finish and quit.


10. if using mongoose to access the encrypted db

    ```js
    mongoose.connect('mongodb://username:password@host:port/database?options...');
    ```

