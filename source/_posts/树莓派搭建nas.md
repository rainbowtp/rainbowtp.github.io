---
title: 树莓派搭建nas
img: 
top: false
cover: false
coverImg: 'https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo/photo/7.jpg'
toc: true
mathjax: false
author: rainbow
date: 2020-04-17 02:32:34
password:
summary: 树莓派实现小型私有云服务
categories:
  - 工具书
tags:
  - 树莓派
---

# 树莓派搭建nas

## 配置
- 树莓派4b 2G版本
- 闪迪16G class10 sd卡
- 金士顿u盘 3.0 64GB
- 操作用的一台mac

## 实现思路及效果
利用samba搭建nas，u盘作为交换磁盘
最终传输速率约20mb/s

## 安装系统
1. 在[树莓派官网](https://www.raspberrypi.org/downloads/raspbian/)下载最新版的系统并解压
2. 下载官方推荐用于格式化sd卡的软件[SD Memory Card Formatter](https://www.sdcard.org/downloads/formatter/eula_mac/SDCardFormatterv5_Mac.zip)并安装，格式化sd卡
![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/格式化sd.png)
3. 在终端用df命令查看所有磁盘
![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/查看磁盘.png)
注意绿线画出来的，是我们sd卡的路径`/dev/disk2s1`记住,后面要用
4. 卸载磁盘，并写入镜像
卸载磁盘：
    ```bash
    sudo diskutil umount /dev/disk2s1
    ```
    出现以下提示说明操作成功
![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/卸载磁盘成功.png)
写入镜像：*将if后的path参数换成你的镜像地址*
    ```bash
    sudo dd bs=1m if=/Users/rainbow/Downloads/2020-02-13-raspbian-buster-lite.img of=/dev/rdisk2
    ```
    速度较慢，耐心等待直到出现以下提示，操作成功
    ![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/树莓派烧录成功.png)
5. ssh与wifi
打开boot盘（刚才刻录好的sd卡）到finder，在mac桌面目录下新建ssh空文件和wifi配置文件wpa_supplicant.conf，然后移动到boot盘
    ```bash
    cd Desktop && touch ssh && vi wpa_supplicant.conf
    ```
    在wpa_supplicant.conf中写入：
    ```bash
    country=CN
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    
    network={
    ssid="WiFi-A"
    psk="12345678"
    key_mgmt=WPA-PSK
    priority=1
    }
    ```
    参数说明：
    **ssid: wifi名称**
    **psk: wifi密码**
    **key_mgmt: wifi安全等级**
    **priority: 连接优先级，越大优先级越高**

6. 保存，推出boot盘，拔掉sd卡插入树莓派，开机
1. 连接到树莓派
树莓派默认用户名是`pi`,密码是`raspberry`，在你的wifi控制台查看树莓派的ip地址，终端输入
    ```bash
    ssh pi@your_ip
    ```
    来连接树莓派，信任该设备：`y`，输入密码： `raspberry`

## 挂载u盘
1. 插上u盘
树莓派的u盘必须挂载才可以使用，所以我们先查看设备路径
    ```bash
    sudo fdisk -l
    ```
    ![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/20200417004201.png)
    `/dev/sda`为我的U盘路径
2. 格式化U盘为ext4
安装ntfs-3g
    ```bash
    sudo apt-get install ntfs-3g
    ```
    格式化
    ```bash
    sudo mkfs.ext4 /dev/sda
    ```
3. 挂载
新建目录
    ```bash
    sudo mkdir /home/share
    ```
    将U盘挂载到该目录
    ```bash
    sudo mount /dev/sda /home/share
    ```
    为用户pi增加该目录的权限
    ```bash
    sudo mount -o uid=pi,gid=pi /dev/sda /home/share
    ```
4. 开机自动挂载u盘
查看U盘的uuid
    ```bash
    sudo blkid
    ```
    编辑 sudo nano /etc/fstab 文件，在末尾加入以下内容
    ```bash
    UUID=994a070a-31c8-4c70-9662-0db1a5c1cd5f     /home/share   ext4  defaults   0   2
    ```

## 安装samba

1. 换源
备份
    ```bash
    sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
    sudo cp /etc/apt/sources.list.d/raspi.list /etc/apt/sources.list.d/raspi.list.bak
    ```
    清华源
    软件：
    ```bash
    deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
    deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi
    ```
    ```bash
    sudo nano /etc/apt/sources.list
    ```
    ![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/20200417002453.png)
    *Ctrl+o Enter Ctrl+x 保存退出*
    系统：
    ```bash
    deb http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
    deb-src http://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui
    ```
    ```bash
    sudo nano /etc/apt/sources.list.d/raspi.list
    ```
    ![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/树莓派换源2.png)
    *同上*
    更新源
    ```bash
    sudo apt update
    sudo apt upgrade
    ```
2. 安装samba
安装
    ```bash
    sudo apt-get install samba samba-common-bin
    ```
    *询问是否设为DHCP：NO*
    配置samba
    ```bash
    sudo nano /etc/samba/smb.conf
    ```
    在末尾加入如下内容
    ```bash
    # 分享名称
    [share]
        # 说明信息
        comment = NAS Storage
        # 要问我为啥多加了个 share，因为我把 ext4 格式的硬盘挂载在 /home/pi/share 下
        # ext4 文件系统会在根目录下产生 lost+found 文件夹，看着烦，就让它“消失了”（多加一层目录）
        # 共享文件的路径
        path = /home/pi/share/share
        # 可被其他人看到资源名称（非内容）
        browseable = yes
        # 可写
        writable = yes
        # 新建文件的权限为 664
        create mask = 0664
        # 新建目录的权限为 775
        directory mask = 0775
    ```
    为samba添加用户，必须是linux系统已经存在的用户，比如`pi`
    ```bash
    sudo smbpasswd -a pi
    ```
    启动samba
    ```bash
    sudo /etc/init.d/smbd restart

    sudo /etc/init.d/nmbd restart
    ```
    设置开机启动samba
    编辑/etc/rc.local,将`sudo /etc/init.d/smbd restart` `sudo /etc/init.d/nmbd restart`加入到`exit 0`之前

## 连线
大多数nas情况下nas传输速度受网络情况影响较大
将树莓派与路由器有线连接可以得到显著的改善

## 使用
打开finder-->前往-->连接服务器
![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/mac.png)
finder偏好设置里打开边栏显示 连接到的服务器
![](https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo//data/finder边栏.png)