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
$ apt-clone info mypackages/apt-clone-state-ubuntuserver.tar.gz Hostname: ubuntuserver Arch: amd64 Distro: bionic Meta: Installed: 516 pkgs (33 automatic) Date: Sat Sep 15 10:23:05 2018
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

以上。