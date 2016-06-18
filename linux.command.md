linux严格区分大小写

su root   切换到root用户

dhclient   获得IP

linux里root的权限最高，建议平时用普通用户，linux也可以有多个root

etc文件夹 为配置文件夹

home为家目录，一个账号一个家目录，用来放置各自的信息

lib为共享函数库

boot为引导库

usr字体帮助文档目录

var 邮件www目录

ctrl+C终止当前命令

shell 用户与内核沟通的中间人

图形化shell--gui
命令行shell--cli





=================命令行===================
命令+选项+参数

ls 显示当前文件

ls -l  详细显示当前目录

ls -l /root  显示root目录的详细文件

ctrl+l 或者 clear 清零结果显示

date  显示当前的日期和时间 年月日时分秒 星期二 东八区

date "+%Y-%m"  指定日期显示格式

date "+%Y-%m-%d %H:%I:%S"

ls / 显示文档根目录文件和文件夹信息

ls -l / 详细显示

yum search tree  安装目录树

cal  显示日历

cal 18 3 2010  显示2010年3月18日的日历

ctrl+alt+f1~f5 切换终端界面

ctrl+shift+=  放大终端界面

ctrl+shift+-  缩放终端界面

useradd 用户名 增加一个用户 只能由root操作

passwd dy 为用户dy更改密码  要root权限才能改

su dy   切换为用户 dy

tab键能够自动补全

连按两下tab键 可以看到总共有的命令的总数

ctrl+c 放弃刚才打入的行或正在执行的命令

exit  退出

ctlr+d   退出

man date 列出date命令，精简版没有man命令

shutdown -h now    立刻关机，需要root权限或者配置相应权限

cd  不到任何参数则为进入当前用户的家目录

cd  /home  进入家目录

sh  显示以s开头的所有命令

reboot  重启，需要root权限

who 查询当前连接linux的用户

shutdown -h +10 "10 i shutdown"  10分钟后关闭并发送广播

shutdown -r now    是重启

==========================权限=========================
账号（用户）user
角色（用户组）group
其他人other

cd  回到当前用户的home文件夹

[daiyan9095@bogon Desktop]$ cd  回到当前用户的home文件夹
[daiyan9095@bogon ~]$ cd /tmp   进到tmp文件目录，要带斜线

[daiyan9095@bogon ~]$ yum search tree  安装文档树插件

[daiyan9095@bogon tmp]$ pwd  显示当前目录

[daiyan9095@bogon ~]$ touch houdunwang.php  在家目录里建立一个空文件

[daiyan9095@bogon ~]$ ls /home/daiyan9095  查看刚才创建的文件

[root@bogon daiyan9095]# exit   退出root的shell,回到之前用户的shell

[daiyan9095@bogon ~]$ ls -l houdunwang.php  显示文件的详细信息

[daiyan9095@bogon ~]$ ls -il 查看当前用户所有文件的id号



-rw-rw-r--. 1 daiyan9095 daiyan9095 0 Jun 13 16:49 houdunwang.php
解释：-为文件类型，表示一个普通文件，若是d的话则为目录
      后面的各位表示权限，3个为一个单位
      前三个rw-指的是所有者daiyan9095的权限
      中间的3个rw-指的是所有组的权限
      后边的三个r--代表的是其他人
r代表可读，w代表可写， 这个-代表执行(属性为不能执行) 若为x则为可以执行    

      1表示链接数，daiyan9095表示用户（创建者），后边的daiyan9095为用户组，
      0 表示文件的大小 使用ls -lh则输出的是kb的大小
      Jun 13 16:49为文件的修改时间

[daiyan9095@bogon ~]$ echo "abc">>houdunwang.php  将abc追加到文件内部

[daiyan9095@bogon ~]$ cat houdunwang.php  查看一下文件内容

[daiyan9095@bogon ~]$ vim houdunwang.php  使用vim查看文件内容

在linux中的以.开头的文件就是隐藏文件 

[daiyan9095@bogon ~]$ ls -a   显示所有的文件，包括隐藏文件

[daiyan9095@bogon ~]$ mkdir abc   在当前目录下新建一个文件目录abc

[daiyan9095@bogon ~]$ rmdir abc 删除当前目录里的abc目录

[daiyan9095@bogon ~]$ touch a  在当前目录下新建立一个a目录

[daiyan9095@bogon ~]$ umask -S 输出文件创建时设置的默认权限

权限的数字表示：
    r=4  w=2  x=1 

-rwxrwxrwx  权限：777 

[daiyan9095@localhost ~]$ mkdir b   在当前文件目录下建立b目录
此时的详细信息：drwxrwxr-x. 2 daiyan9095 daiyan9095 4096 Jun 14 07:49 b
说明对目录给予了x的权限

[daiyan9095@localhost ~]$ umask  不带参数 -S的话会以数字的形式表示文件的权限，这里得到的值为0002,可以使用减法，7-0=7 7-0=7 7-0=7 7-2=5 同样能得到文件的权限信息

[daiyan9095@localhost ~]$ umask -S  则结果为u=rwx g=rwx o=rx 

ls -l 的缩写形式为  ll 

[daiyan9095@localhost ~]$ cd /tmp   进到临时目录

[daiyan9095@localhost tmp]$ mkdir dy  创建目录  dy 

[daiyan9095@localhost tmp]$ cd dy  进入到dy 目录下

[daiyan9095@localhost dy]$ touch a/1.php  在tmp下的dy里的a下放置一个文件1.php 

-rw-rw-r--. 1 daiyan9095 daiyan9095 0 Jun 14 07:59 1.php  该文件的信息

[daiyan9095@localhost a]$ chmod 777 1.php   更改1.php的权限 

-rwxrwxrwx. 1 daiyan9095 daiyan9095 0 Jun 14 07:59 1.php  加完权限后的信息

[daiyan9095@localhost a]$ echo "hello world">>1.php  在1.php里写入hello world 

[daiyan9095@localhost a]$ cat 1.php   输出 1.php的内容 

以上的权限仅指的是文件的内容，与文件自身无关，要看文件是否可删要看其目录的权限 

