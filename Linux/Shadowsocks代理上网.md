


## 安装

Debian/Ubuntu:
```
apt-get install python-pip
pip install shadowsocks
```

Redhat/CentOS:
```
sudo yum install python-setuptools && easy_install pip
sudo pip install shadowsocks
```

## 配置

创建shadowsocks的配置文件，一般放在/etc目录下面：
配置文件内容如下：

```
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

## 运行

直接运行：
```
sslocal -c /home/xx/Software/ShadowsocksConfig/shadowsocks.json
```

## 一些问题

### sslocal命令未找到

再次执行安装命令安装shadowsocks。

### 启动报错

在启动上面程序时，Shadowsocks报错：
```
undefined symbol: EVP_CIPHER_CTX_cleanup
```

找到存在问题的openssl.py文件。
编辑此文件，将其中的CIPHER_CTX_cleanup替换为CIPHER_CTX_reset。应该有两处。
然后重新运行Shadowsocks即可




[在 iOS 上使用 Socks5 代理](https://hev.cc/2524.html)


[ShadowSocks启动报错undefined symbol EVP_CIPHER_CTX_cleanup](https://blog.csdn.net/youshaoduo/article/details/80745196)

[通过 ProxyChains-NG 实现终端下任意应用代理](https://www.hi-linux.com/posts/48321.html)
