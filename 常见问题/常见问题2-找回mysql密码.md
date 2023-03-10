# 找回mysql的root密码



#### 一、修改步骤

1. ```shell
   vim /etc/my.cnf
   #然后在末尾加一句
   skip-grant-tables #表示跳过权限表，然后空密码就能登录
   #然后重启mysql服务
   restart mysqld.service
   mysqld -u root -p
   show databases
   #然后进去mysql这个数据库
   show tables
   #然后修改user表
   #里面有个authentication_string字段，这个就是root密码
   update user set authentication_string=password('mj20020519') where user='root'
   flush privileges #刷新权限
   #然后回到/etc/my.cnf，注销掉我们之前加的那句话
   restart mysqld.service重启服务
   ```

   