drwxrwxr-x. 2 daiyan9095 daiyan9095 4096 Jun 14 07:59 a   看到其他人对目录仅有读的权限而没有写的权限，因此不能删除a下的文件 

exit  退出当前的shell

[daiyan9095@localhost dy]$ chmod 770 a   改变a的权限，要在其父目录里面改 

目录的rwx ：w 表示新建文件和删除文件移动文件，即增删改
            r 表示读取目录
            x 表示能够进入到目录里面 

chmode   改变文件权限  

[daiyan9095@localhost dy]$ hostname   显示主机名 

[daiyan9095@localhost qq]$ chmod u=rw sina   更改所有者的权限为rw即6

[daiyan9095@localhost qq]$ chmod g=r sina   单独更改所有组的权限

[daiyan9095@localhost qq]$ chmod o=rwx sina   单独更改其他人的权限 

[daiyan9095@localhost qq]$ chmod o=rwx,g=rwx sina  

[daiyan9095@localhost qq]$ chmod o-w sina 使得其他人对文件不具有w的权限，即减掉权限 

[daiyan9095@localhost hd]$ chmod u-r,g-r,o-r baidu  去掉用户的r权限 

[daiyan9095@localhost hd]$ chmod -r baidu  去掉用户的r权限 

[daiyan9095@localhost dy]$ chown qq index.php 将index.php的所有者改为qq 

[daiyan9095@localhost dy]$ chown qq:qq index.php 改变index.php的所有者和所有组 

rm 文件名 删除文件
rmdir 目录名 删除目录，此目录必须为空 

[root@localhost tmp]# mkdir -p www/admin/tpl 递归创建目录  

touch  新建文件  

[root@localhost www]# chown -R daiyan9095:daiyan9095 admin 递归的将admin即其子目录和文件改变所有者和所有组

.代表当前目录
..代表上一级目录

[daiyan9095@localhost ~]$ cd .  还是当前目录

[daiyan9095@localhost ~]$ cd .. 进入到上一级目录

[daiyan9095@localhost ~]$ ls .  显示当前目录

[daiyan9095@localhost ~]$ ls ..  显示上一级目录

[daiyan9095@localhost ~]$ ls ../... 显示上上一级的目录 

[daiyan9095@localhost a]$ ls -l ..

[daiyan9095@localhost a]$ ls -l ../..

[daiyan9095@localhost a]$ ls ../../dy

[daiyan9095@localhost ~]$ cd ~daiyan9095  进入用户的家目录 

[daiyan9095@localhost ~]$ cd -  在之前的工作目录之间进行切换 

[daiyan9095@localhost ~]$ echo $PATH  输出linux的环境变量

[daiyan9095@localhost ~]$ PATH=$PATH:/daiyan9095  增加环境变量，一定要带着原来的$PATH否则重写了

[daiyan9095@localhost ~]$ ./houdunwang.php  没有增加当前目录的环境变量的话要执行当前目录下的文件就要加./

dirname 取得父级目录

basenam取得文件的名字

[daiyan9095@localhost ~]$ basename ~daiyan9095

[daiyan9095@localhost ~]$ ls -lh 按k表示文件的大小显示文件信息

[daiyan9095@localhost ~]$ ls -lhS 以文件大小降序显示

[daiyan9095@localhost ~]$ ls -lhSr 以文件大小升序显示

[daiyan9095@localhost ~]$ ls -la

[daiyan9095@localhost ~]$ ls -ltS  按时间降序排列

[daiyan9095@localhost ~]$ mkdir ~/html  在自己家创建一个html目录 

[daiyan9095@localhost ~]$ rmdir -p html/admin/ask 递归删除空目录

[daiyan9095@localhost ~]$ rm -rf a  删除a下的所有文件

[daiyan9095@localhost ~]$ rm -r a/b/c  询问递归删除目录

#7 
 移除目录  rmdir
 移除文件 rm 
[root@localhost www]# chown -R daiyan9095:daiyan9095 admin  递归更改目录文件的所有者和所有组，该文件夹及以下的文件都被更改

[root@localhost model]# pwd

[root@localhost model]# ls /  显示根目录 

[root@localhost model]# cd ~ 回到家目录

[root@localhost ~]# cd ~daiyan9095  到daiyan9095的家目录 


[root@localhost ~]# cd -   在上一个目录之间来回的切换


#8

[root@localhost www]# cp hd.sh admin  将hd.sh文件复制到admin 

[root@localhost www]# cp hd.sh admin/a.sh 复制文件并改名

[root@localhost admin]# cp * model 复制当期目录下的所有文件到model

[root@localhost admin]# rm -rf model 递归删除model及其下的所有文件
  
[root@localhost www]# cp index.php ~daiyan9095  复制文件到daiyan9095的家目录

[daiyan9095@localhost www]$ cd ~ 到daiyan9095的家目录

[daiyan9095@localhost ~]$ scp  远程复制

[root@localhost daiyan9095]# mv index.php index01.php  改名字

[root@localhost daiyan9095]# mv b a  更改目录名

[root@localhost daiyan9095]# scp y1.php root@www.houdunwang.com:/www/html/edu/y1.php    通过远程ssh将y1.php复制到后盾网的服务器的根目录下的www下的html下的edu的y1.php

[root@localhost daiyan9095]# ll --full-time  显示详细的时间

[root@localhost daiyan9095]# touch -t 0902211033 a  将文件a的创建时间改为09年2月21日10点33分

软连接--快捷方式
[daiyan9095@localhost admin]$ touch baidu.sh
[daiyan9095@localhost admin]$ echo "echo 'baidu.sh'">>baidu.sh
[daiyan9095@localhost admin]$ cat baidu.sh
echo 'baidu.sh'
[daiyan9095@localhost admin]$ ./baidu.sh
bash: ./baidu.sh: Permission denied
[daiyan9095@localhost admin]$ chmod u+x baidu.sh 
[daiyan9095@localhost admin]$ ./baidu.sh
baidu.sh


[root@localhost admin]# ./baidu.sh   本地执行
baidu.sh
[root@localhost admin]# ln -s /tmp/www/admin/baidu.sh /usr/bin/baidu.sh  创建软连接，类似快捷方式

[root@localhost ~]# baidu.sh   不用加路径直接执行
baidu.sh


