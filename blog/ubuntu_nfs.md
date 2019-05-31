# 关于启动ubuntu中的nfs启动问题

## 嵌入式开发，如果使用nfs挂载来启动内核和文件系统，这样便于调试文件系统和驱动，则首先要保证ubuntu开启nfs服务，

###  执行以下命令安装nfs服务，安装后自动运行
``` shell
sudo apt-get install nfs-kernel-server
```
### 配置其配置文件
``` shell
sudo vi /etc/exports 在里面增加想要挂载的文件路径


11 /work/nfs_root *(rw,sync,no_root_squash)
12 /work/nfs_root/first_fs *(rw,sync,no_root_squash)
13 /work/kernel *(rw,sync,no_root_squash)
14 /work/nfs_root/fs_qtopia *(rw,sync,no_root_squash)
15 /work/system/u-bootbin *(rw,sync,no_root_squash)
16 / *
``` 
> 其中"*"表示所有客户机都可以访问（只要能通过网络访问到你）
> rw当然表示有读写权限（不要担心）
> no_root_squash表示客户机对此目录有root操作权限

这样就可以通过nfs服务来挂载nfs_root,kernel等目录下的所有文件；

### 配置完毕，可以重启NFS服务
``` shell
       sudo /etc/init.d/portmap restart      //nfs is a RPC service, portmap maps its port

       sudo /etc/init.d/nfs-kernel-server restart
```
   
- 查看NFS目录可以使用  ”showmount -e“ 命令

### 测试NFS服务是否开启成功

      在本机ubuntu（10.13.60.120）上挂载nfs目录到/mnt，（挂载未在/etc/exports里面添加的目录是无效的）

      sudo mount -t nfs 10.13.60.120:/home

      可以看到/mnt下已经有/home的内容了 ,卸载使用 umount /mnt命令即可

 

通常，为了能够正常使用NFS，还需要一些相关的服务来协同工作：
nfs：启动相应RPC服务进程来服务对于NFS文件系统的请求。
nfslock：一个可选的服务，用于启动相应的RPC进程，允许NFS客户端在服务器上对文件加锁。
portmap：Linux的RPC服务，它响应RPC服务的请求和与请求的RPC服务建立连接。

 

### 问题：当我把u-boot中关于nfs挂载参数设置好后，一直出现如下错误：
``` shell
Booting Linux ...
ERROR: resetting DM9000 -> not responding
dm9000 i/o: 0x20000000, id: 0x90000a46 
DM9000: running in 16 bit mode
MAC: 08:00:3e:26:0a:5b
could not establish link
File transfer via NFS from server 10.13.62.120; our IP address is 10.13.62.100
Filename '/work/kernel/uImage'.
Load address: 0x30007fc0
Loading: Timeout
## Booting image at 30007fc0 ...
Bad Magic Number

 ```

问题是这样解决的：因为我的ubuntu没有开启portmap功能
``` shell
sudo /etc/init.d/portmap restart 
```
开启后再重新启动nfs系统就可以正常挂载ubuntu中的内核