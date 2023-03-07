# RPM与YUM



#### 一、rpm包的管理

1. 介绍：rpm用于互联网下载包的打包及安装工具，它包含在某些linux的发行版本之中，它生成具有.RPM扩展名的文件。RPM是ReaHat Package Manager（RedHat软件包管理工具）的缩写，类似于Windows的setup.exe，这一文件格式名称虽然打了RedHat的标志，但理念是通用的。
2. rpm包的简单查询指令
   - 查询已安装的rpm列表 rpm -qa | grep xx
3. rpm包命名格式
   - 一个rpm包名：firefox-60.2.2-1.el7.centos.x86_64
     - 名称：firefox
     - 版本号：60.2.2-1
     - 适用操作系统：el7.centos.x86_64  （表示centos.x的64位系统）
     - 如果是i686，i386表示32位系统，noarch表示通用。
4. rpm包的其他查询指令
   - rpm -qa：查询所安装的所有rpm软件包
   - rpm -qa | more
   - rpm -qa | grep X [rpm -qa | grep firefox]
   - rpm -q 软件包名：查询软件包是否安装
   - rpm -qi 软件包名：查询软件包的信息
   - rpm -ql 软件包名：查询软件包中的文件
   - rpm -qf 文件全路径名 查询文件所属的软件包
     - rpm -qf /etc/passwd
     - rpm -qf /root/install.log
5. rpm包的卸载
   - 基本语法：
     - rpm -e RPM包的名称 
   - 案例
     - 删除firefox包
     - rpm -e firefox
   - 如果其他软件包依赖于要删除的软件包，那么卸载时就会出现错误
   - 如果此时要强行删除，可以增加参数 --nodeps，就可以强制删除
     - rpm -e --nodeps foo
6. 安装rpm包
   - 基本语法：
     - rpm -ivh RPM包全路径名称
   - 参数说明
     - i=install 安装
     - v=verbose 提示
     - h=hash 进度条

#### 二、yum

1. yum是一个Shell前端软件包管理器，基于RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次性安装所有依赖的软件包。
2. yum的基本指令
   - 查询yum服务器是否有需要安装的软件
   - yum list | grep xxx软件列表
   - 安装指定的yum包
   - yum install xxx 下载安装