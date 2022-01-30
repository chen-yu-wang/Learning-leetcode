### Linux目录结构

Linux一切皆文件

**Linux根目录下文件夹都是规定好的**，Linux根目录下每个文件夹内存放的内容都是规定好的；其下的：

​	**/usr**，类似windows下的programsfiles，用户的很多文件和应用程序基本都放在该目录下

​	/root为root用户的目录

​	/lib，开机所需的最基本的动态链接库，几乎所有应用都需要用到它

​	/ home为存放普通用户的主目录，内含已创建的所有用户的ID命名的目录

​	/bin目录，常用的指令放在bin下 

​	/sbin,存放系统管理员使用的系统管理程序		

​	/etc目录里有配置文件，存放系统管理所需要的配置文件和目录。比如mysql的配置文件、环境配置都放在etc下。

​	/boot目录下有linux启动时需要的核心文件

​	/proc，是一个虚拟目录，是系统内存的映射

​	/dev，设备管理器，**linux将所有的硬件映射成文件来进行管理**，一切皆文件。

​	/media，linux自动识别一些设备(U盘、光盘等)，识别后linux会将其挂载到这个目录下



### vi与vim

#### 常见的三种模式

​	正常模式：以vim打开一个档案直接进入，此模式中可以上下左右按键移动光标，可以删除内容、复制粘贴处理数据

​	插入模式：按下I、i、o、O、A、a、R、r等任何一个字母进入。

​	命令行模式：此模式中提供相关指令以完成读取，存盘、离开vim等操作

​							从插入模式中输入一个esc，再输入一个： 就可以进入该模式。

​							正常模式中输入:或/也可以进入该模式

​		:wq，就可以完成保存并退出。

​		: q,退出

​		:q! 强制退出不保存

#### 快捷键

<img src="pic\image-20220122210514077.png" alt="image-20220122210514077" style="zoom: 80%;" />

在正常模式下，有如下几个常见快捷键。

​	yy 复制当前行， p粘贴

​	4yy 复制4行

​	dd删除当前行

​	5dd删除5行

​	G定位到末行，gg定位到首行

​	**u 撤销之前的动作**

​	**ctrl+r 反撤销**

​	4 + shift+g 快速定位到第四行

命令行模式中：

​	/快捷查找，/hello查找hello，输入n就是查找下一个

​	set nu 设置行号



### 关机与重启

#### 基本命令

​	shutdown 默认是shutdown -h 1 一分钟后关机

​	shutdown -h now 立即关机

​	halt 立即关机

​	reboot 立即重启

​	sync 将内存的数据同步到磁盘

#### 细节

​	㡳重启系统还是关机，都应该首先运行sync命令，将内存数据写入磁盘

​	目前的三种shutdown/halt/reboot在底层都已经调用了sync，但最好还是写一遍



### 用户登录与重启

​	su root 从a切换至root权限，exit(或logout)从root切换至a，在a用户下logout会直接退出系统

​	su 用户名 切换用户，从高权限用户切换低权限用户不需要输入密码，反之则需要输入密码 

​	logout 注销用户，但是**在图形界面logout是无效的，只有在运行级别3，多用户无图形界面下有效**



### 用户管理

#### 添加用户

​	useradd 用户名 添加用户，默认该用户的家目录在/home/用户名

​	userad  -d 用户目录  用户名， 此命令可以指定用户目录的文件夹名，默认是与用户名相同

#### 指定/修改密码

​	passwd 用户名 ，用户名一定要指定清楚，否则是默认修改当前登录用户的密码

#### 删除用户

​	userdel 用户名 ，仅删除用户，但是保存家目录，即home目录下仍然有该用户的文件夹

​	userdel -r 用户名 删除用户名与家目录

#### 查询用户信息

​	id 用户名 

​	whoami 查询当前用户名，**查询的是当前的用户**，比如用a登录后su root，查询到的是root

​	who am i 查询当前用户信息，包括登录时间等；**查询的是登录时的用户**，比如用a登录后su root，查询到的是a

#### 用户组操作

​	groupadd 组名 新建组

​	groupdel 组名 删除组

​	useradd -g 用户组 用户名 添加一个用户到指定组(组需要提前建好)，当useradd没有指定组时，会新建一个同名组，该用户是改同名组的唯一成员

#### 用户和组相关文件

