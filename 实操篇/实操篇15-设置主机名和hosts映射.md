# 设置主机名和hosts映射



#### 一、设置主机名

1. 指令：hostname：查看主机名
2. 修改文件在/etc/hostname 指定
3. 修改后，重启生效

#### 二、设置hosts映射

1. 如何通过主机名能够找到（比如ping）某个linux系统
   - windows：在C:\Windows\System32\drivers\etc\hosts文件指定即可
     - 添加 ip地址 主机名
   - linux：在/etc/hosts文件指定
     - 添加 ip地址 计算机名

#### 三、主机名解析过程分析（Hosts，DNS）

1. 一个文本文件，用来记录IP和Hostname（主机名）的映射关系。
2. DNS
   - DNS，就是Domain Name System的缩写，翻译过来就是域名系统。
   - 是互联网上作为域名和IP地址相互映射的一个分布式数据库。
   - <img src="../asset/image-20230306233333599.png">