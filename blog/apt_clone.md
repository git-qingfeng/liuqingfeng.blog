# Apt-clone可以帮你做如下工作：

- 在Ubuntu系操作系统的多个系统中安装完全一致的应用程序。
- 在多个系统上安装同一组软件包。
- 备份所有已安装的应用程序，并根据需要随时恢复它们。

在这个简短的指南中，我们将讨论如何在基于debian的系统上安装和使用Apt-clone。我在Ubuntu18.04 LTS系统上测试了这个实用程序，但是它应该可以在所有基于Debian和Ubuntu的系统上工作。

**备份已安装的包，并在新安装的Ubuntu系统上恢复它们**

在默认的软件存储库中就可以得到Apt-clone。要安装它，只需从终端输入以下命令:
```shell
$sudo apt install apt-clone
```
安装后，只需创建已安装包的列表，并将它们保存在您选择的任何位置。
```shell
$mkdir ~/mypackages

$sudo apt-clone clone ~/mypackages
```
上面的命令将我的Ubuntu系统中所有已安装的软件包保存在/mypackages目录下名为apt-clone-state-ubuntuserver.tar.gz的文件中。

要查看备份文件的详细信息，请运行:
```shell
$ apt-clone info mypackages/apt-clone-state-ubuntuserver.tar.gz 

Hostname: ubuntuserver Arch: amd64 Distro: bionic Meta: Installed: 516 pkgs (33 automatic) Date: Sat Sep 15 10:23:05 2018
```
如上所示，我的Ubuntu服务器上总共有516个包。

现在，将此文件复制到USB或外部驱动器上，然后复制到任何其他想要安装相同软件包的系统上。或者您也可以将备份文件传输到网络上的系统，使用以下命令安装包:
```shell
$sudo apt-clone restore apt-clone-state-ubuntuserver.tar.gz
```
请注意，此命令将覆盖现有的/etc/apt/sources.list并安装/删除软件包。记住了!另外，要确保目标系统和原来的操作系统版本相同。例如，如果源系统使用18.04LTS 64位运行，则目标系统也必须使用相同的版本。

如果您不想在系统上还原软件包，您可以简单地使用--destination/some/locationn选项将克隆解压到此目录。
```shell
$sudo apt-clone restore apt-clone-state-ubuntuserver.tar.gz--destination ~/oldubuntu
```
在这种情况下，上面的命令将备份文件保存在一个名为~/oldubuntu的文件夹中。

有关详细信息，请参阅帮助信息:
```shell
$apt-clone -h
```
或者,man手册:
```shell
$man apt-clone
```

以上!!
---
当我们在基于 Ubuntu/Debian 的系统上使用 ***apt-clone***，包安装会变得更加容易。如果你需要在少量系统上安装相同的软件包时，***apt-clone*** 会适合你。

如果你想在每个系统上手动构建和安装必要的软件包，这是一个耗时的过程。它可以通过多种方式实现，Linux 中有许多程序可用。我们过去曾写过一篇关于 Aptik 的文章。它是能让 Ubuntu 用户备份和恢复系统设置和数据的程序之一。

## 什么是 apt-clone？
a***pt-clone*** 能让你为 Debian/Ubuntu 系统创建所有已安装软件包的备份，这些软件包可以在新安装的系统（或容器）或目录中恢复。

该备份可以在相同操作系统版本和架构的多个系统上还原。

## 如何安装 apt-clone？
***apt-clone*** 包可以在 Ubuntu/Debian 的官方仓库中找到，所以，使用 apt 包管理器 或 apt-get 包管理器 来安装它。

使用 apt 包管理器安装 apt-clone。

$ sudo apt install apt-clone
使用 apt-get 包管理器安装 apt-clone。
```shell
$ sudo apt-get install apt-clone
```
## 如何使用 apt-clone 备份已安装的软件包？
成功安装 apt-clone 之后。只需提供一个保存备份文件的位置。我们将在 /backup 目录下保存已安装的软件包备份。

***apt-clone*** 会将已安装的软件包列表保存到 ***apt-clone-state-Ubuntu18.2daygeek.com.tar.gz*** 中。
```shell
$ sudo apt-clone clone /backup
```
我们同样可以通过运行 ls 命令来检查。
```shell
$ ls -lh /backup/
total 32K
-rw-r--r-- 1 root root 29K Apr 20 19:06 apt-clone-state-Ubuntu18.2daygeek.com.tar.gz
```
运行以下命令，查看备份文件的详细信息。
```shell
$ apt-clone info /backup/apt-clone-state-Ubuntu18.2daygeek.com.tar.gz
Hostname: Ubuntu18.2daygeek.com
Arch: amd64
Distro: bionic
Meta: libunity-scopes-json-def-desktop, ubuntu-desktop
Installed: 1792 pkgs (194 automatic)
Date: Sat Apr 20 19:06:43 2019
```
根据上面的输出，备份文件中总共有 1792 个包。

## 如何恢复使用 apt-clone 进行备份的软件包？
你可以使用任何远程复制程序来复制远程服务器上的文件。
```shell
$ scp /backup/apt-clone-state-ubunt-18-04.tar.gz Destination-Server:/opt
```
复制完成后，使用 apt-clone 执行还原。

使用以下命令进行还原。
```shell
$ sudo apt-clone restore /opt/apt-clone-state-Ubuntu18.2daygeek.com.tar.gz
```
请注意，还原将覆盖现有的 /etc/apt/sources.list 并安装/删除包。所以要小心。

如果你要将所有软件包还原到文件夹而不是实际还原，可以使用以下命令。
```shell
$ sudo apt-clone restore /opt/apt-clone-state-Ubuntu18.2daygeek.com.tar.gz --destination /opt/oldubuntu
```

[via]( https://www.2daygeek.com/apt-clone-backup-installed-packages-and-restore-them-on-fresh-ubuntu-system/)