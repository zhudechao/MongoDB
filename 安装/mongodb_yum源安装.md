##MongoDB_YUM源安装

参考资料

```
https://juejin.cn/post/6844903828811153421
```
配置yum源

```
ark ~]# vi /etc/yum.repos.d/mongodb-org-4.4.repo
[mongodb-org-4.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.4.asc

```
安装

```
ark ~]# yum install -y mongodb-org
```
运行

```
[root@ark ~]# systemctl start mongod.service      
```
重启

```
service mongod restart
```
检查运行情况

```
[root@ark ~]# netstat -natp | grep 27017
tcp        0      0 127.0.0.1:27017         0.0.0.0:*               LISTEN      20451/mongod  

[root@ark ~]# ps -aux | grep mongod
mongod   20451  1.6  6.5 1553392 66724 ?       Sl   21:50   0:00 /usr/bin/mongod -f /etc/mongod.conf
root     20488  0.0  0.0 112728   976 pts/0    R+   21:51   0:00 grep --color=auto mongod
```

运行客户端命令

```
[root@ark ~]# mongo
MongoDB shell version v4.4.2
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("6bf6c899-eb18-4a69-9eaa-a62eb0dd853c") }
MongoDB server version: 4.4.2
Welcome to the MongoDB shell.
For interactive help, type "help".
For more comprehensive documentation, see
	https://docs.mongodb.com/
Questions? Try the MongoDB Developer Community Forums
	https://community.mongodb.com
---
The server generated these startup warnings when booting: 
        2020-12-31T21:50:46.267+08:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
        2020-12-31T21:50:46.942+08:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
        2020-12-31T21:50:46.942+08:00: /sys/kernel/mm/transparent_hugepage/enabled is 'always'. We suggest setting it to 'never'
        2020-12-31T21:50:46.942+08:00: /sys/kernel/mm/transparent_hugepage/defrag is 'always'. We suggest setting it to 'never'
---
---
        Enable MongoDB's free cloud-based monitoring service, which will then receive and display
        metrics about your deployment (disk utilization, CPU, operation statistics, etc).

        The monitoring data will be available on a MongoDB website with a unique URL accessible to you
        and anyone you share the URL with. MongoDB may use this information to make product
        improvements and to suggest MongoDB products and deployment options to you.

        To enable free monitoring, run the following command: db.enableFreeMonitoring()
        To permanently disable this reminder, run the following command: db.disableFreeMonitoring()
---
> 

```