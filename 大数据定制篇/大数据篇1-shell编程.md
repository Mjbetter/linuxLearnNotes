# shell编程



#### 一、shell

1. shell是一个命令行解释器，它为用户提供一个向Linux内核发出请求以便运行程序的界面系统级程序，用户可以用Shell来启动，挂起，停止甚至是编写一些程序。

#### 二、Shell脚本的执行方式

1. 脚本格式要求

   - 脚本以#!/bin/bash开头
   - 脚本需要可执行权限

2. 编写第一个Shell脚本

   - 需求说明：创建一个Shell脚本，输出hello world！

     - ```shell
       #!/bin/bash
       echo "Hello,World!"
       ```

3. 脚本的常用执行方式

   - 方式1：（输入脚本的相对路径或者绝对路径）
     - 说明：首先要赋予helloworld.sh脚本的+x权限，再执行脚本。
       - chmod u+x helloworld.sh
   - 方式2：（sh+脚本）
     - 说明：不用赋予脚本+x权限，直接执行即可。

#### 三、Shell的变量

1. Shell变量介绍
   - Linux中Shell中的变量分为，系统变量和用户自定义变量
   - 系统变量$HOME,$PATH,$SHELL,$USER等等，比如，echo $HOME
   - 显示当前shell中所有变量：set
2. Shell变量的定义
   - 基本语法：
     - 定义变量：变量=值
     - 撤销变量：unset 变量
     - 声明静态变量：readonly变量，注意，不能unset
     - 输出变量需要加上$
     - shell脚本的多行注释： :<< !    内容 ！,前面和结尾都单独一行
3. 案例
   - 定义变量A：A=1
   - 撤销变量A：unset A
   - 声明静态变量B：readonly B=2
4. Shell变量的定义：
   - 定义变量的规则：
     - 变量名称可以由字母，数字，下划线组成，但是不能以数字开头
     - 等号两侧<font color="red">不能有空格</font>
     - 变量名称一般习惯大写
   - 将命令的返回值赋给变量
     - A='date'反引号，运行里面的命令，并把结果返回给A
     - A=$(date)等价于反引号

#### 四、位置参数变量

1. 当我们执行一个shell脚本时，如果希望获取到命令行的参数信息，就可以使用到位置参数变量，比如：./myshell.sh 100 200，这个就是一个执行shell的命令行，可以在myshell脚本中获取到参数信息

2. 基本语法：

   - $n：n为数字，$0代表命令本身，$1-$9代表第一个到第九个参数，十以上的参数需要用大括号来包含，如${10}
   - $*：这个变量代表命令行中的所有参数，$ * 把所有的参数看成一个整体
   - $@：这个变量也代表命令行中所有的参数，不过$@把每个参数区分对待
   - $#：这个变量代表命令行中所有参数的个数

3. 位置参数变量

   - 编写一个shell脚本position.sh，在脚本中获取到命令行的各个参数信息

     - ```shell
       #!/bin/bash
       echo "0=$0 1=$1 2=$2"
       echo "所有的参数=$*"
       echo "$@"
       echo "$#"
       ```



#### 五、预定义变量

1. 基本介绍

   - 就是shell设计者事先已经定义好的变量，可以直接在shell脚本中使用

2. 基本语法：

   - $$：当前进程的进程号（PID）
   - $!：后台运行的最后一个进程的进程号（PID）
   - $?：最后一次执行的命令的返回状态，如果这个变量的值为0，证明上一个命令正确执行。如果这个变量的值非0（具体什么数，由命令自己来决定），则证明上一个命令执行不正确了。

3. 实例

   - 在一个shell脚本中简单使用一下预定义变量--preVar.sh

     - ```shell
       #!/bin/bash
       echo "当前执行的进行id=$$"
       # 以后台的方式运行一个脚本，并获取他的进程号
       /root/shcode/myshell.sh &
       echo "最后一个后台方式运行的进程的id=$!"
       echo "执行的结果是$?"
       ```

#### 六、运算符

1. 基本语法：

   - “$((运算式))”或“$[运算式]” 或者 expr m + n
   - 注意expr运算符之间要有空格,如果要赋值给其他变量，要用``反引号括起来
   - expr m - n
   - expr \\*，/,%, 乘，除，取余

2. 应用实例

   - 计算（2+3）× 4的值

     - ```shell
       #!/bin/bash
       RES1=$(((2+3)*4))
       echo "res1=$RES1"
       RES2=$[(2+3)*4]
       echo "res2=$RES2"
       TEMP=`expr 2 + 3`
       RES3=`expr $TEMP \* 4`
       echo "res3=$RES3"
       ```

   - 请求出命令行的两个参数[参数]的和

     - ```shell
       SUM=$[$1+$2]
       echo "SUM=$SUM"
       ```

#### 七、条件判断