[root@localhost tmp]# ls -il   显示文件节点 
total 4
927247 -rw-r--r--. 1 root       root        0 Jun 17 12:57 1.txt
927241 -rw-r--r--. 1 root       root        0 Jun 17 12:14 a.sh
927246 -rwxrw-r--. 1 daiyan9095 daiyan9095 16 Jun 17 12:46 baidu.sh
927240 -rw-r--r--. 1 root       root        0 Jun 17 12:12 hd.sh

硬链接：多个文件名引用同一个文件
[root@localhost admin]# ln /tmp/www/admin/1.txt /tmp/www/1.bak.txt

[root@localhost www]# ll -i
total 4
927247 -rw-r--r--. 2 root       root          0 Jun 17 12:57 1.bak.txt  此时它与1.txt的节点号相同，且变为2表示两个引用
927229 drwxr-xr-x. 2 daiyan9095 daiyan9095 4096 Jun 17 12:57 admin
927239 -rw-r--r--. 1 root       root          0 Jun 17 12:12 hd.sh
927085 -rw-r--rwx. 1 root       root          0 Jun 17 12:17 index.php


[root@localhost admin]# rm 1.txt
rm: remove regular empty file `1.txt'? y
[root@localhost admin]# cd ..
[root@localhost www]# l
bash: l: command not found
[root@localhost www]# ll -i
total 4
927247 -rw-r--r--. 1 root       root          0 Jun 17 12:57 1.bak.txt  此时仅有一个引用，变为1
927229 drwxr-xr-x. 2 daiyan9095 daiyan9095 4096 Jun 17 13:03 admin
927239 -rw-r--r--. 1 root       root          0 Jun 17 12:12 hd.sh
927085 -rw-r--rwx. 1 root       root          0 Jun 17 12:17 index.php

mv也可以移动，也可以改名
[root@localhost www]# mv 1.bak.txt admin/1.bak.txt
[root@localhost www]# cd admin
[root@localhost admin]# ll
total 4
-rw-r--r--. 1 root       root        0 Jun 17 12:57 1.bak.txt
-rw-r--r--. 1 root       root        0 Jun 17 12:14 a.sh
-rwxrw-r--. 1 daiyan9095 daiyan9095 16 Jun 17 12:46 baidu.sh
-rw-r--r--. 1 root       root        0 Jun 17 12:12 hd.sh

cat 查看文件所有内容 
more 一部分的查看文件内容 相当于分页，分屏

[root@localhost www]# more index.php  可以用空格键来翻页，按q则退出查看

less index.php  可以上下滚动的查看文件内容 相当于长网页，可以在底部运用正则表达式来高亮匹配内容
/isset   按n向下查看，按q退出

[root@localhost www]# less index.php
...
果要将一个变量强制转换为某类型(如在变量前加(string)转换为字符串)，可以对其使用强制转换或者 `settype()` 函数。
gettype()返回参数的类型字符串
echo gettype("a");//string
$a=array();
echo gettype($a);//array 

/isset   正则查询

按n向下查询，N向上查找；按q退出 

[root@localhost www]# tail -5 index.php   仅显示后5行
[root@localhost www]# head -5 index.php   仅显示前5行

查找文件
[root@localhost www]# find / -user daiyan9095  从根目录下开始查找与daiyan9095用户相关的文件

[root@localhost www]# find / -size +6000k 查找600k以上的文件

[root@localhost www]# find / -name index.php  查找文件名为index.php的文件

[root@localhost www]# which passwd  查找passwd
/usr/bin/passwd

[root@localhost www]# whereis index.php 查找index.php
index: /usr/share/man/man3/index.3.gz /usr/share/man/man3p/index.3p.gz
没有查找到，是因为那是今天创建的文件，文件名数据库还未更新

updatedb  更新文件名数据库
[root@localhost www]# locate index.php  这时查找到index.php文件
/home/daiyan9095/.index.php.swp

which 和 whereis  一般用来查询命令

locate 用来查询某一文件（从数据库，此数据库一天更新一次）
find是全盘搜索，速度较慢
[root@localhost www]# which ll
alias ll='ls -l --color=auto'
      /bin/ls
和
[root@localhost www]# whereis ls
ls: /bin/ls /usr/share/man/man1/ls.1.gz /usr/share/man/man1p/ls.1p.gz

find可以根据大小、名字、时间等进行查询，查看文档

#磁盘操作

[root@localhost ~]# ls -lh  h查看磁盘大小

[root@localhost ~]# du -a  查看目录大小
[root@localhost tmp]# du -a
4     ./pulse-niRveYndCUNc
0     ./dy/index.php
4     ./dy/a
8     ./dy
...

[root@localhost tmp]# du -ah  以可识别的单位来显示磁盘文件的大小
4.0K  ./pulse-niRveYndCUNc
0     ./dy/index.php
4.0K  ./dy/a
8.0K  ./dy
4.0K  ./ks-script-2Ru861.log
4.0K  ./virtual-
...

以上命令显示的包括目录中的文件

[root@localhost tmp]# du -s  列出总大小
516   .
[root@localhost tmp]# du -sh  h是以可识别的单位表示
516K  

[root@localhost tmp]# du -shS   仅查看当前目录的大小，不包括子目录

[root@localhost tmp]# df  查看分区

[root@localhost tmp]# df -h   以可识别的单位来显示分区大小
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        18G  2.6G   14G  16% /
tmpfs           491M  228K  491M   1% /dev/shm
/dev/sda1       283M   34M  234M  13% /boot

[root@localhost tmp]# sync  将内存的数据同步到磁盘中，在关闭之前要多执行

[root@localhost tmp]# fdisk -l  查看分区结构，fdisk命令

init 0    也可以关机

linux磁盘要分区挂载才能使用

[root@bogon Desktop]# ls /dev  查看磁盘文件夹

[root@bogon Desktop]# fdisk /dev/sdb    sdb磁盘分区，一定要确定是那块硬盘分区，以避免其他硬盘被格式化

Command (m for help): n   根据m提示出的帮助来操作，n为添加一个新的分区
Command action
   e   extended        扩展分区
   p   primary partition (1-4)    主分区，最多只能添加4个

p          添加主分区
Partition number (1-4): 1      添加1号主分区
First cylinder (1-391, default 1):    选择开始位置，新盘就选择默认，回车即可
Using default value 1
Last cylinder, +cylinders or +size{K,M,G} (1-391, default 391): +1G    选择分区大小，可以使用kmg来表示

Command (m for help): n     添加第二号分区
Command action
   e   extended
   p   primary partition (1-4)
p                           添加主分区
Partition number (1-4): 2     分区号为2,1已经被占用
First cylinder (133-391, default 133):     开始位置，选择默认
Using default value 133
Last cylinder, +cylinders or +size{K,M,G} (133-391, default 391):   选择默认大小即表示将剩下的所有分给2分区
Using default value 391

Command (m for help):  m   查看帮助
Command (m for help): p     表示打印分分区表，m提示由此功能

Disk /dev/sdb: 3221 MB, 3221225472 bytes
255 heads, 63 sectors/track, 391 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xc4a6922b

   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         132     1060258+  83  Linux    分区1
/dev/sdb2             133         391     2080417+  83  Linux    分区2
分区后不能使用，需要格式化才能用（添加了文件系统）

Command (m for help): d    删除分区

Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
e                   添加扩展分区
Partition number (1-4): 3
First cylinder (198-391, default 198): 
Using default value 198
Last cylinder, +cylinders or +size{K,M,G} (198-391, default 391): 
Using default value 391

打印分区情况
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         132     1060258+  83  Linux
/dev/sdb2             133         197      522112+  83  Linux
/dev/sdb3             198         391     1558305    5  Extended

Command (m for help): n
Command action
   l   logical (5 or over)            将剩余空间分给扩展分区后在分区就只能分主分区和逻辑分区
   p   primary partition (1-4)

分逻辑分区
Command (m for help): n
Command action
   l   logical (5 or over)
   p   primary partition (1-4)
l
First cylinder (198-391, default 198): 
Using default value 198
Last cylinder, +cylinders or +size{K,M,G} (198-391, default 391): +500M

打印分区情况5和6为逻辑分区
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         132     1060258+  83  Linux
/dev/sdb2             133         197      522112+  83  Linux
/dev/sdb3             198         391     1558305    5  Extended
/dev/sdb5             198         262      522081   83  Linux
/dev/sdb6             263         391     1036161   83  Linux

只有主分区和逻辑分区才能使用
逻辑分区从5开始，因为1-4被占位主分区

   w   write table to disk and exit
   x   extra functionality (experts only)

Command (m for help): w    写入分区到磁盘
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

fdisk -l  查看分区即可以看到刚才做的分区 
   Device Boot      Start         End      Blocks   Id  System
/dev/sdb1               1         132     1060258+  83  Linux
/dev/sdb2             133         391     2080417+   5  Extended
/dev/sdb5             133         197      522081   83  Linux
/dev/sdb6             198         391     1558273+  83  Linux

创建文件系统/格式化
[root@bogon Desktop]# mkfs -t ext4 /dev/sdb1   格式化sdb1分区

[root@bogon Desktop]# mkfs   查看mkfs的帮助
Usage: mkfs [-V] [-t fstype] [fs-options] device [size]

手动挂载
[root@bogon Desktop]# ls /mnt/   这个是linux通用的挂载区

[root@bogon Desktop]# mount  查看挂载详情
/dev/sda2 on / type ext4 (rw)    sda2挂载了第一块硬盘的第二个分区在根目录下，所有对根目录的操作都是对这个分区的操作
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw,rootcontext="system_u:object_r:tmpfs_t:s0")
/dev/sda1 on /boot type ext4 (rw)    同理这个挂在了boot目录下，是ext4的文件系统
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
vmware-vmblock on /var/run/vmblock-fuse type fuse.vmware-vmblock (rw,nosuid,nodev,default_permissions,allow_other)

[root@bogon ~]# mkdir /mnt/sdb1   挂载就是创建一个目录，将分区分配到这个目录，就是将这个目录作为分区的操作空间，类似win的def盘，这个目录名随意起

[root@bogon ~]# mount /dev/sdb1 /mnt/sdb1    实现挂载，将sdb1分区挂载到目录sdb1

[root@bogon ~]# cd /mnt/sdb1 此时该分区就可以使用了，通过这目录的操作实际就是对分区的操作
[root@bogon sdb1]# ll

[root@bogon sdb1]# mount  此时可以看到挂载了分区

[root@bogon ~]# e2label /dev/sdb1 web   给/dev/sdb1起一个卷标web

[root@bogon ~]# e2label /dev/sdb1  打印卷标，此时即使硬盘在电脑中随意摆放也不会乱了

[root@bogon ~]# umount /dev/sdb1    弹出sdb1的挂载

[root@bogon ~]# mount  此时在查看时就没有挂载了

[root@bogon ~]# mount -L "web" /web    使用卷标来挂载，使用关键字 -L 

扩展分区不用挂载

[root@bogon ~]# df -h   这里可以看到已经可用的磁盘
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        18G  2.6G   14G  16% /
tmpfs           491M  248K  491M   1% /dev/shm
/dev/sda1       283M   34M  234M  13% /boot
/dev/sdb1       988M  1.3M  935M   1% /web

[root@bogon ~]# df -h    全部挂载完成
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        18G  2.6G   14G  16% /
tmpfs           491M  248K  491M   1% /dev/shm
/dev/sda1       283M   34M  234M  13% /boot
/dev/sdb1       988M  1.3M  935M   1% /web
/dev/sdb5       486M  2.3M  458M   1% /backup
/dev/sdb6       1.5G  2.3M  1.4G   1% /soft

还需要一步操作，使得电脑启动时自动挂载
修改配置文件/ect/fstab,使用vim编辑即可，要小心操作

proc                    /proc                   proc    defaults        0 0
/dev/sdb1               /web                    ext4    defaults        0 2
添加下面的一句即挂载

[root@bogon Desktop]# tail -1 /etc/fstab  查看文件内容最后一行

/dev/sdb1               /web                    ext4    defaults        0 2
/dev/sdb5               /backup                 ext4    defaults        0 0
LABEL=soft              /soft                   ext4    defaults        0 0
上面的最后一行时以卷标形式挂载，注意卷标名唯一



忘记root密码就要进入单用户模式来修改查看,单用户模式只能在服务器上操作
passwd root
输入新的密码
重启即可

mount -n -o reount,rw /     重新挂载根目录并使其可写(在单用户只能读取文件时可以这样操作)

#12 压缩文件
体积变小  容易复制

[root@bogon backup]# zip passwd.zip passwd   将passwd压缩为passwd.zip，linux没有rar，因为该软件搜费

[root@bogon www]# unzip passwd.zip  解压缩

[root@bogon backup]# gzip index.php  使用gzip压缩index.php文件 

[root@bogon backup]# gzip -d index.php.gz  将文件解压缩

[root@bogon backup]# bzip2 shadow   使用bzip2压缩文件

[root@bogon backup]# bzip2 -d shadow.bz2   解压缩
以上方法仅能压缩单个文件

tar  打包
参数 ：
   -j 使用bzip2进行打包
   -z 使用gzip进行打包
   -f 设置文件名
   -c 新建打包文件
   -v 显示执行过程
   -x 解包
   -t 查看压缩包内的内容，不会解包

[root@bogon www]# tar -zcvf admin.gz admin  将文件夹打包，使用gzip,新建打包文件，命名打包文件，显示打包过程

[root@bogon test]# tar -zxvf /tmp/www/admin.gz   x 是解包

[root@bogon www]# tar -ztvf admin.gz  查看压缩包内的内容 


-rw-r--r--. 1 root root 7947148 Jun 17 20:06 daiyan9095.tar.bz2
drwxr-xr-x. 3 root root    4096 Jun 17 20:07 home
-rw-r--r--. 1 root root       0 Jun 17 19:39 index.php
-rw-r--r--. 1 root root    1441 Jun 17 19:28 passwd
-rw-r--r--. 1 root root     753 Jun 17 19:30 passwd.zip
----------. 1 root root     827 Jun 17 19:44 shadow
[root@bogon backup]# cd home
[root@bogon home]# ll
total 4
drwx------. 30 daiyan9095 daiyan9095 4096 Jun 17 19:15 daiyan9095

tar解压缩并不会删除压缩包

vim
i插入模式，可以更改写入

esc键为返回一般模式

退出：
: 命令模式
q 直接退出
w 保存写入的信息

在vim编辑器内发出命令:set nu  显示行号,:set nonu 不显示行号
  1 <?php
  2 class IndexControl extends Control{
  3         function index(){
  4 
  5 }
  6 }
  7 ?>


在普通模式下快速移动，并立即切换到编辑模式
i  在当前位置插入
I  在行首插入
a  下一个字符
A  行尾插入
o  下一行
O  上一行 

:sh执行命令，将vim放入后台 
exit后右退回到vim编辑器

:w!强制保存
:q!强制退出
:w user.control.class.php  另存为user.control.class.php 
x 删除一个字符
#15 
vim 编辑命令
:set tapstop=2 设置tab空格为两个字符
:2 跳转到第二行
:100 跳转到100行
:0  调到最开始
:20000很大的数组则调到最后
:/查找内容   向下查找
   :n 和:N来向下和向上查找

:?查找内容 向上查找
                                                                        
:1,10s/e/p/g  从第一行到10行替换(s)，将e换为p，g表示执行全部替换

直接按u是撤销的意思

:1,10s/e/p/gc  每次替换都需要确定，以免出错
dd剪切当前行
yy复制
p是粘贴到当前光标下一行
P粘贴到上一行

按出12 然后按dd则从当前光标及之下的12行被剪切

按出3，然后按yy则复制当前光标及之下的3行

:r IndexCtrol.class.php  导入另一个文件中的数据

:sp  打开一个新的空窗口

:wq!强制关闭一个窗口

:sp IndexControl.class.php 在新的窗口中打开IndexControl.class.php

ctrl+ww在多个窗口之间进行切换

:set autoindent 设置自动缩进
以上操作仅影响到当前的文件

要想影响到所有的文件，在用户家目录下，建立新的文件.vimrc,编辑内容
set nu
set autoindent
set tabstop=2
保存退出
这时用vim打开任何文件都带有了配置


#17 

/etc/passwd文件
daiyan9095:x:500:500:centos:/home/daiyan9095:/bin/bash
用户名   x代表密码 500为id 500为组的id home/daiyan9095为家目录  

创建账号bjhd
[root@bogon backup]# useradd bjhd
查看/etc/passwd的最后一行
[root@bogon backup]# tail -1 /etc/passwd
bjhd:x:501:501::/home/bjhd:/bin/bash

这个文件中的字段用:隔开

现在的用户密码不存在passwd里了，而是存在了/etc/shadow中 
[root@bogon backup]# tail -1 /etc/shadow
bjhd:!!:16970:0:99999:7:::

为用户bjhd添加密码admin888
[root@bogon backup]# passwd bjhd
Changing password for user bjhd.
New password: 
BAD PASSWORD: it is based on a dictionary word
Retype new password: 
passwd: all authentication tokens updated successfully.

此时密码做了更改：
[root@bogon backup]# tail -1 /etc/shadow
bjhd:$1$UlfrA.xc$30M5ZIl5fWJxX84/D8k.W0:16970:0:99999:7:::
16970表示设置密码的事件unix的天数，0表示随时可以再更改密码需要的时间，
若为2表示需要2天后才能更改密码，当然root不受此限制
99999表示99999天后必须修改密码，否则登录不了
7表示到期前7天会提醒用户修改密码
后面的参数设置即使过期了也可以在指定天数内修改


#用户高级管理
[root@bogon backup]# more /etc/group  查看管理用户组的文件

daiyan9095:x:500:
bjhd:x:501:
第一个参数为组名，第二个参数为组密码 第三个参数501为组id
如果还有参数则是组的成员
初始组即用户即为一个组则不显示

[root@bogon backup]# more /etc/gshadow   查看组的密码

daiyan9095:!::
bjhd:!::
！表示没有密码
第一个参数为组名，第二个参数为组的密码，第三个参数为组的管理员，第四个参数为组的成员

[root@bogon backup]# ls /home
bjhd  daiyan9095   添加完用户后会在home下自动创建这个用户的家目录

[root@bogon backup]# useradd u1
[root@bogon backup]# ls /home
bjhd  daiyan9095  u1

u1:x:502:502::/home/u1:/bin/bash   同时在passwd文件中添加了用户的信息学

cat /etc/group  下也会创建组
bjhd:x:501:
u1:x:502:

[root@bogon backup]# groupadd hd  创建一个hd的组
cat /etc/group   查看新建的组
u1:x:502:
hd:x:503:

[root@bogon backup]# useradd -g hd u2  新添加一个用户u2并指定组为hd
[root@bogon backup]# tail -2 /etc/passwd
u1:x:502:502::/home/u1:/bin/bash
u2:x:504:503::/home/u2:/bin/bash
[root@bogon backup]# tail -1 /etc/group
hd:x:503:

[root@bogon backup]# useradd -G hd xiaobai  添加附加组，这时小白属于自己的组合hd组

[root@bogon backup]# id xiaobai  查看小白用户的id
uid=504(xiaobai) gid=504(xiaobai) groups=504(xiaobai),503(hd)
可以看到小白的组属于自己和hd

[root@bogon test]# chgrp hd hd1  更改hd1的用户组为hd
[root@bogon test]# ll
total 12
drwxr-xr-x. 2 daiyan9095 daiyan9095 4096 Jun 17 13:05 admin
drwxr-sr-x. 2 root       hd         4096 Jun 17 23:44 hd  此时组变为hd
-rw-r--r-x. 1 root       root         64 Jun 17 21:17 index.php

[root@bogon test]# chown root:root hd  改变index.php的所有者和所有组 

chgrp hd hdddd  仅改变所有组为hd

[root@bogon test]# chmod g+w hd  为hd的所有组添加w权限


[xiaobai@bogon test]$ cd hd  此时xiaobai可以在hd下创建文件
[xiaobai@bogon hd]$ ll
total 0
-rw-rw-r--. 1 xiaobai hd 0 Jun 17 23:52 hdphp
[xiaobai@bogon hd]$ touch dd

[u1@bogon test]$ cd hd   u1就创建不了，每有操作的权限
[u1@bogon hd]$ touch hehe
touch: cannot touch `hehe': Permission denied