​	/etc/passwd文件：用户(user)的配置文件，记录用户的各种信息，每行的含义：用户名：口令：用户标识号：组标识号：注释性描述：登录shell(一般是bin下的bash)

​	/etc/shadow文件：口令的配置文件

​	/etc/group文件：组的配置文件



### 运行级别

#### 基本介绍

​	0：关机

​	1：单用户(可以用来找回丢失密码)

​	2：多用户状态无网络服务(不常用)

​	**3：多用户状态有网络服务(最常用)**

​	4：保留

​	5：图形界面(常用)

​	6：系统重启

#### 相关指令

​	init  num 切换运行级别

​	systemctl get-default 查看当前的默认运行级别

​	systemctl set-default xxxx.target 设置默认运行级别



### 文件目录类指令

​	pwd 显示当前所在的绝对路径

​	ls 显示当前目录下的目录与文件

​			-a 显示所有文件与目录，包括隐藏的

​			-l  以列表的方式显示

​	cd 切换到指定目录，可以使用相对路径与绝对路径

​			cd~回到家目录(root的在/root，tom在/home/tom)

​			cd ..回到当前目录的上级目录

·	mkdir 创建目录(默认只能创建一级目录)

​			mkdir -p 创建多级目录	(mkdir -p /home/wudang/zwj)

​	rmdir 删除空目录

​			rm -rf /home/wudang  删除整个wudang目录

​	touch xx.xx 创建一个空文件

​	cp source dest拷贝指定文件到指定目录

​			cp -r source dest 递归复制整个**文件夹**

​			\cp -r source dest 强制覆盖不提示(不强制的话每个同名文件会请示是否覆盖)

​	rm xxx 删除文件

​			rm -r xx 递归删除整个文件夹(会一直请示每个文件)

​			rm -f xx  强制删除不提示

​	mv oldfilename newfilename 重命名

​	mv file targetfolder 移动文件

​	cat file 查看文件 

​			cat只能浏览文件，为了使用方便，一般使用 cat -n file| more (-n可显示行号，在more管道查看中，输入enter显示下一行，空格翻页)

​	more file 文本过滤器，以全屏方式显示内容，内置许多快捷键

​			Enter 显示下一行

​			space 翻页

​			q 退出

​			ctrl+f 向下滚动一屏

​			ctrl+b 返回上一屏

​			= 输出当前行号

​			:f 输出文件名与末尾行号

​	less file 查看文件，不同于more的全部加载，less是根据需要加载，适合显示大文件

​			space 向下翻页

​			pageup  向上一行 pagesown 向下一行

​			/字串 向下搜寻字串，  n下一个  N 上一个

​			字串 向上搜寻

​			q 退出

​	head file 显示文件开头部分内容，默认前十行

​			head -n 12 file 显示file前12行

​	tail file 显示file尾部内容，默认最后十行

​			tail -n 5 file最后五行

​			**tail -f file 追踪file，当文件被删除或改名时，追踪终止**

​			tail -F file 追踪file，并保持重试，当文件被删除或者改名后，如果出现相同名字文件，继续追踪

​			tailf file 追踪file，但是当文件不增长时不会访问磁盘

​	echo 输出内容到控制台

​			echo $HOSTNAME(主机名) $helloword(输出helloword) $PATH(输出路径)

​			echo haha > file 用haha覆写file文件的内容

​			echo haha >> file 将haha**追加**到file文件的末尾



### 查找指令

​	find 范围 选项 	递归查找指定目录及其下子目录，将满足条件的文件或目录显示在终端

​			find -name 查询方式 	 按照指定文件名查找

​			find -user 用户名	查找属于指定用户的所有文件

​			find -size 文件大小(+200M -200M 分别是大于与小于200M 的文件)	查找指定大小的文件

​	locate file 查找文件，显示文件路径

​			locate使用数据库，因此在使用locate之前必须updatedb指令创建locate数据库

​	grep指令+|管道符号，可以只显示文件内需要的内容

​			举例：cat /home/he.txt | grep -n "hello"	(其实也可以 grep -n "hello" /home.he.txt)

​			常用选项	-i 忽略字母大小写

​								-n 显示行号



### 压缩与解压指令

​	gzip file 	压缩成*.gz文件

​	gunzip *.gz 	解压.gz文件

​	zip [选项] xxx.zip file	将file压缩并命名为xxx

