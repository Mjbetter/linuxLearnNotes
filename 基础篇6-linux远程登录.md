# Linux远程登录



#### 一、远程登录软件

​	Linux-Xshell6，Xshell是目前最好的远程登录到Linux操作的软件，流程的速度并且完美解决了中文乱码的问题，是目前程序员的首选软件。Xshell是一个强大的安全终端模拟软件，它支持SSH1，SSH2，以及Microsoft Windows平台的TELNET协议。Xshell可以在Windows界面下用来访问远端不同系统下的服务器，从而比较好的达到远程控制终端的目的。

​	选择版本：free-for-home-school版本，免费的用于学习的版本

​	地址：https://www.netsarang.com/en/free-for-home-school/

#### 二、获取虚拟机ip地址

```
输入指令ifconfig
如果显示错误
Ubuntu环境下输入sudo apt install net-tools来安装工具包
完成以后再次输入ifconfig
```

<img  src= ".\asset\image-20230301205648562.png"/>

​	如上图所示，inet后面的192.169.58.128就是虚拟机的ip地址，然后我们在windows系统这边打开cmd，ping一下这个ip地址，看看能否正常通信。

<img src=".\asset\image-20230301205758756.png">

#### 三、开始建立连接

​	打开Xshell，新建会话，按照如图配置，名称随意，协议选择SSH，主机号就是我们虚拟机的IP地址，端口号22，然后点击确认即可。

<img  src= ".\asset\image-20230301210539851.png">

​	如果无法连接，那么就在虚拟机上输入指令：

```
sudo apt install openssh-server来安装服务包即可
```

​	随后在弹出的窗口选择接受并保存，然后输入连接的用户和密码即可成功连接。