[root@bogon hd]# useradd -G hd,u1 h6 创建新的用户u6并添加多个附加组
[root@bogon hd]# id h6
uid=505(h6) gid=505(h6) groups=505(h6),502(u1),503(hd)

[root@bogon hd]# useradd -M u7  创建u7但不创建家目录
[root@bogon hd]# ls /home
bjhd  daiyan9095  h6  u1  u2  xiaobai

修改用户的信息
[root@bogon hd]# usermod -G hd h6  修改h6的组为hd和自身
[root@bogon hd]# id h6
uid=505(h6) gid=505(h6) groups=505(h6),503(hd)

[root@bogon hd]# usermod -L h6   锁定用户
此时/etc/shadow下的对应行密码前多了一个！
h6:!$1$SNnLzR.X$v6/epl4dsDuarfoakGwcx0:16970:0:99999:7:::

[root@bogon hd]# usermod -U h6  为用户解锁
此时相应的!也没了
h6:$1$SNnLzR.X$v6/epl4dsDuarfoakGwcx0:16970:0:99999:7:::

用户锁定后就不能登陆了

删除用户
[root@bogon hd]# userdel u1
[root@bogon hd]# ls /home  但是该用户在home下的文件没有删除
bjhd  daiyan9095  h6  u1  u2  xiaobai

