# Linux权限



#### 一、权限的基本介绍

1. ls -l中显示的内容如下： -rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc
2. 0-9位说明：（-rwxrw-r--）
   - 第0位确定文件类型（d，-，l，c，b）
     - l是链接，相当于windows的快捷方式
     - d是目录，相当于windows的文件夹
     - c是字符设备文件，鼠标，键盘等
     - b是块设备，比如硬盘
   - 第1-3位确定所有者（该文件的所有者）拥有该文件的权限。---user
   - 第4-6位确定所属组（同用户组的）拥有该文件的权限。---group
   - 第7-9位确定其他用户拥有该文件的权限 --other 
3. rwx权限详解
   - [r]代表可读(read)：可以读取，查看
   - [w]代表可写(write)：可以修改，但是不可以删除该文件，删除一个文件的前提条件是对该文件所在的目录有写权限，才可以删除该文件。
   - [x]代表可执行(execute)：可以被执行
4. rwx作用到目录
   - [r]代表可读(read)：可以读取，ls查看目录内容
   - [w]代表可写(write)：可以修改，对目录内创建+删除+重命名目录
   - [x]代表可执行(execute)：可以进入该目录

#### 二、文件及目录权限实际案例

1. ls -l中显示的内容如下：-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc
   - 第一个字符表示文件类型： l d c b
   - 其余字符每三个一组(rwx)--读(r)写(w)执行(x)
   - 第一组rwx：文件拥有者的权限是读，写和执行
   - 第二组rw-：文件拥有者同一组的用户的权限是读写
   - 第三组r--：不与文件拥有者同组的其他用户的权限是读
2. 可用数字表示：r=4，w=2，x=1，因此rwx=4+2+1=7
   - 不同权限组合起来的和是不同的。
   - rw-：6，r-x：5，-wx=3，r--：4，-w-：2，--x=1
3. 其他说明
   - 1：文件：硬连接数或目录：子目录数
   - root：用户
   - root：组
   - 1213：文件大小（字节），如果是文件夹，显示4096字节
   - Feb 2 09:39：最后修改日期
   - abc：文件名

#### 三、修改权限

1. 基本说明：通过chmod指令，可以修改文件或目录的权限
2. 第一种方式：+，-，= 变更权限
   - u：所有者，g：所有组，o：其它人，a：所有人（u，g，o的总和）
   - chmod u=rwx,g=rx,o=x 文件/目录名
   - chmod o+w 文件/目录名 --给其它人添加写权限
   - chmod a-x 文件/目录名 --给所有用户除去执行权限
3. 第二种方式：通过数字变更权限
   - r=4，w=2，x=1    rwx=7
   - chmod u=rwx，g=rx，o=x 文件目录名
   - 相当于chmod 751 文件目录名

#### 四、修改所有者和所在组

1. 基本介绍
   - chown newowner 文件/目录--改变所有者
   - chown newowner:newgroup 文件/目录 --改变所有者和所在组
   - -R 如果是目录，则使其下所有子文件或目录递归生效
   - 请将/home/abc.txt 文件的所有者修改成tom  ---chown tom /home/abc.txt
   - 请将/home/kkk 目录下所有的文件和目录的所有者都修改成tom --chown -R tom /home/kkk
2. 修改文件所在组
   - chgrp newgroup 文件/目录 改变所有组
   - 请将/home/abc.txt 文件所在组修改成shaolin。--chgrp shaolin /home/abc.txt
   - 请将/home/kkk 目录下的所有文件和目录的所在组都修改成shaolin。--chgrp -R tom /home/kkk

#### 五、权限管理应用实例

1. 警察和土匪游戏

   - police,bandit

   - jack,jerry:警察

   - xh,xq:土匪

   - ```
     //1.创建组
     groupadd police和groupadd bandit
     //2.创建用户
     useradd -g police jack和useradd -g police jerry
     useradd -g bandit xh和useradd -g bandit xq
     //3.jack创建一个文件，自己可以读写，本组人可以读，其他组人没有权限
     su jack
     touch test.txt
     chmod 640 test.txt
     //4.jack修改该文件，让其他组人可以读，本组人可以读写
     chmod g+w test.txt
     chmod o+r test.txt
     //5.xh投靠警察，看看是否可以读写
     usermod -g police xh
     ```

   - 如果要对目录内的文件进行操作，需要先拥有对该目录的相应权限。

2. 神仙妖怪

   - 建立两个组（神仙（sx），妖怪（yg））

   - 建立四个用户（唐僧，悟空，八戒，沙僧）

   - 设置密码

   - 把悟空，八戒放入妖怪，唐僧，沙僧放入神仙

   - 用悟空建立一个文件（monkey.java该文件需要输出i am monkey）

   - 给八戒一个可以rw的权限

   - 八戒修改monkey.java（加入一句话）（i am a pig）

   - 唐僧沙僧对该文件没有权限

   - 把沙僧放入妖怪组

   - 让沙僧修改该文件monkey，加入一句话（“我是沙僧，我是妖怪”）

   - ```
     groupadd xs;groupadd yg --创建分组
     useradd -g xs ts;useradd -g xs ss;useradd -g yg wk;useradd -g bj yg --添加用户并分组
     passwd xs;passwd ts;passwd bj;passwd wk --设置密码
     su wk;touch monkey.java --登录悟空，创建文件
     chmod 770 monkey.java --自己所有权限，同组读写权限，其它人没有权限  （目录必须给x权限，不然无法进入目录）
     usermod -g yg se --沙僧进入妖怪组
     ```

3. x:表示可以进入到该目录，比如可以执行cd。r:表示表示可以ls，比如将目录的内容显示。w:表示可以在该目录，删除或者创建文件。





