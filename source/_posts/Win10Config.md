---
title: Win10Config
img: 'https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo/photo/3.jpg'
top: false
cover: false
coverImg: 'https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo/'
toc: true
mathjax: false
author: rainbow
date: 2020-08-28 14:38:37
password: 
summary: win10重装系统
categories: 系统
tags: 
    - win10 
    - scoop
---
# <center>win10 config</center>
## 系统

- 进入系统时不要联网，直接使用Microsoft账户会更改注册表文件，改回来很麻烦

- 数字激活
  [汉化版](https://github.com/TGSAN/CMWTAT_Digital_Edition/releases/tag/2.5.0.0)

- 更新系统
- 修改dns
    首选 8.8.4.4
    备选 114.114.114.114

- 磁盘分区 C系统：100g D软件:465g E文件:365g
  
    下载：E:\Downloads
    文档：E:\Documents
    
- 删除开始菜单冗余
  
    任务栏自动隐藏
    
- 分辨率

- 开始菜单主题色背景
    创建文件 20H2.reg 并写入以下内容:
    
    ```powershell
    Windows Registry Editor Version 5.00
        
    [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FeatureManagement\Overrides\0\2093230218]
        
    "EnabledState"=dword:00000002
        
    "EnabledStateOptions"=dword:00000000
    
    ```
    保存并执行，然后重启电脑
    
- 字体
  
    ```powershell
    git clone git@github.com:rainbowtp/fonts.git C:\Users\rainbow\Desktop\fonts
    ```
    
    下载苹方字体并安装，使用`MacType`进行替换
    字体显示-125% 显示-100% 桌面-查看-小图标 

## Office

- wps套件 a19678@myoffice.site
- onedrive rainbow@stu.xupt.edu.cn --> speedpanx v2ray
- 配置邮箱 pop3

## 网络

### proxy

v2ray -- fengchao

### speedpanX

填入激活码

### dns

[查找ip](https://www.ipaddress.com/)

```github.com```

``` github.global.ssl.fastly.net```

## 软件-scoop
安装Scoop，以管理员权限运行powershell
```powershell
Set-ExecutionPolicy UnRestricted # 给予powershell执行脚本的权限
$env:SCOOP='D:\scoop' # 自定义scoop安装路径
[environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')
iwr -useb get.scoop.sh | iex # 安装scoop
#  定制自己的bucket
##  参考[scoop官方文档](https://github.com/lukesampson/scoop/wiki/Buckets)
#设置http代理 在C:\Users\user\.config\scoop 查看
scoop config proxy 127.0.0.1:10809
```
# 安装配置git
```powershell
scoop install git
ssh-keygen -t rsa -C “1844283837@qq.com” # ssh密钥,连续敲三次Space
git config --global user.name "Rainbow"
git config --global user.email "1844283837@qq.com"
Get-Content C:\Users\rainbow\.ssh\id_rsa.pub > C:\Users\rainbow\Desktop\ssh_pub.txt # 复制填入github的ssh设置中
ssh git@github.com # 测试连接到github
# http代理
git config --global http.https://github.com.proxy socks5://127.0.0.1:10808 
# ssh代理
"Host github.com`n`tProxyCommand D:/scoop/apps/connect/1.100/connect.exe -S 127.0.0.1:10808 %h %p" | Out-File -Encoding utf8 C:\Users\rainbow\.ssh\config
# 完全放弃http协议，使用ssh协议，安全和速度都优于http
# eg： git clone git@github.com:rainbowtp/Scoop_bucket.git
```
配置aria2
```powershell
scoop config aria2-max-connection-per-server 16 ; scoop config aria2-split 16 ; scoop config aria2-min-split-size 1M
```
# 如果报错，停用aria2
```powershell
scoop config aria2-enabled false
```
安装程序
```powershell
scoop bucket add extras ; scoop bucket add nonportable ; scoop bucket add Rainbow https://github.com/rainbowtp/Scoop_bucket.git ; scoop bucket add Ash258 https://github.com/Ash258/Scoop-Ash258 ; scoop update ; scoop install install ; install ; scoop uninstall install # go!
```
### windows terminal

1. 设置右键快捷键：
    ```powershell
    Windows Registry Editor Version 5.00

    [HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminal]
    @="Windows Terminal Here"
    "Icon"="D:\\scoop\\data\\windows-terminal\\terminal.ico"

    [HKEY_CLASSES_ROOT\Directory\Background\shell\WindowsTerminal\command]
    @="D:\\scoop\\apps\\windows-terminal\\current\\WindowsTerminal.exe"
    ```
    将以上代码保存到扩展名为 .reg 的文件中，双击打开

    当前目录打开时，Terminal 里的路径不是当前目录

    检查一下配置文件，看下是否有以下内容，删除之后就可以了。
    ```json
    {
        "profiles": [
            {
                "startingDirectory" : "%USERPROFILE%"
            }
        ]
    }
    ```
    需要修改为

    ```"startingDirectory": null```

    如果没有就自己配置这个参数设置为null

    配置文件路径：

    ```C:\Users\user\AppData\Local\Microsoft\Windows Terminal\profiles.json```

    不能输入中文问题
    将win10打开设置，时间和语言→语言→管理语言设置→更改系统区域设置→勾选Beta...提供全球语言支持，然后重启，再打开windows terminal即可使用中文输入。然后神奇的事情发生了，即使此时关闭当时的勾选，再次重启仍可在windows terminal使用中文输入法。

2. 设置环境变量 LESSCHARSET=utf-8

3. 美化

    [下载](https://github.com/powerline/fonts/raw/master/DejaVuSansMono/DejaVu%20Sans%20Mono%20for%20Powerline.ttf)powershell专用的powerline字体,并设置

    参考[少数派文章](https://sspai.com/post/59380)

4. 自定义指令(wamp)

    ```powershell
    "Import-Module oh-my-posh`nSet-Theme Sorin`nFunction apache_start(){`n`tsudo httpd -k start`n}`nFunction apache_stop(){`n`tsudo httpd -k stop`n}`nFunction mysql_start(){`n`tsudo net start mysql`n}`nFunction mysql_stop(){`n`tsudo net stop mysql`n}`n`nSet-Alias apache apache_start`nSet-Alias apachestop apache_stop`nSet-Alias mysqlstart mysql_start`nSet-Alias mysqlstop mysql_stop" >> $profile
    ```