[root@bogon hd]# userdel -r u2  此时连同家目录一起删除
[root@bogon hd]# ls /home
bjhd  daiyan9095  h6  u1  xiaobai


删除没有所有者的目录
[root@bogon hd]# find / -nouser  全盘搜索没有所有者的文件

[root@bogon hd]# find / -nouser -exec rm -rf {} \; 查找并执行删除操作

[root@bogon hd]# find / -nouser -exec rm -ri {} \;  连续确定是否删除
{}就代表找到的文件

root可以更改任何用户的密码 

其他用户只能更改自己的密码

[root@bogon hd]# passwd -l bjhd  也可以用来锁定用户
此时在shadow密码前加两个!!
[root@bogon hd]# passwd -u bjhd  解除锁定

[root@bogon hd]# passwd -S bjhd  查看状态
bjhd PS 2016-06-17 0 99999 7 -1 (Password set, MD5 crypt.)

修改用户信息
[root@bogon hd]# chage -l bjhd
Last password change                            : Jun 18, 2016
Password expires                          : never
Password inactive                         : never
Account expires                                 : never
Minimum number of days between password change        : 0
Maximum number of days between password change        : 99999
Number of days of warning before password expires     : 7


[root@bogon hd]# chage -m 3 bjhd  修改了需要3天后才可以修改密码
[root@bogon hd]# chage -l bjhd
Last password change                            : Jun 18, 2016
Password expires                          : never
Password inactive                         : never
Account expires                                 : never
Minimum number of days between password change        : 3
Maximum number of days between password change        : 99999
Number of days of warning before password expires     : 7

