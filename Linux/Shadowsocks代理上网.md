


## ��װ

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

## ����

����shadowsocks�������ļ���һ�����/etcĿ¼���棺
�����ļ��������£�

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

## ����

ֱ�����У�
```
sslocal -c /home/xx/Software/ShadowsocksConfig/shadowsocks.json
```

## һЩ����

### sslocal����δ�ҵ�

�ٴ�ִ�а�װ���װshadowsocks��

### ��������

�������������ʱ��Shadowsocks����
```
undefined symbol: EVP_CIPHER_CTX_cleanup
```

�ҵ����������openssl.py�ļ���
�༭���ļ��������е�CIPHER_CTX_cleanup�滻ΪCIPHER_CTX_reset��Ӧ����������
Ȼ����������Shadowsocks����




[�� iOS ��ʹ�� Socks5 ����](https://hev.cc/2524.html)


[ShadowSocks��������undefined symbol EVP_CIPHER_CTX_cleanup](https://blog.csdn.net/youshaoduo/article/details/80745196)

[ͨ�� ProxyChains-NG ʵ���ն�������Ӧ�ô���](https://www.hi-linux.com/posts/48321.html)
