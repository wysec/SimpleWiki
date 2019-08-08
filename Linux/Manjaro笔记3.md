## Shutdown ACPI interrupts

The system cpu is high, about 65%.

通过以下命令查询是enable状态，且数量非常高的文件：
> grep "enable" /sys/firmware/acpi/interrupts/*

然后执行以下命令将此文件设置为disable：

>su
>echo "disable" > gpe6F


## 配置源
配置中国的mirrors：
> sudo pacman-mirrors -i -c China -m rank

同步并更新系统：
> sudo pacman -Syyu


## 安装拼音 GooglePinyin
1. 安装Google输入法和fcitx管理工具：
> sudo pacman -S fcitx-googlepinyin

> sudo pacman -S fcitx-im

> sudo pacman -S fcitx-configtool


2. 中文输入法切换配置：
> vi .xprofile
```txt
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```
3. 重启系统。

4. 选择`Configure Current Input Method`，添加Google Pinyin。 这就可以使用中文输入法了。

## 安装Shadowsocks

> sudo pacman -S shadowsocks

配置文件：
> sudo gedit /etc/shadowsocks/config.json
```txt
{
  "server":"my_server_ip",
  "local_address": "127.0.0.1",
  "local_port":1080,
  "server_port":my_server_port,
  "password":"my_password",
  "timeout":300,
  "method":"aes-256-cfb"
}
```

启动Shadowsocks，可以：
> sslocal -c /etc/shadowsocks/config.json

配合nohup和&可以使之后台运行，关闭终端也不影响：
> sslocal -c /etc/shadowsocks/config.json &

建议使用systemd来管理Shadowsocks服务，启动服务（config是config.json的文件名）：
> sudo systemctl start shadowsocks@conifg

若需开机自启动：
> sudo systemctl enable shadowsocks@config

`Created symlink /etc/systemd/system/multi-user.target.wants/shadowsocks@config.service → /usr/lib/systemd/system/shadowsocks@.service.`

## 配置Oh-my-zsh
- 查看系统安装的shell： cat /etc/shells
- 查看当前shell： echo $SHELL
- 使用chsh切换默认shell


## 界面美化
1. 安装 Gnome Tweak Tool

Gnome Tweak Tool是为Gnome3桌面开发的一个GUI配置工具，用户可以用它来更改图标主题、GTK主题和Gnome Shell主题。
> sudo pacman -S gnome-tweak-tool

2. 安装Gnome-shell Extensions

Gnome shell扩展，它可以安装gnome上的第三方组件和插件。通过这些插件可以方便的定制gnome桌面。访问网站https://extensions.gnome.org。安装浏览器插件。

安装系统的插件：
> sudo pacman -S chrome-gnome-shell

访问网站，安装 `User Themes`



## 安装git：
sudo pacman -S git

解决git status显示中文文件名乱码问题：` git config --global core.quotepath false`。因为git对0x80以上的字符进行quote，这样就不会对0x80以上的字符进行quote。中文就显示正常了。

## 安装Onedrive：
1. 安装依赖
> sudo pacman -S curl sqlite dlang

2. 安装
> git clone https://github.com/skilion/onedrive.git
> cd onedrive
> make
> sudo make install

3. First run

After installing the application you must run it at least once from the terminal to authorize it.

You will be asked to open a specific link using your web browser where you will have to login into your Microsoft Account and give the application the permission to access your files. After giving the permission, you will be redirected to a blank page. Copy the URI of the blank page into the application.

4. Uninstall

> sudo make uninstall //# delete the application state

> rm -rf .config/onedrive


## 安装Yay

> git clone https://aur.archlinux.org/yay.git

> cd yay

> makepkg -si

安装软件：
> yay -S package-name

## 降级curl
由于在执行onedrive进行文件同步时始终报错，`HTTP request returned status code 302 (Found)`，通过[查询](https://github.com/skilion/onedrive/issues/430)确定应该是curl版本高的原因，需要对curl版本进行降级。

执行命令：
> downgrade curl
```txt
Downgrading from A.L.A. is disabled on the stable branch. To override this behavior, set DOWNGRADE_FROM_ALA to 1 .
See https://wiki.manjaro.org/index.php?title=Using_Downgrade  for more details.
```
执行如下命令：
> DOWNGRADE_FROM_ALA=1 downgrade curl

选择需要降级的软件版本前面的序号。

编辑`/etc/pacman.conf`文件， 添加IgnorePkg = curl，系统在更新软件包时忽略对curl的更新。

## 安装Chrome
> sudo pacman -S chromium


## 使用systemd开机启动服务

1. 在`/usr/lib/systemd/system/`目录中创建service文件，如：auto-config.service。添加如下内容：
```
[Unit]
Description=Auto Script

[Service]
Type=simple
User=root
ExecStart=/root/gpe.sh

[Install]
WantedBy=multi-user.target
```
2. 进入`/etc/systemd/system`目录，将上面文件链接到multi-user.target.wants（这样这个服务就可以开机自启动）。
> sudo ln -s /usr/lib/systemd/system/auto-script.service ./multi-user.target.wants/

这样就可以使用`systemctl`来管理auto-config服务了，可以在里面添加需要开机执行的脚本。

















