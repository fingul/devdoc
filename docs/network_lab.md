 1084  sudo nano /etc/sysconfig/network-scripts/ifcfg-br0

DEVICE=br0
TYPE=Bridge
IPADDR=192.168.0.201
PREFIX=24
BOOTPROTO=none
ONBOOT=yes
DELAY=0

 1085  h
 1086  sudo systemctl restart network
