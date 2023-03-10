# io监控



#### 一、linux的高级命令

1. ```shell
   netstat //网络状态监控
   top //系统运行状态监控
   lsblk //查看硬盘分区
   find //查看
   ps -aux //查看运行进程
   chkconfig //查看服务启动状态
   systemctl //管理系统服务器
   ```

#### 二、Linux查看内容，io读写，磁盘存储，端口占用，进程查看命令

1. ```shell
   iotop //查看磁盘资源占用
   df -lh //查看磁盘存储
   netstat -tunlp //端口占用情况
   ps -aux //进程查看
   ```

#### 三、用linux命令计算t2.txt第二列的和并输出

1. ```shell
   cat t2.txt | awk -F " " '{sum+=$2} END {print sum}' 
   ```

   

