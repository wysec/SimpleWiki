
## 硬盘安装Debian

通过磁盘安装Debian最好的方式还是使用[win32-loader](http://ftp.debian.org/debian/tools/win32-loader/stable/)。

## 安装和配置Samba

### 安装

安装samba
```
# apt install samba
```
为了测试目的，可以选择安装samba client。
```
# apt install smbclient
```

### 配置

编辑`/etc/samba/smb.conf`配置文件
```
# cp /etc/samba/smb.conf /etc/samba/smb.conf_backup
# grep -v -E "^#|^;" /etc/samba/smb.conf_backup | grep . > /etc/samba/smb.conf
```

### 创建用户

Samba有自己的用户管理系统。但是任何samba用户都必须存在于/etc/passwd文件中。因此，先使用`useradd`命令创建系统用户，再创建samba用户。
```
# smbpasswd -a smbuser
```

### 配置Samba home目录

默认home目录是只读的，修改默认配置。
```
[homes]
   comment = Home Directories
   browseable = yes
   read only = no
   create mask = 0700
   directory mask = 0700
   valid users = %S
```

### 共享配置

创建共享目录
```
# mkdir /var/samba
# chmod 777 /var/samba/
```
修改`/etc/samba/smb.conf`文件
```
[public]
  comment = public anonymous access
  path = /var/samba/
  browsable =yes
  create mask = 0660
  directory mask = 0771
  writable = yes
  guest ok = yes
```
重启samba服务
```
# systemctl restart smbd
```

### 访问samba

在资源管理器中输入命令直接访问`\\samba-server`。

选择此电脑“映射网络驱动器”，文件夹中填写`\\samba-server\smbuser`，进行认证后就可以像正常驱动器那样访问了。

## 诊断和处理CPU使用高

通过查询资料，发现可以通过`perf`工具来进行CPU诊断。

1. 安装
```
sudo apt-get install linux-perf-4.9
```

2. 分析
```
sudo perf record -a -e cycles -o cycle.perf -g sleep 10
```

3. 查看报告
```
perf report -i cycle.perf | more
```
通过查看诊断报告，可以发现是`ACPI`占用CPU高。

4. 关闭服务

禁用ACPI，可以通过修改`/etc/default/grub`来实现。在 GRUB_CMDLINE_LINUX_DEFAULT 变量中以 “name=value” 的格式添加内核参数。
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi=off"
```




## 安装无线网卡驱动

要安装无线网卡驱动，首先当然是要知道是什么型号的网卡了，这可以通过`lspci`命令查看，还有`lspci -vvv`可以查看更详细的信息。

我的网卡是：

> 02:00.0 Network controller: Intel Corporation WiFi Link 5100

通过型号关键字 Intel Corporation WiFi Link 5100 搜索，可以很容易找到[英特尔® 无线适配器的 Linux* 支持](https://www.intel.cn/content/www/cn/zh/support/articles/000005511/network-and-i-o/wireless-networking.html)。找到英特尔® 无线 WiFi Link 5100AGN的固件[iwlwifi-5000-ucode-5.4.A.11.tar.gz](https://wireless.wiki.kernel.org/_media/en/users/drivers/iwlwifi-5000-ucode-5.4.a.11.tar.gz
)并下载。

解压缩固件包
```
tar -xzvf iwlwifi-5000-ucode-5.4.a.11.tar.gz
```

安装此固件/驱动
```
# cp iwlwifi-5000-1.ucode /lib/firmware
```

最后重启系统，无线网卡就可以用了。


## 命令行配置无线密码

wpa_supplicant是一个连接、配置WIFI的工具，它主要包含wpa_supplicant与wpa_cli两个程序。通常情况下，可以通过wpa_cli来进行WIFI的配置与连接，如果有特殊的需要，可以编写应用程序直接调用wpa_supplicant的接口直接开发。

In order to use wpa_cli, a control interface must be specified for wpa_supplicant, and it must be given the rights to update the configuration. Do this by creating a minimal configuration file:

1. 创建`/etc/wpa_supplicant/wpa_supplicant.conf`文件，内容如下：
```
ctrl_interface=/run/wpa_supplicant
update_config=1
```

2. 启动wpa_supplicant
```
# wpa_supplicant -B -i interface -c /etc/wpa_supplicant/example.conf
```

3. 启动wpa_cli
```
# wpa_cli
```

4. 使用scan和scan_results命令查看可用的网络
```
> scan
OK
<3>CTRL-EVENT-SCAN-RESULTS
> scan_results
bssid / frequency / signal level / flags / ssid
00:00:00:00:00:00 2462 -49 [WPA2-PSK-CCMP][ESS] MYSSID
11:11:11:11:11:11 2437 -64 [WPA2-PSK-CCMP][ESS] ANOTHERSSID
```
5. 连接无线网络

```
> add_network
0
> set_network 0 ssid "MYSSID"
> set_network 0 psk "passphrase"
> enable_network 0
<2>CTRL-EVENT-CONNECTED - Connection to 00:00:00:00:00:00 completed (reauth) [id=0 id_str=]
```

如果不需要密码，要用`set_network 0 key_mgmt NONE`命令替换`set_network 0 psk "passphrase"`。

6. 最后保存这个网络到配置文件
```
> save_config
OK
```
7. 把`iface wlp2s0 inet dhcp wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
    `命令加入`/etc/network/interfaces`文件最后。
```
➜  ~ cat /etc/network/interfaces
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

iface wlp2s0 inet dhcp wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```

8. 重启网卡
```
# ifup wlp2s0
```

这样就可以连接到无线网络了。

## 配置开机启动命令

对于配置开机启动命令，一般都是推荐添加命令到 /etc/rc.local 文件，但是 Debian 9 默认不带 /etc/rc.local 文件，而 rc.local 服务却还是自带的。

因此可以按照如下方法来配置：

1. 手工添加一个 /etc/rc.local 文件

```
sudo cat <<EOF >/etc/rc.local
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

exit 0
EOF
```

2. 赋予执行权限
```
# chmod +x /etc/rc.local
```
3. 把需要开机启动的命令添加到 /etc/rc.local 文件，放在 exit 0 前面即可，如
```
/bin/systemctl stop wpa_supplicant
/sbin/wpa_supplicant -B -i wlp2s0 -c /etc/wpa_supplicant/wpa_supplicant.conf
/sbin/ifup wlp2s0
```
4. 启动 rc-local 服务
```
# systemctl start rc-local
```
重启后可以发现开机启动命令已执行。


## 安装Gitlab

### 通过Docker安装

1. 通过Docker下载Gitlab：

```
sudo docker pull gitlab/gitlab-ce:latest
```

2. 启动Gitlab

用下面的命令启动一个默认配置的Gitlab。如果只在本机测试使用的话，将hostname替换为localhost。如果需要让外部系统也能访问的话使用外网IP地址。

```
sudo docker run --detach \
    --hostname gitlab.example.com \
    --publish 443:443 --publish 80:80 --publish 22:2222 \
    --name gitlab \
    --restart unless-stopped \
    --volume /srv/gitlab/config:/etc/gitlab \
    --volume /srv/gitlab/logs:/var/log/gitlab \
    --volume /srv/gitlab/data:/var/opt/gitlab \
    gitlab/gitlab-ce:latest
```

首次启动可能比较慢，需要等待一分钟左右的时间。我们可以使用sudo docker ps命令查看当前所有Docker容器的状态。当它的状态由starting变为运行时间时，说明成功启动了。我们直接使用上面配置的IP地址（如localhost）在浏览器中访问即可。

这里把主机的 443、80、22 端口直接转发到容器，同时利用 --volume /srv/gitlab/config:/etc/gitlab 、 --volume /srv/gitlab/logs:/var/log/gitlab、--volume /srv/gitlab/data:/var/opt/gitlab 这三个参数将 gitlab 的配置、数据和日志持久化到主机文件系统上来。

*以上方法未成功*。

### 直接安装

1. 安装依赖

```
# apt install curl openssh-server ca-certificates postfix
```

2. 安装

可以通过脚本方便的安装。

```
#curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
# apt install gitlab-ce
```

3. 配置

使用`gitlab-ctl`命令行工具来管理Gitlab。首先需要使用它来产生配置文件。
```
# gitlab-ctl reconfigure
```
在完成配置后，可以启停Gitlab。
```
# gitlab-ctl start
# gitlab-ctl stop
```

最后，就可以在浏览器中输入URL地址访问Gitlab了 。

## 安装和配置Aria2

1. 使用命令直接安装Aria2
```
apt-get install aria2
```

2. 创建配置文件

创建 aria2.session 文件
```
touch /etc/aria2/aria2.session
```
创建 aria2.conf 配置文件：
```
touch /etc/aria2/aria2.conf
```

3. 配置aria2.conf

配置文件可以参考[这里](http://aria2c.com/usage.html)。

4. 运行

```
sudo aria2c --conf-path=/etc/aria2/aria2.conf -D
```
加-D是后台运行。 有错误可以直接在配置文件中修改。

5. 安装和配置AriaNg 

- 下载最新版本：https://github.com/mayswind/AriaNg/releases
- 解压压缩文件到制定目录
- 进入程序文件目录，可以使用`python -m SimpleHTTPServer`开启web服务（python3可以执行：`python3 -m http.server 8000`）
- 用浏览器打开并访问URL:8000，就可以直接访问AriaNg进行下载操作了

6. BT下载设置

开启BT设置
```txt
enable-dht=true
bt-enable-lpd=true
enable-peer-exchange=true
```

添加 BT trackers
```txt
bt-tracker=udp://62.138.0.158:6969/announce,udp://87.233.192.220:6969/announce,
```


## 安装frp
frp 是一个可用于内网穿透的高性能的反向代理应用，支持 tcp, udp, http, https 协议。

- 利用处于内网或防火墙后的机器，对外网环境提供 http 或 https 服务。
- 对于 http, https 服务支持基于域名的虚拟主机，支持自定义域名绑定，使多个域名可以共用一个80端口。
- 利用处于内网或防火墙后的机器，对外网环境提供 tcp 和 udp 服务，例如在家里通过 ssh 访问处于公司内网环境内的主机。

1. 程序[下载地址](https://github.com/fatedier/frp/releases)，服务端和客户端都要下载。

2. 解压安装文件并进入文件目录
```
tar -zxvf frp_0.21.0_linux_amd64.tar.gz
```

3. 配置服务端
  编辑 frps.ini 文件
```
# frps.ini
[common]
bind_port = 7000
```

4. 启动frps.ini

```
./frps -c ./frps.ini
```

5. 配置客户端
  编辑 frpc.ini 文件，假设 frps 所在服务器的公网 IP 为 x.x.x.x
```
# frpc.ini
[common]
server_addr = x.x.x.x
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000
```

6. 启动frpc.ini

```
./frpc -c ./frpc.ini
```

7. 通过SSH访问内网主机
```
ssh user@x.x.x.x -p 6000
```

8. 后台运行



## 安装h5ai

1. 程序[下载地址](https://release.larsjung.de/h5ai/)
2. 拷贝文件到apache目录/var/www/html/
3. 直接访问http://YOUR-DOMAIN.TLD/_h5ai/public/index.php
4. 添加/_h5ai/public/index.php到apache.conf：`DirectoryIndex  index.html  index.php  /_h5ai/public/index.php`


## 安装LAMP

### MariaDB(MySQL)

```
# apt install mariadb-client mariadb-server
```

执行下面命令登录MariaDB并设置root密码。
```
mysql -u root -p
```

### PHP
```
# apt install php7.0 php7.0-mysql
```

### Apache
```
# apt install apache2 libapache2-mod-php7.0
```
默认Apache服务器内容在/var/www/html。


## 参考资料


[How do I disable ACPI when booting?](https://askubuntu.com/questions/160036/how-do-i-disable-acpi-when-booting)

[How to configure Samba Server share on Debian 9 Stretch Linux](https://linuxconfig.org/how-to-configure-samba-server-share-on-debian-9-stretch-linux)

[WPA supplicant](https://wiki.archlinux.org/index.php/WPA_supplicant_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

[wpa_supplicant及wpa_cli使用方法](https://segmentfault.com/a/1190000011579147)

[How to Install Gitlab On Debian 9 Stretch Linux](https://linuxconfig.org/how-to-install-gitlab-on-debian-9-stretch-linux)

[Ubuntu Docker 简单安装 GitLab](http://www.cnblogs.com/xishuai/p/ubuntu-install-gitlab-with-docker.html)

[GitLab 中文社区版 Docker 镜像](https://github.com/beginor/docker-gitlab-ce)

[Ubuntu16 下载软件Aria2 全局配置方法](https://www.jianshu.com/p/b2649d073741)

[Aria2 Linux 完整安装及使用教程](https://www.htcp.net/3652.html)

[How to Install a LAMP Server on Debian 9 Stretch Linux](https://linuxconfig.org/how-to-install-a-lamp-server-on-debian-9-stretch-linux)

[h5ai 目录列表程序完整安装使用教程](https://www.htcp.net/3643.html)