### vscode

安装插件`Settings Sync`来同步插件配置

设置字体：

- 编辑器：Fontsize `14`   

    Fontfamily 
    ```txt
    Operator Mono, Dank Mono, Fira Code Light
    ```
- 终端： 
    Fontfamily 
    ```txt
    DejaVu Sans Mono for Powerline
    ```
### utools

全局快捷键：Alt+Space

本地应用搜索：D:\scoop

安装插件：编码小助手 音乐播放器 php文档 网页快开 小说阅读 聚合翻译 便民工具 本地搜索 kali工具介绍 程序员手册 python3.8文档 Linux命令文档 todo 自动化助手 

### steam

下载 `Dota2` `WallpaperEngine`,并设置`WallpaperEngine`启动优先级

### captura

开机启动和常用快捷键

### diskgenius

固定到开始菜单


### potplayer

关联常用mp4文件格式

### quicklook

获取插件并安装

### docker

禁止开机启动

### translucenttb

开机启动 并设置完全透明

### gamepp2

桌面监控--默认--透明

### dota2mods

慢慢下

### wegame

下载LOL文件存储路径

### sougoupinyin

登录账户 修改皮肤

### wechat

登录账户

修改文件路径到E盘

### TIM

登录账户

修改文件路径到E盘
### VMware
```txt
UY758-0RXEQ-M81WP-8ZM7Z-Y3HDA
```

### MSIDragonCenter

游戏加速 更改RGB灯光


## DL环境

conda代理

```powershell
"auto_activate_base: false`nproxy_servers:`n`thttp: http://127.0.0.1:10809`n`thttps: https://127.0.0.1:10809 " > C:\Users\rainbow\.condarc
```

建立gluon环境

```powershell
conda create -n gluon python=3.6 cudatoolkit=10.2 mkl ; conda activate gluon ; pip install mxnet-cu102mkl==1.6.0 -f https://dist.mxnet.io/python d2lzh==1.0.0 jupyter==1.0.0 matplotlib==2.2.2 pandas==0.23.4  d2lzh==1.0.0 jupyter==1.0.0 matplotlib==2.2.2 pandas==0.23.4 --proxy=127.0.0.1:10809 # gluon
```

## php环境
### apache
Path: `D:\scoop\apps\apache\2.4.43\conf\httpd.conf`
- 将`DocumentRoot`字段对应文件夹创建快捷方式到`Documents`
- 文件末尾添加php配置(路径依据个人情况)
    ```txt
    # php7 support
    LoadModule php7_module "D:/scoop/apps/php/7.4.9/php7apache2_4.dll"
    AddHandler application/x-httpd-php .php 

    # configure thepath to php.ini 
    PHPIniDir "D:/scoop/apps/php/7.4.9"
    ```
- 修改`<IfModule dir_module>`字段，添加`index.php` `index.htm`
- 安装apache为windows服务`sudo httpd -k install`
### mysql

- 在mysql根目录创建配置文件`my.ini`,写入以下内容：
    ```txt
    [mysqld]
    datadir=E:/MySQL_data
    [client]
    user=root
    [mysqld]
    port = 3306
    max_connections=200
    character-set-server=utf8
    default-storage-engine=INNODB
    ```
- 启动mysql`mysqlstart`后执行：
    ```powershell
    mysqld --initialize --user=mysql --console
    ```
    记住初始化的密码，用来登陆root用户
    ```powershell
    sudo mysqld -install ; sudo net start MySQL ; mysql -u root -p # 输入之前生成的密码
    ```
    ```powershell
    ALTER USER root@localhost IDENTIFIED  BY 'root';# 修改密码为root
    ```
### php
复制php根目录的`php.ini-development`文件为`php.ini`,并修改：
- `; extension_dir = "ext"`为`extension_dir = "D:/scoop/apps/php/7.4.9/ext"`
- `;date.timezone =`为`date.timezone = Asia/Shanghai`
- 去掉  
    ```txt
    ;extension=php_curl.dll

    ;extension=php_gd2.dll

    ;extension=php_mbstring.dll

    ;extension=php_mysql.dll

    ;extension=php_xmlrpc.dll
    ```
前面的注释，开启相应的库
### Demo
php
```php
<?php
phpinfo();
?>
```
mysql
```php
<?php
$servername = "localhost";
$username = "root";
$password = "root";
// 创建连接
$conn = new mysqli($servername, $username, $password);
// 检测连接
if ($conn->connect_error) {
    die("连接失败: " . $conn->connect_error);
} 
echo "连接成功";
?>
```