​			unzip -r  myhome.zip /home/ 将整个home压缩成myhome.zip

​	unzip [选项] xxx.zip 	解压缩

​			常用选项： -d <目录>  指定压缩以后存放路径

​								-r 递归压缩整个文件夹

​	tar [选项]  XXX.tar.gz  打包内容

​			常用选项： -c 产生.tar 文件

​								-v 显示详细信息

​								-f 指定压缩后的文件名

​								-z 打包同时压缩

​								-x 解包.tar文件

​			举例：tar -zcvf pc.tar.gz haha.txt hello.txt 将两个txt打包压缩成pc.tar.gz

​						tar -zxvf  pc.tar.tz -C /opt/tmp2 将pc解压到指定目录需要用到**-C**



### 所有者/所在组/rwx权限

#### 文件所有者

​	ls -ahl 	显示文件所有者

​	chown 用户名 文件名	更改文件的所有者

#### 文件所在组

​	groupadd 组名	新建一个组

​	ls -ahl	显示文件所在组

​	chgrp 组名 文件名	修改文件所在组

#### 用户所在组

​	usermod -g 新组名 用户名	用root更改用户所属组

​	usermod -d 目录名 用户名 	改变该用户登录的初始目录(注意该用户一定要能进入该目录)

#### rwx权限

##### 权限的基本介绍

​		例：ls -l 显示的内容如下： **-rwxrw-r--** 1 root root 1213 Feb 2 09:39 abc

​		前九位分别表示的含义 

​				(1).第0位确定文件类型(d,-,l,c,b)

​						l是连接，相当于win的快捷方式

​						d是目录，类似win的文件夹

​						c是字符设备文件，比如鼠标键盘

​						b是块设备，比如磁盘

​				(2).1~3位确定所有者对该文件的权限，此处是可读写可执行

​				(3).4~6位确定所属组对该文件的权限，此处为可读写不可执行

​				(4)7~9位确定其他组对该文件的权限，此处为只可读

​		其他说明：

​				1	文件：硬链接数目     目录：子目录数量

​				root 	用户

​				root 	组

​				1213	文件大小(字节)

​				Feb 2 09:39 	最后修改日期

​				abc	文件名

##### rwx作用于文件

​		[r]代表可读，查看

​		[w]代表可写，可以修改，但不代表可以删除该文件(**删除一个文件的条件是对该文件所在目录由写权限**)

​		[x]代表可执行

##### rwx作用于目录

​		[r]代表可读，可ls查看目录内容

​		[w]代表可写，可以修改，可以在目录内创建+删除文件+重命名该目录

​		[x]代表可执行，**可以进入该目录**

#### 文件rwx权限修改——chmod

##### 方法一:+ - = 变更权限

​		u:所有者 	g:所有组	o:其他人	a：所有人(ugo)

​		chmod u=rwx,g=rx,o=x abc		=是声明，给所有者以rwx，所在组rx，其他人x

​		chmod u-x,g+w, abc		+是增加，-是除去，给所有者除去x，所在组增加w

##### 方法二:数字变更权限

​		r = 4 w = 2 x = 1

​		chmod 751 abc  	给abc以所有者rwx，所在组rx，其他人x权限

#### 文件所有者修改——chown

​		chown newowner file 	改变所有者

​		chown newowner:newgroup file	改变所有者与所在组

​		如果是目录，则 **-R**可以使其下所有子目录都递归生效



### crond任务调度

#### 概述

​	任务调度：指定系统在某个时间执行的特定命令或程序

​	任务调度分类：①系统工作，一些重要的工作必须周而复始进行，如病毒扫描

​							   ②个别用户工作：个别用户可能希望执行某些程序，如mysql的备份

#### 用法

​	设置任务调度文件：/etc/crontab

​	设置个人任务调度，执行crontab -e命令

​	接着输入任务到调度文件，如*/1 * * * * ls -l /etc/ > /tmp/to.txt

​	<img src="pic\image-20220128171726193.png" alt="image-20220128171726193" style="zoom:80%;" />

​	<img src="pic\image-20220128171857986.png" alt="image-20220128171857986" style="zoom:80%;" />

![image-20220128194917241](pic\image-20220128194917241.png)	

​	crontab [选项]

​				-e	编辑crontab定时任务

​				-l	 查询crontab任务

​				-r 	删除当前用户所有的crontab任务



### at定时任务

