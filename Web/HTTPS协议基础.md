
超文本传输安全协议（英语：Hypertext Transfer Protocol Secure，缩写：HTTPS，常称为HTTP over TLS，HTTP over SSL或HTTP Secure）是一种网络安全传输协议。在计算机网络上，HTTPS经由HTTP（超文本传输协议）进行通信，但利用SSL/TLS来加密数据包。HTTPS开发的主要目的，是提供对网络服务器的身份认证，保护交换数据的隐私与完整性。

## 1. SSL/TLS协议

SSL/TLS协议的基本思路是采用公钥加密法，也就是说，客户端先向服务器端索要公钥，然后用公钥加密信息，服务器收到密文后，用自己的私钥解密。

**这里有两个问题**

1. 如何保证公钥不被篡改？

> 解决方法：将公钥放在数字证书中。只要证书是可信的，公钥就是可信的。

2. 公钥加密计算量太大，如何减少耗用的时间？

> 解决方法：每一次会话（session），客户端和服务器端都生成一个"会话密钥"（session key），用它来加密信息。由于"会话密钥"是对称加密，所以运算速度非常快，而服务器公钥只用于加密"会话密钥"本身，这样就减少了加密运算的消耗时间。

因此，SSL/TLS协议的基本过程是这样的：

> 1.  客户端向服务器端索要并验证公钥
> 2.  双方协商并生成"会话密钥"
> 3.  双方采用"会话密钥"进行加密通信

上面过程的前两步，又称为"握手阶段"（handshake）。

## 2. 握手过程