1. 判断语句

   - 基本语法：
     - [ condition ]（注意condition前后要有空格）
     - #非空返回true，可使用$?验证（0为true，1为false）
   - 常用判断条件
     - = 字符串比较
     - 两个整数的比较
       - -lt 小于
       - -le 小于等于
       - -eq 等于
       - -gt 大于
       - -ge 大于等于
       - -ne 不等于
     - 按照文件权限进行判断
       - -r 有读的权限
       - -w 有写的权限
       - -x 有执行的权限
     - 按照文件类型进行判断
       - -f 文件存在并且是一个常规的文件
       - -e 文件存在
       - -d 文件存在并是一个目录

2. 实例

   - “ok”是否等于“ok”

     - ```shell
       #!/bin/bash
       if [ "ok" = "ok" ]
       then
       	echo "equal"
       fi
       ```

   - 23是否大于等于22

     - ```shell
       #!/bin/bash
       if [ 23 -ge 22 ]
       then
       	echo "23>22"
       fi
       ```

   - /root/shcode/aaa.txt目录中的文件是否存在

     - ```shell
       #!/bin/bash
       if [ -f /root/shcode/aaa.txt ]
       then
       	echo "/root/shcode/aaa.txt目录中的文件存在"
       fi
       ```

#### 八、流程控制

1. if elif基本语法

   - ```shell
     if [ 条件判断式 ]
     then
     	代码
     fi
     # 或者
     if [ 条件判断式 ]
     then
     	代码
     elif [ 条件判断式 ]
     then
     	代码
     fi
     ```

2. case 基本语法

   - ```shell
     case $变量名 in
     "值1")
     程序1
     ;;
     "值2")
     程序2
     ;;
     "值3")
     程序3
     ;;
     *)
     都不是就执行程序4
     ;;
     esac
     ```

3. for循环基本语法

   - ```shell
     for 变量 in 值1 值2 值3...
     do
     程序
     done
     # 或者
     for ((初始值;循环控制条件;变量变化))
     do
     程序
     done
     ```

   - ```shell
     #!/bin/bash
     for i in $*
     do 
     	echo "num is $i"
     done
     for j in $@
     do
     	echo "num is $i"
     done
     
     SUM=0
     for (( i=1; i<=$1; i++ ))
     do
     	SUM=$[$SUM+$i]
     done
     echo "总和SUM=$SUM"
     ```

4. while循环基本语法

   - ```shell
     #!/bin/bash
     while [ 条件判断式 ]
     do
     	程序
     done
     ```

#### 九、read读取控制台输入

1. 基本语法：

   - read [选项] 参数
     - -p：指定读取值时的提示符
     - -t：指定读取值时的等待时间（秒），如果没有在指定的时间内输入，就不再等待了
   - 参数
     - 变量：指定读取值的变量名

2. 案例

   - 读取控制台输入一个NUM1值

     ```shell
     #!/bin/bash
     read -p "请输入一个数NUM1=" NUM1
     ```

   - 读取控制台输入一个NUM2值，在10秒内输入

     ```shell
     #!/bin/bash
     read -t 10 -p "请在10秒内输入数NUM1=" NUM1
     ```

#### 十、系统函数

1. 函数介绍

   - shell编程和其他编程语言一样，有系统函数，也可以自定义函数。系统函数中，这里介绍两个。

2. 系统函数

   - basename基本语法

     - basename [pathname] [suffix]
     - basename [string] [suffix] --basename命令会删掉所有的前缀包括最后一个（’/‘），然后将字符串显示出来。

   - 实例

     - 请返回/home/aaa/test.txt的"test.txt"部分

       ```
       basename /home/aaa/test.txt =>test.txt
       basename /home/aaa/test.txt .txt => test
       ```

   - dirname基本语法

     - 返回完整路径最后 / 的前面的部分，常用于返回路径部分

     - dirname 文件绝对路径 

     - ```
       dirname /home/aaa/test.txt => /home/aaa
       ```

#### 十一、自定义函数

1. 基本语法

   - ```shell
     [ function ] funname [()]
     {
     	Action;
     	[return int;]
     } 
     ```

   - 调用直接写函数名：funname [值]

2. 实例

   - 计算输入两个参数的和(动态的)，getSum

     ```shell
     #!/bin/bash
     function getSum ()
     {
     	SUM=$[$n1+$n2]
     	echo "和是=$SUM"
     }
     
     #输入两个值
     read -p "请输入一个数n1=" n1
     read -p "请输入一个数n2=" n2
     
     getSum $n1 $n2
     ```

#### 十二、定时备份数据库

1. 需求分析
   - 每天凌晨2:30备份，数据库mj 到/data/backup/db
   - 备份开始和备份结束能够给出相应的信息
   - 备份后的文件要求以备份时间为文件名，并打包成.tar.gz的形式，比如:2021-03-12_230201.tar.gz
   - 在备份的同时，检查是否有10天前备份的数据库文件，如果有就将其删除