[root@bogon hd]# chage -M 10 bjhd 设置10天后必须修改密码
[root@bogon hd]# chage -l bjhd
Last password change                            : Jun 18, 2016
Password expires                          : Jun 28, 2016
Password inactive                         : never
Account expires                                 : never
Minimum number of days between password change        : 3
Maximum number of days between password change        : 10
Number of days of warning before password expires     : 7

[root@bogon hd]# chage -W 9 bjhd  修改9天之前必须提醒我
[root@bogon hd]# chage -l bjhd
Last password change                            : Jun 18, 2016
Password expires                          : Jun 28, 2016
Password inactive                         : never
Account expires                                 : never
Minimum number of days between password change        : 3
Maximum number of days between password change        : 10
Number of days of warning before password expires     : 9

#18 

[root@bogon test]# chmod 0777 index.php  更改文件的权限
0777中的0代表特殊权限位

[root@bogon test]# passwd --help 查看某个命令的帮助

[root@bogon test]# man passwd  查询更加详细的帮助信息

查看passwd命令所在的位置，which whereis  find也可以  locate
[root@bogon test]# which passwd
/usr/bin/passwd
[root@bogon test]# whereis passwd  
passwd: /usr/bin/passwd /etc/passwd /etc/passwd.OLD /usr/share/man/man5/passwd.5.gz /usr/share/man/man1/passwd.1.gz