![](https://upload.wikimedia.org/wikipedia/commons/a/ae/SSL_handshake_with_two_way_authentication_with_certificates.svg)

"握手阶段"涉及四次通信，但需要注意的是，**"握手阶段"的所有通信都是明文的**。

### 2.1 客户端发出请求（ClientHello）

客户端（通常是浏览器）先向服务器发出加密通信的请求，这被叫做ClientHello请求。在这一步，客户端主要向服务器提供以下信息。

> 1. 支持的协议版本，比如TLS 1.2版
> 2. 一个客户端生成的随机数，稍后用于生成"会话密钥"
> 3. 支持的加密套件候选列表，比如RSA公钥加密
> 4. 支持的压缩方法

这里需要注意的是，客户端发送的信息之中不包括服务器的域名。也就是说，理论上服务器只能包含一个网站，否则会分不清应该向客户端提供哪一个网站的数字证书。这就是为什么通常一台服务器只能有一张数字证书的原因。

在2006年，TLS协议加入了一个[Server Name Indication](http://tools.ietf.org/html/rfc4366)扩展，允许客户端向服务器提供它所请求的域名。

### 2.2 服务器回应（SeverHello）

服务器收到客户端请求后，向客户端发出回应，这叫做SeverHello。

从Server Hello到Server Done，有些服务端的实现是每条单独发送，有服务端实现是合并到一起发送。Sever Hello和Server Done都是只有头没有内容的数据。

服务器的回应包含以下内容。

> 1. 确认使用的加密通信协议版本，比如TLS1.2版本。如果浏览器与服务器支持的版本不一致，服务器关闭加密通信
> 2. 一个服务器生成的随机数，稍后用于生成"会话密钥"
> 3. 确认使用的加密套件，比如RSA公钥加密
> 4. 服务器证书

在服务端向客户端发送的证书中没有提供足够的信息（证书公钥）的时候，还可以向客户端发送一个 Server Key Exchange。

除了上面这些信息，如果服务器需要确认客户端的身份，就会再包含一项请求 Cerficate Request ，要求客户端提供"客户端证书"。比如，金融机构往往只允许认证客户连入自己的网络，就会向正式客户提供USB密钥，里面就包含了一张客户端证书。

### 2.3 客户端回应（Certificate Verify）

客户端收到服务器回应以后，首先验证服务器证书Certificate Verify，这些证书通常基于X.509。<u>如果证书不是可信机构颁布、或者证书中的域名与实际域名不一致、或者证书已经过期</u>，就会向访问者显示一个警告，由其选择是否还要继续通信。

如果证书没有问题，客户端就会从证书中取出服务器的公钥。然后，向服务器发送下面三项信息。

> 1. 一个随机数。该随机数用服务器公钥加密，防止被窃听
> 2. 编码改变通知，表示随后的信息都将用双方商定的加密方法和密钥发送
> 3. 客户端握手结束通知，表示客户端的握手阶段已经结束。这一项同时也是前面发送的所有内容的hash值，用来供服务器校验

上面第一项的随机数，是整个握手阶段出现的第三个随机数，它是客户端使用一些加密算法(例如：RSA, Diffie-Hellman)产生一个48个字节的key，这个key叫 `pre-master secret`，很多材料上也被称作 `pre-master key`。有了它以后，客户端和服务器就同时有了三个随机数，接着双方就用事先商定的加密方法，各自生成本次会话所用的同一把"会话密钥"。
至于为什么一定要用三个随机数，来生成"会话密钥"。


> 不管是客户端还是服务器，都需要随机数，这样生成的密钥才不会每次都一样。由于SSL协议中证书是静态的，因此十分有必要引入一种随机因素来保证协商出来的密钥的随机性。
> 对于RSA密钥交换算法来说，pre-master-key本身就是一个随机数，再加上hello消息中的随机，三个随机数通过一个密钥导出器最终导出一个对称密钥。
> pre master的存在在于SSL协议不信任每个主机都能产生完全随机的随机数，如果随机数不随机，那么pre master secret就有可能被猜出来，那么仅使用pre master secret作为密钥就不合适了，因此必须引入新的随机因素，那么客户端和服务器加上pre master secret三个随机数一同生成的密钥就不容易被猜出了，一个伪随机可能完全不随机，可是是三个伪随机就十分接近随机了。


ChangeCipherSpec是一个独立的协议，体现在数据包中就是一个字节的数据，用于告知服务端，客户端已经切换到之前协商好的加密套件（Cipher Suite）的状态，准备使用之前协商好的加密套件加密数据并传输了。

然后，客户端会使用之前协商好的加密套件和Session Secret加密一段 Finish 的数据传送给服务端，此数据是为了在正式传输应用数据之前对刚刚握手建立起来的加解密通道进行验证。

此外，如果前一步，服务器要求客户端证书，客户端会在这一步发送证书及相关信息Client Key Exchange。

### 2.4 服务器的最后回应（Server Finish）

服务器收到客户端的第三个随机数pre-master key之后，计算生成本次会话所用的"会话密钥"。然后，向客户端最后发送下面信息。

> 1. 编码改变通知，表示随后的信息都将用双方商定的加密方法和密钥发送。
> 2. 服务器握手结束通知，表示服务器的握手阶段已经结束。这一项同时也是前面发送的所有内容的hash值，用来供客户端校验。

一切准备好之后，会给客户端发送一个 ChangeCipherSpec，告知客户端已经切换到协商过的加密套件状态，准备使用加密套件和 Session Secret加密数据了。之后，服务端也会使用 Session Secret 加密一段 Finish 消息发送给客户端，以验证之前通过握手建立起来的加解密通道是否成功。

> 客户端与服务器通过公钥保密协商共同的主私钥（双方随机协商），这通过精心谨慎设计的伪随机数功能实现。结果可能使用Diffie-Hellman交换，或简化的公钥加密，双方用各自用私钥解密。所有其他关键数据的加密均使用这个“主密钥”。数据传输中记录层（Record layer）用于封装更高层的HTTP等协议。记录层数据可以被随意压缩、加密，与消息验证码压缩在一起。每个记录层包都有一个Content-Type段用以记录更上层用的协议

至此，整个握手阶段全部结束。接下来，客户端与服务器进入加密通信，就完全是使用普通的HTTP协议，只不过用"会话密钥"加密内容。

## 3. 密钥协商和加密算法

在客户端和服务器开始交换TLS所保护的加密信息之前，他们必须安全地交换或协定加密密钥和加密数据时要使用的密码。用于密钥交换的方法包括：使用RSA算法生成公钥和私钥（在TLS 握手协议中被称为`TLS_RSA`），Diffie-Hellman（`TLS_DH`），ephemeral Diffie-Hellman（`TLS_DHE`），椭圆曲线迪菲-赫尔曼（`TLS_ECDH`），ephemeral elliptic-curve Diffie-Hellman（`TLS_ECDHE`），anonymous Diffie-Hellman（`TLS_DH_anon`），预共享密钥/pre-shared key（`TLS_PSK`）和 Secure Remote Password（`TLS_SRP`）。

TLS_DH_anon和TLS_ECDH_anon的密钥协商协议不能验证服务器或用户，因为易受中间人攻击因此很少使用。只有`TLS_DHE`和`TLS_ECDHE`提供**前向保密**能力。

### 3.1 基于 RSA 的密钥协商

RSA密钥交换中，RSA起的作用是key transmission，也就是说，用于产生session key的“种子”是由客户端决定，用服务器的公钥加密并再次传输到服务器端。（TLS Record Layer: 用密钥k进行加密））

![rsa](https://pic4.zhimg.com/80/42ac9058525f1b57092f1f1202e8d2cf_hd.jpg)

为了防止RSA密钥协商时的假冒身份，就需要RSA结合数字证书一起使用。

### 3.2 基于 DH 的密钥协商

DH密钥交换中，DH起的作用是key exchange，也就是说，用于产生session key的“种子”，是客户端和服务器都参与了的。(见下图的g^c和g^s)

![dh](https://pic2.zhimg.com/80/f7617fa90df014bb0fc44070a3b13d85_hd.jpg)

由于DH 算法本身有不支持认证的缺点。就是说：它虽然可以对抗“偷窥”，却无法对抗“篡改”，自然也就无法对抗“中间人攻击/MITM”。因此DH 需要与其它签名算法（如 RSA、DSA、ECDSA）配合，靠签名算法帮忙来进行身份认证。当 DH 与 RSA 配合使用，称之为“DH-RSA”，与 DSA 配合则称为“DH-DSA”，以此类推。如果 DH没有配合某种签名算法，则称为“DH-ANON”。

DH 算法有一个变种，称之为 ECDH（全称是“Elliptic Curve Diffie-Hellman”）。它与 DH 类似，差别在于：DH 依赖的是求解“离散对数问题”的困难；ECDH 依赖的是求解“椭圆曲线离散对数问题”的困难。另外，ECDH 跟 DH 一样，也是“无认证”的，同样需要跟其它签名算法配合使用。

由于DH 和 ECDH的密钥是持久的（静态的）。就是说通讯双方生成各自的密钥之后，就长时间用下去。但是这样存在安全隐患，就是无法做到[前向保密](https://en.wikipedia.org/wiki/Forward_secrecy)。为了达到“前向保密”，就是每次会话都要重新协商一次密钥，用完后就丢弃掉。就出现了针对上述两个算法的改良版本DHE 和 ECDHE。

### 3.3 基于 PSK 的密钥协商

PSK （Pre-Shared Key），预共享密钥。就是在通信前就预先让通信双方共享一些密钥（通常是对称加密的密钥）。这样的好处是：不依赖公钥体系；不涉及非对称加密。

由于通信双方已经预先配置了若干共享的密码。为了标识多个密钥，给每一个密钥定义一个唯一的 ID。在协商时，客户端把自己选好的密钥的 ID 告诉服务端，服务端在自己的密钥池子中找到这个 ID，就用对应的密钥与客户端通讯；否则就报错并中断连接。

### 3.4 基于 SRP 的密钥协商

SRP，Secure Remote Password protocol。它和PSK类似，只不过 client/server 双方共享的是比较人性化的密码（password）而不是密钥（key）。该算法采用了一些机制（盐/salt、随机数）来防范“嗅探/sniffer”或“字典猜解攻击”或“重放攻击”。

### 3.5 安全的密钥交换协议

在TLS1.3中推荐使用：

- DHE-RSA（具有前向安全性）
- ECDHE-RSA（具有前向安全性）
- ECDHE-ECDSA（具有前向安全性）

### 3.6 安全的加密

在TLS1.3中推荐使用：

- AES GCM（块密码）
- AES CCM（块密码）
- ChaCha20-Poly1305（流密码）

### 3.7 数据完整性

在TLS1.3中推荐使用：

- AEAD


## 3. 参考

[HTTPS](https://en.wikipedia.org/wiki/HTTPS)

[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security)

[扫盲 HTTPS 和 SSL/TLS 协议3：密钥交换（密钥协商）算法及其原理](https://program-think.blogspot.com/2016/09/https-ssl-tls-3.html)

[SSL/TLS协议运行机制的概述](http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)

[SSL/TLS原理详解](http://seanlook.com/2015/01/07/tls-ssl/)

http://insights.thoughtworkers.org/cipher-behind-https/

http://honglu.me/2016/01/13/HTTPS%E8%AF%A6%E8%A7%A3/