#### 概述

​	at命令是一次性定时任务，at的守护进程atd会以后台模式运行，每六十秒检查作业队列，有作业时，会检查作业运行时间，若与当前时间匹配，则执行，且**只执行一次**	

​	在使用at命令前，一定要确定atd是否已经启用，使用如下命令查询：ps -ef | grep atd

#### 用法

​	at [选项] [时间] 	

​	atq可以查看当前队列中的任务们

​	atrm + 编号 可以按编号移除队列任务

​	**退出用Ctrl +D**![image-20220128211813838](pic\image-20220128211813838.png)

​	![image-20220128211844026](pic\image-20220128211844026.png)



### Linux磁盘分区与挂载

#### Linux分区

​	Linux硬盘分IDE硬盘和SCSI硬盘，目前基本上是SCSI硬盘
​	对于IDE硬盘，驱动器标识符为“hdx~”，其中“hd”表明分区所在设备的类型，这里是指IDE硬盘
了。“x”为盘号（a为基本盘，b为基本从属盘，c为辅助主盘，d为辅助从属盘），“～”代表分区，
前四个分区用数字1到4表示，它们是主分区或扩展分区，从5开始就是逻辑分区。例，hda3表示为
第一个IDE硬盘上的第三个主分区或扩展分区，hdb2表示为第二个IDE硬盘上的第二个主分区或扩展
分区。
​	对于SCSI碰盘则标识为“sdx~”，SCSI硬盘是用“sd”来表示分区所在设备的类型的，其余则和
IDE硬盘的表示方法一样。

#### 设备挂载相关命令

​	lsblk 或者  lsblk   -f	查看所有设备挂载情况

​	fdisk /dev/sdxxx	开始对sdxxx分区，随后键入： n，新增分区，然后选择 p ，分区类型为主分区。两次回车默认剩余全部空间。最后输入 w 写入分区并退出，若不保存退出输入 q。、

​		常用命令如下：

​				m	显示命令列表	

​				p	 显示磁盘分区，同fdisk -l

​				n	 新增分区

​				d 	删除分区

​				w	 写入并退出(注意**退出前一定要w**，否则都不保存)

​	mkfs -t ext4   /dev/sdxx		将adxx格式化 	，其中ext4是分区类型

​	mount	/dev/sdxx	挂载目录		将一个分区与一个目录联系起来，注意，**重启后会失效**

​	umount		设备名/挂载目录	解除挂载

​	**修改/etc/fstab可以实现永久挂载**

#### Linux磁盘使用情况查询

​	df -h 	查询磁盘整体使用情况

​	du -h /目录	查询指定目录的磁盘占用情况(不指定目录则查询当前目录)

​		举例：du -hac --max-depth=1 /opt

​			-s 指定目录占用大小汇总 

​			-h 带计量单位 

​			-a 含文件

​			-c 列出明细的同时，增加汇总值

​			--max-depth=1 子目录深度 

#### Linux磁盘实用指令举例

​	1) 统计/opt 文件夹下文件的个数	 ls -l /opt | grep "^-" | wc -l 

​				"^-"正则表达式表示以-开头的，也就是非文件夹，	

​				| wc -l	管道，统计数目

​	2) 统计/opt 文件夹下目录的个数 	ls -l /opt | grep "^d" | wc -l 

​	3) 统计/opt 文件夹下文件的个数，包括子文件夹里的	ls -lR /opt | grep "^-" | wc -l 

​				-R表示递归

​	4) 统计/opt 文件夹下目录的个数，包括子文件夹里的	 ls -lR /opt | grep "^d" | wc -l 

​	5) 以树状显示目录结构 tree 目录 	tree /home/



### Linux网络配置

#### Linux网络环境配置之自动获取

​	DHCP,	登陆后，通过界面的来设置自动获取 ip，特点：linux 启动后会自动获取 IP,缺点是每次自动获取的 ip 地址可 能不一样

#### Linux网络环境配置之指定IP

​	直接修改配置文件来指定 IP,并可以连接到外网

​	编辑 vi /etc/sysconfig/network-scripts/ifcfg-ens33

```
	BOOTPROTO=static
	#IP地址
	IPADDR=192.168.200.130
	#网关
	GATEWAY=192.168.200.2
	#域名解析器
	DNS1=192.168.200.2
```

​	重启网络服务或者重启系统生效 	service network restart 