which 和 whereis 专门找命令地址的


[root@bogon test]# ls -l /usr/bin/passwd 
-rwsr-xr-x. 1 root root 30768 Nov 23  2015 /usr/bin/passwd
这个命令文件是rws，s代表拥有suid的权限位
这个s使得当其他用户拥有执行权限即x时，在执行该文件时会临时转换为root执行命令


[root@bogon test]# ls -l /etc/shadow
----------. 1 root root 938 Jun 18 00:50 /etc/shadow
密码文件其他任何用户没有权限操作，只有root能改

chmod 4755 index.php  将index.php的权限改为 
-rwsr-xr-x  这里的index.php必须是可执行文件不能是目录，而且要有操作该文件的权限

[root@bogon test]# chmod 4755 index.php
[root@bogon test]# ll
total 12
drwxr-xr-x. 2 daiyan9095 daiyan9095 4096 Jun 17 13:05 admin
drwxrwsr-x. 2 root       hd         4096 Jun 17 23:55 hd
-rwsr-xr-x. 1 root       root         84 Jun 18 02:10 index.php


sgid 当执行文件时变为文件的所有者，类似suid,可以对目录操作
[root@bogon test]# chmod 2755 hd
[root@bogon test]# ll
total 12
drwxr-xr-x. 2 daiyan9095 daiyan9095 4096 Jun 17 13:05 admin
drwxr-sr-x. 2 root       hd         4096 Jun 17 23:55 hd
-rwxr-xr-x. 1 root       root         84 Jun 18 02:10 index.php

也可以单独设置：
  chmod g+s hd
表示当我在占整个文件夹下操作时自动变为hd组
2770的2代表sgid


[xiaobai@bogon hd]$ touch hh
[xiaobai@bogon hd]$ ll
total 0
-rw-rw-r--. 1 xiaobai hd 0 Jun 17 23:55 dd
-rw-rw-r--. 1 xiaobai hd 0 Jun 17 23:52 hdphp
-rw-rw-r--. 1 xiaobai hd 0 Jun 18 02:27 hh  这时虽然是xiaobai创建的文件，但是组却会变为hd

[root@bogon hd]# groupadd blog  增加blog组

[root@bogon test]# chgrp blog Application/
[root@bogon test]# ll
total 16
drwxr-xr-x. 2 daiyan9095 daiyan9095 4096 Jun 17 13:05 admin
drwxr-sr-x. 2 root       blog       4096 Jun 18 02:31 Application
drwxrwsrwx. 2 root       hd         4096 Jun 18 02:27 hd
-rwxr-xr-x. 1 root       root         84 Jun 18 02:10 index.php


[root@bogon test]# useradd liu
[root@bogon test]# useradd li
[root@bogon test]# useradd wnag
[root@bogon test]# userdel -r wnag
[root@bogon test]# ls /home
bjhd  daiyan9095  li  liu  xiaobai
[root@bogon test]# useradd wang
[root@bogon test]# usermod -G blog liu
[root@bogon test]# id liu
uid=507(liu) gid=508(liu) groups=508(liu),507(blog)


[root@bogon test]# usermod -G blog wang  这个命令是附加组，原有组不变 
chgrp 组 用户 这个是更改组


[liu@bogon Application]$ touch liu.html
[liu@bogon Application]$ ll
total 0
-rw-rw-r--. 1 liu blog 0 Jun 18 02:58 liu.html  此时的liu.html文件自动变为blog组
[liu@bogon Application]$ 


[li@bogon Application]$ vim liu.html   属于一个组的用户可以修改组文件


-rw-rw-r-t如果目录设置了t，则所有在这之下的文件只能被创建者删除，其他用户不能删除


drwxr-xr-x. 2 root       root       4096 Jun 18 03:10 sbit
[root@bogon test]# chmod 1777 sbit  设置t属性
drwxrwxrwt. 2 root       root       4096 Jun 18 03:10 sbit
1777中的1代表sbit，目录下的文件只能被创建者删除（不考虑root）
也可以chmod o+t sbit 

