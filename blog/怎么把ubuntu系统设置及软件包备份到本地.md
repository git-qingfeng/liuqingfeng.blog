# 备份软件
1. 在已经安装和配置好的电脑上，不要删除/var/cache/apt/archives目录，执行下面的命令，生成当前安装软件的内容列表
```shell
dpkg -–get-selections | grep -v deinstall > ubuntu.files
```
2. 把ubuntu.files和archives目录中的所有内容都cp到别的机器对应的目录。
3. 重装完成后，配置sources.list，执行如下命令
```shell
sudo apt-get update
sudo apt-get dist-upgrade
dpkg -–set-selections < ubuntu.files
sudo dselect
```
4. 按提示，按下 i，然后全部回车即可。
--------
# 备份系统
安装好Ubuntu之后，别忘了安装 for linux 防火墙和杀毒软件。
在备份系统前，请保证系统是无错和干净的：
本人操作系统是ubuntu14.04，不知道是系统出了问题还是装的软件有问题，每次开机都出现：System program problem detected 我初步感觉是显卡驱动的问题。
看着很心烦，关闭方法：
管理员权限打开/etc/default/apport
```shell
# set this to 0 to disable apport, or to 1 to enable it
# you can temporarily override this with
# sudo service apport start force_start=1
enabled=1
```
把原先的1改成0就可以了。

清理Ubuntu14.04的系统的垃圾：
先清空回收站，软件升级到最新。
Ubuntu系统与Windows系统所采用的文件系统不同， Ubuntu系统在使用或更新过程中不会产生文件碎片和垃圾文件，所以在使用 Ubuntu系统中不用考虑清理系统的文件垃圾和整理文件碎片。
如果你确实想去清理一下Ubuntu系统的话，那么请你参照下述方法去做吧：
1、按“Ctrl+Alt+T”，调出终端。
2、在终端输入下面的命令（复制到终端窗口即可）——按回车键——输入帐户密码——按回车键。
```shell
sudo apt-get autoclean（清理旧版本的软件缓存）
sudo apt-get clean（清理所有软件缓存）
sudo apt-get autoremove（删除系统不再使用的孤立软件）
```
在备份Windows系统的时候你可能想过，我能不能把整个C盘都放到一个ZIP文件里去呢。这在Windows下是不可能的，因为在Windows中有很多文件在它们运行时是不允许拷贝或覆盖的，因此你需要专门的备份工具对Windows系统进行特殊处理。
和备份Windows系统不同，如果你要备份Ubuntu系统(或者其它任何Linux系统)，你不再需要像Ghost这类备份工具。事实上，Ghost这类备份工具对于Linux文件系统的支持很糟糕，例如一些Ghost版本只能完善地支持Ext2文件系统，如果你用它来备份Ext3和Ext4文件系统，你可能会丢失一些宝贵的数据。

1. 备份系统
我该如何备份我的Ubuntu系统呢？很简单，就像你备份或压缩其它东西一样，使用TAR。和Windows不同，Linux不会限制root访问任何东西，你可以把分区上的所有东西都扔到一个TAR文件里去！
备份第一步：打开一个终端，并运行 sudo su（回车后要求输入密码）
第二步：继续在终端中输入 cd /(注意中间有一个空格)
第三步：（开始备份系统）
在终端中输入：
```shell
tar cvpzf Ubuntu.tgz –exclude=/proc –exclude=/lost+found –exclude=/Ubuntu.tgz –exclude=/mnt –exclude=/sys /
```
让我们来简单看一下这个命令：
'tar' 是用来备份的程序
c - 新建一个备份文档
v - 详细模式， tar程序将在屏幕上实时输出所有信息。
p - 保存许可，并应用到所有文件。
z - 采用‘gzip’压缩备份文件，以减小备份文件体积。
f - 说明备份文件存放的路径， Ubuntu.tgz 是本例子中备份文件名。
“/”是我们要备份的目录，在这里是整个文件系统。
在档案文件名“Ubuntu.gz”和要备份的目录名“/”之间给出了备份时必须排除在外的目录。有些目录是无用的，例如“/proc”、“/lost+ found”、“/sys”。当然，“Ubuntu.gz”这个档案文件本身必须排除在外，否则你可能会得到一些超出常理的结果。如果不把“/mnt”排 除在外，那么挂载在“/mnt”上的其它分区也会被备份。另外需要确认一下“/media”上没有挂载任何东西(例如光盘、移动硬盘)，如果有挂载东西， 必须把“/media”也排除在外。
有人可能会建议你把“/dev”目录排除在外，但是我认为这样做很不妥，具体原因这里就不讨论了。
执行备份命令之前请再确认一下你所键入的命令是不是你想要的。执行备份命令可能需要一段不短的时间。
备份完成后，在文件系统的根目录将生成一个名为“Ubuntu.tgz”的文件，它的尺寸有可能非常大。现在你可以把它烧录到DVD上或者放到你认为安全的地方去。
你还可以用Bzip2来压缩文件，Bzip2比gzip的压缩率高，但是速度慢一些。如果压缩率对你来说很重要，那么你应该使用Bzip2，用“j”代替命令中的“z”，并且给档案文件一个正确的扩展名“bz2”。完整的命令如下：
```shell
tar cvpjf Ubuntu.tar.bz2 –exclude=/proc –exclude=/lost+found –exclude=/Ubuntu.tar.bz2 –exclude=/mnt –exclude=/sys /
```
2. 恢复系统
切换到root用户，并把文件“Ubuntu.tgz”拷贝到分区的根目录下。
在 Linux中有一件很美妙的事情，就是你可以在一个运行的系统中恢复系统，而不需要用boot-cd来专门引导。当然，如果你的系统已经挂掉不能启动了，你可以用Live CD来启动，效果是一样的。
使用下面的命令来恢复系统：
```shell
tar xvpfz Ubuntu.tgz -C /
```
如果你的档案文件是使用Bzip2压缩的，应该用：
```shell
tar xvpfj Ubuntu.tar.bz2 -C /
```
注意：上面的命令会用档案文件中的文件覆盖分区上的所有文件。
参数x是告诉tar程序解压缩备份文件。 -C 参数是指定tar程序解压缩到的目录。( 在本例中是/ ），这会花一段时间。只需确保在你做其他任何事情之前，重新创建你剔除的目录： ( /proc, /lost+found, /mnt, /sys, 等等。)
```shell
mkdir /proc /lost+found /mnt /sys
#或者这样：
mkdir proc
mkdir lost+found
mkdir mnt
mkdir sys
```
执行恢复命令之前请再确认一下你所键入的命令是不是你想要的，执行恢复命令可能需要一段不短的时间。触类旁通，熟练以上操作后，对用户和部分升级文件进行定期备份，可以节省大量时间和提高安全性。