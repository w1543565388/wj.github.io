+++  
title = 'Samba 相关'  
date = 2024-04-12T09:39:39Z  
draft = true  
+++

##### 1、安装
```
yum install -y samba samba-client samba-common
```
##### 2、创建文件作为共享文件夹
```
mkdir /hl
```
##### 3、编辑配置文件（/etc/samba/smb.conf）
``` /etc/samba/smb.conf
[global]
   workgroup = WORKGROUP
   server string = %h server (Samba, Ubuntu)
   dns proxy = no
   log file = /var/log/samba/log.%m
   max log size = 1000
   syslog = 0
   panic action = /usr/share/samba/panic-action %d
   server role = standalone server
   passdb backend = tdbsam
   obey pam restrictions = yes
   unix password sync = yes
   passwd program = /usr/bin/passwd %u
   passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
   pam password change = yes
   map to guest = bad user
   usershare allow guests = yes

[hl]
comment = hl
path = /hl
browseable = yes
writable = yes
create mode = 0777
directory mode = 0777
guest ok = yes
locking = no
```
##### 4、重启服务
```
systemctl restart smb
```