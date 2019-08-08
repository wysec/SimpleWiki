

SSH端口转发也被称作SSH隧道(SSH Tunnel)，因为它们都是通过SSH登录之后，在SSH客户端与SSH服务端之间建立了一个隧道，从而进行通信。SSH隧道是非常安全的，因为SSH是通过加密传输数据的(SSH全称为Secure Shell)。

SSH有三种端口转发模式，本地端口转发(Local Port Forwarding)，远程端口转发(Remote Port Forwarding)以及动态端口转发(Dynamic Port Forwarding)。


## 本地端口转发

所谓本地端口转发，就是将发送到本地端口的请求，转发到目标端口。这样，就可以通过访问本地端口，来访问目标端口的服务。使用-L属性，就可以指定需要转发的端口，语法是这样的：

```
 ssh -L <local port>:<remote host>:<remote port> <SSH hostname>
```

## 远程端口转发

所谓远程端口转发，就是将发送到远程端口的请求，转发到目标端口。这样，就可以通过访问远程端口，来访问目标端口的服务。使用-R属性，就可以指定需要转发的端口，语法是这样的:

```
ssh -R <local port>:<remote host>:<remote port> <SSH hostname>
```

## 动态端口转发

```
ssh -D
```

## 参考资料

[玩转SSH端口转发](https://blog.fundebug.com/2017/04/24/ssh-port-forwarding/)

[SSH Tunnel - Local and Remote Port Forwarding Explained With Examples](https://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html)

https://blog.twofei.com/528/
[]()

https://blog.mythsman.com/2017/01/14/1/