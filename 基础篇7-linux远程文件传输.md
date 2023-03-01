# Linux远程文件传输



#### 一、传输使用的软件

​	远程上传下载文件-Xftp6，是一个基于windows平台的功能强大的SFTP，FTP文件传输软件，使用了Xftp后，windows用户就能安全的在UNIX/Linux和Windows PC 之间传输文件，下载方法和远程登录软件的下载方法一致。如果弹出来的只有Xshell的下载，那么选择的时候就不选择both，而是单独选择Xftp6即可。



#### 二、开始建立连接

​	按照如图开始配置端口即可，名称随意，主机选择虚拟机的ip地址，协议最好选择SFTP，端口号是22，不是21。

![image-20230301211908809](C:\Users\MJ\AppData\Roaming\Typora\typora-user-images\image-20230301211908809.png)

​	此时左边显示的是windows的文件，右边显示的是linux的文件，如果右边文件显示都是乱码，那么点击左上角的的文件，点当前会话属性，点选项，把编码换成utf-8即可。