drwxrwxrwt. 2 root       root       4096 Jun 18 03:10 sbit
-rwxrwxrwx. 1 liu liu 29 Jun 18 03:15 liu.css
[li@bogon sbit]$ rm liu.css  即使对该目录有w权限，但是不能删除
rm: cannot remove `liu.css': Operation not permitted

[root@bogon sbit]# su liu 
[liu@bogon sbit]$ rm liu.css 只能由创建者删除

能不能删文件要看对目录的是否有w权限和是否设置了t属性


ACL 

[root@bogon test]# setfacl -m u:liu:rwx acl  设置acl,使得li对acl文件目录rwx
[root@bogon test]# getfacl acl
# file: acl
# owner: li
# group: li
user::rwx
user:liu:rwx  这就是增加的权限
group::r-x
mask::rwx
other::r-x

其他文件都能获得这个性质
[root@bogon test]# getfacl admin
# file: admin
# owner: daiyan9095
# group: daiyan9095
user::rwx
group::r-x
other::r-x

给指定组设置特殊权限
[root@bogon test]# setfacl -m g:blog:rwx acl
[root@bogon test]# getfacl acl
# file: acl
# owner: li
# group: li
user::rwx
user:liu:rwx
group::r-x
group:blog:rwx
mask::rwx
other::r-x

以上的acl设置要受到mask这个值得影响
[root@bogon test]# setfacl -m m:rwx acl  设置mask的权限


#19 

su - 也是切换到root，这时同时改变了环境变量

sudo 临时切换用户并执行命令

[root@bogon root]$ vim /etc/sudoers  设置sudo需要修改该文件
在这个文件中配置文件，赋予其他用户某些root功能


锁定用户的方法：
   1 passwd -l 
   2 usermod -L 
   3 修改/etc/shadow 下的密码加上!

halt也是关机

推荐使用visudo修改/etc/sudoers文件

     90 ## Allow root to run any commands anywhere
     91 root  ALL=(ALL)   ALL
     92 daiyan9095 ALL=(ALL) ALL  加上这一行表示从任何位置登陆的daiyan9095账号，可以却换为任何用户，可以执行任何操作；这三个属性分别对应三个all

ctrl+shift+t 打开新的标签

[daiyan9095@bogon ~]$ vim /etc/shadow  这样查看没有哦权限

[daiyan9095@bogon ~]$ sudo vim /etc/shadow  这样就能查看了

此时只要在命令最前方加上sudo则daiyan9095账号几乎与root的权限一样了

[daiyan9095@bogon ~]$ useradd a2
bash: /usr/sbin/useradd: Permission denied
[daiyan9095@bogon ~]$ sudo useradd a2
[daiyan9095@bogon ~]$ tail -1 /etc/passwd
a2:x:510:511::/home/a2:/bin/bash
[daiyan9095@bogon ~]$ userdel a2
bash: /usr/sbin/userdel: Permission denied
[daiyan9095@bogon ~]$ sudo userdel -r a2
[daiyan9095@bogon ~]$ ls /home
bjhd  daiyan9095  li  liu  wang  xiaobai


[daiyan9095@bogon ~]$ sudo -u xiaobai ls /home  切换为xiaobai账号执行某一命令

[daiyan9095@bogon ~]$ sudo -u root ls ~

ctrl+pageup/pagedown 切换标签


:!which cat 编辑状态下临时执行一条命令 

 91 root  ALL=(ALL)   ALL
92 daiyan9095 ALL=(root)   /bin/cat /etc/shadow
增加92行使得从任何途径（网络远程，本地）的daiyan9095账号都可以却换到root账号，只能执行root的cat 命令(该命令在/bin/cat下)，且只能查看/etc/shadow文件

[daiyan9095@bogon home]$ sudo useradd a7
Sorry, user daiyan9095 is not allowed to execute '/usr/sbin/useradd a7' as root on bogon.
此时的daiyan9095已经不能执行此条命令了

[daiyan9095@bogon home]$ cat /etc/shadow
cat: /etc/shadow: Permission denied
[daiyan9095@bogon home]$ sudo cat /etc/shadow
只能通过sudo查看/etc/shadow文件

92 daiyan9095 ALL=(root)   /bin/cat /etc/shadow,/sbin/shutdown -h now
一次添加多个命令，命令要用绝对路径 使用which 命令名 查看命令的绝对路径





/usr/sbin/useradd
92 hd_stu_1 ALL=(root)   /usr/sbin/useradd
给hd_stu_1赋予添加用户命令
[root@bogon ~]# id zxg
uid=511(zxg) gid=512(zxg) groups=512(zxg)

[root@bogon ~]# id hd_stu_1
uid=510(hd_stu_1) gid=511(hd_stu_1) groups=511(hd_stu_1)

编辑sudo文件用visudo,因为这个有提示

passwd可以读取而shadow不能随意读取

91 root  ALL=(ALL)   ALL
92 #hd_stu_1 ALL=(root)    /usr/sbin/useradd,!/usr/bin/passwd,/usr/bin/pass    wd [a-zA-Z]*,!/usr/bin/passwd root
！表示不能执行某命令，可以使用正则表达式来匹配
加上该项!/usr/bin/passwd是因为sudo passwd 默认切换为root的密码更改


91 Cmnd_Alias MODIFYUSERPASSWD = /sbin/shutdown -h now,!/usr/bin/passwd,/us
        r/bin/passwd [a-zA-Z]*,!/usr/bin/passwd root
92 root  ALL=(ALL)   ALL
93 hd_stu_1 ALL=(root)   MODIFYUSERPASSWD
通过别名设置hd_stu_1的sudo权限，这时仍可以执行

[hd_stu_1@bogon Desktop]$ passwd liu
passwd: Only root can specify a user name.
[hd_stu_1@bogon Desktop]$ sudo passwd liu
[sudo] password for hd_stu_1: 
Changing password for user liu.
New password: 
BAD PASSWORD: it is based on a dictionary word
Retype new password: 
passwd: all authentication tokens updated successfully.
[hd_stu_1@bogon Desktop]$ sudo passwd root
Sorry, user hd_stu_1 is not allowed to execute '/usr/bin/passwd root' as root on bogon.
[hd_stu_1@bogon Desktop]$ sudo passwd
Sorry, user hd_stu_1 is not allowed to execute '/usr/bin/passwd' as root on bogon.


还可以将多个用户存入一个别名，给这个别名设置sudo权限
     91 User_Alias ADMIN = cl_zhangsan,cl_lisi,hd_stu_1
     92 Cmnd_Alias MODIFYUSERPASSWD = /sbin/shutdown -h now,!/usr/bin/passwd,/us  r/bin/passwd [a-zA-Z]*,!/usr/bin/passwd root 
     93 root  ALL=(ALL)   ALL
     94 ADMIN=(root)    MODIFYUSERPASSWD

将用户cl_zhangsan,cl_lisi,hd_stu_1存入别名ADMIN要大写别名
然后设置命令的别名
然后设置sudo权限

[root@bogon Desktop]# visudo
[root@bogon Desktop]# su hd_stu_1
[hd_stu_1@bogon Desktop]$ passwd cl_zhangsan
passwd: Only root can specify a user name.
[hd_stu_1@bogon Desktop]$ sudo passwd cl_zhangsan
[sudo] password for hd_stu_1: 
Changing password for user cl_zhangsan.
New password: 
BAD PASSWORD: it is based on a dictionary word
Retype new password: 
passwd: all authentication tokens updated successfully.

利用张三的改李四的
[hd_stu_1@bogon Desktop]$ su cl_zhangsan
Password: 
[cl_zhangsan@bogon Desktop]$ passwd cl_lisi
passwd: Only root can specify a user name.
[cl_zhangsan@bogon Desktop]$ sudo passwd cl_lisi

We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for cl_zhangsan: 
Changing password for user cl_lisi.
New password: 
BAD PASSWORD: it is based on a dictionary word
Retype new password: 
passwd: all authentication tokens updated successfully.




















































































=============设置网络=================


