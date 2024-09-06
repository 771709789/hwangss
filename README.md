# hwangss

#####################################################################

创建实例CentOS 7 - 在高级选项 - 选择粘贴cloud-init脚本 - root密码rootpasswd

#!/bin/bash
echo root:rootpasswd |sudo chpasswd root
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config;
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config;
sudo reboot

#####################################################################

用户名
opc
获取root权限
sudo -i

#####################################################################

更新 yum
yum -y update

查看内核
uname -r
# 内核版本 3.10.0-1062.12.1.el7.x86_64

手动下载秋水 BBRPlus版内核
wget https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/bbrplus/centos/7/kernel-4.14.129-bbrplus.rpm

手动安装内核
yum -y install kernel-4.14.129-bbrplus.rpm

更新引导
grub2-mkconfig -o /boot/grub2/grub.cfg
grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg

列出系统开机启动项
sudo awk -F\' '$1=="menuentry " {print i++ " : " $2}' /boot/efi/EFI/centos/grub.cfg

设置新版内核默认启动项
grub2-set-default 0

重启
reboot

开启 BBRPlus 及优化
秋水一键脚本,选择7开启BBRPlus加速
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
再次./tcp.sh运行脚本,选择10优化并重启完成

检测 Bottleneck Bandwidth and RTT Plus 是否开启成功，输入
sysctl net.ipv4.tcp_available_congestion_control

如果返回值为：
net.ipv4.tcp_available_congestion_control = bbrplus cubic reno
则开启成功

#####################################################################

pcbind
使用netstat -ntlp命令发现rpcbind监听了111端口,如担心安全可执行以下命令卸载禁用:

systemctl stop rpcbind
systemctl stop rpcbind.socket
systemctl disable rpcbind
systemctl disable rpcbind.socket

oracle-cloud-agent
卸载甲骨文云官方后台监控程序

systemctl stop oracle-cloud-agent
systemctl disable oracle-cloud-agent
systemctl stop oracle-cloud-agent-updater
systemctl disable oracle-cloud-agent-updater

#####################################################################

执行v2ray一键安装脚本
https://github.com/233boy/v2ray/wiki/V2Ray%E6%90%AD%E5%BB%BA%E8%AF%A6%E7%BB%86%E5%9B%BE%E6%96%87%E6%95%99%E7%A8%8B

#####################################################################

https://hk.vless220924.top:19529/s/default/615d3c9ff7ef91fd9b3692a09c62b53b
#
https://1d7c93c3.no-mad-world.club/link/sjUd4EZygPeOTojI?shadowrocket=1
