# ubuntu下用ethstatus可以监控实时的网卡带宽占用。
##  这个软件能显示当前网卡的 RX 和 TX 速率，单位是Byte
1. 安装 ethstatus 软件 
``` shell
sudo apt-get install ethstatus
```
2. 查看 ADSL 的速度 
``` shell
sudo ethstatus -i ppp0
```
3. 查看 网卡 的速度 
``` shell
sudo ethstatus -i eth0
```