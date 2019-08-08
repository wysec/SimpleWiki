# 简介

**认证**是对个人，实体或网站所声称的身份进行验证的过程。在web应用程序中的认证通常通过提交用户名或ID以及只有特定用户才知道的一个或多个私有信息项来执行。

**会话管理**是服务端与交互的客户端保持状态的过程。这要求服务端记住怎样对随后传输的请求进行处理。会话通过在服务器上维护会话标识符，会话标识符可以在发送和接收请求时在客户端和服务器之间来回传递。会话应该是每个用户都唯一的，且很难通过计算预测的。



# 认证的一般指导原则

## 用户ID

确保用户名/用户ID是不区分大小写的。比如用户名“smith”和“Smith”应该是相同的用户。用户名应该也是唯一的。对于高安全性的应用程序，用户名可以是被分配的而不是用户定义的。

### Email地址作为用户ID

有关验证Email地址的信息，参考https://www.owasp.org/index.php/Input_Validation_Cheat_Sheet#Email_Address_Validation



## 实施恰当的密码强度控制

使用密码进行身份认证的一个关键是密码强度。

### 密码长度

更长的密码提供更大的字符组合，从而使攻击者更难以猜测。

- 最小密码长度应由应用程序强制执行。

小于10个字符的密码被认为是比较弱的。（[NIST SP800-132](http://csrc.nist.gov/publications/nistpubs/800-132/nist-sp800-132.pdf)）

虽然最小长度的强制执行可能会在某些用户中导致记住密码的问题，应用应鼓励用户设置密码短语（句子或词的组合），这比典型的密码要长的多，并且更容易记住。

- 最大密码长度不要设置的太低，这会影响用户创建密码短语。典型的最大长度是128个字符。

如果密码短语是小写字母且小于20个字符，这通常被认为是比较弱的，

### 密码复杂度

应用程序应该执行密码复杂度规则，以防止容易猜测密码。密码机制应该允许用户输入的任何字符可作为密码的一部分，包括空格符。

密码更改机制需要最低程度的复杂度，这对应用程序及其用户群是有意义的。

例如：

- 密码必须至少满足以下4个复杂规则中的3个
  - 至少一个大写字符（A-Z）
  - 至少一个小写字符（a-z）
  - 至少一个数字（0-9）
  - 至少一个[特殊字符](https://www.owasp.org/index.php/Password_special_characters) - 空格也是特殊字符
- 至少10个字符
- 至多128个字符
- 不超过2个相同字符在一行中（如：111是不允许的）


更多阅读：

[Your Password Complexity Requirements are Worthless - OWASP AppSecUSA 2014](https://www.youtube.com/watch?v=zUM7i8fsf0g)

[PathWell: Password Topology Histogram Wear-Leveling](https://www.korelogic.com/Resources/Presentations/bsidesavl_pathwell_2014-06.pdf)

### Password Topologies

- Ban commonly used password topologies
- Force multiple users to use different password topologies
- Require a minimum topology change between old and new passwords


### 附加信息

- 确保用户键入的每个字符实际上都包含在密码中
- 在密码设置页面上明确的展示密码策略
- 如果新设置密码没有符合密码复杂度策略，错误信息应该描述新密码未符合的所有的密码复杂度规则，而不仅仅是第一条不符合的规则。



##  实施安全的密码恢复机制

应用程序通常都会提供一种方法为用户在忘记密码时访问他们的帐户。这可以参考[忘记密码](https://www.owasp.org/index.php/Forgot_Password_Cheat_Sheet)部分。



## 安全的存储密码

应用系统使用正确的加密技术来存储密码是非常重要的。这个可以参考[密码存储](https://www.owasp.org/index.php/Password_Storage_Cheat_Sheet)部分。



## 使用加密链路传输密码

[Transport Layer Protection Cheat Sheet](https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet)

登录页面和所有后续的已认证页面必须通过TLS或其他强壮的传输方式独占访问。



## 对敏感特征要再次认证

为了缓解CSRF和会话劫持问题，在更新敏感账号信息（如：用户密码）或转账操作时，要求对当前账号凭证进行再次认证。如果没有这样的控制措施，攻击者可能通过CSRF或XSS攻击执行敏感的传输而不用知道用户当前的凭证。



## 考虑强事务验证

一些应用应该使用第二个因素来检查是否用户可以执行敏感操作。更多信息可参考：[Transaction Authorization Cheat Sheet](https://www.owasp.org/index.php/Transaction_Authorization_Cheat_Sheet)。

### TLS客户端认证

TLS客户端身份验证，也称为双向TLS身份验证，由浏览器和服务器组成，在TLS握手过程中发送各自的TLS证书。

 [Client-authenticated TLS handshake](https://en.wikipedia.org/wiki/Transport_Layer_Security#Client-authenticated_TLS_handshake)



## 认证和错误消息

在认证功能中不正确的实施错误消息可能导致用户账号和密码被枚举攻击。应用程序应该以一般的方式响应（HTTP和HTML）。

### 认证响应

不管是用户账号还是密码错误，应用都应只返回一般通用的错误消息。其中不应指示现有账号的状态。

### 不正确的响应示例

- 登录用户foo：无效的密码
- 登录失败，无效用户ID
- 登录失败；账号被禁用
- 登录失败；此账号不存在

### 正确的响应示例

- 登录失败；无效的用户ID或密码

正确的响应没有指示用户ID或密码是否是不正确的，因此不能推断出有效的用户ID。

###  错误码和URLs

应用程序可能返回不同的HTTP错误代码，这取决于身份验证尝试响应。它可以返回200作为积极的结果，也可以是403作为消极的结果。即使向用户显示一个通用的错误页面，HTTP响应代码可能不同，它可能泄漏帐户是否是有效的。



## 防止暴力破解攻击

如果应用系统对多次失败认证没有控制措施，那么攻击者就可以通过暴力破解的方式来破解账号密码。对于这种情况，可以在登录失败一定次数后对账号进行锁定处理。为了防止锁定导致对账号的拒绝服务攻击，可以在锁定一定时间（如，20分钟）后对其解锁。这可以减慢攻击者的攻击并且可以允许正常用户的使用。

此外，使用多因素认证也是个非常好的防御控制措施。当使用多因素认证时，账号锁定机制就非必须了。



# 日志和监控

启用身份认证的日志和监控功能以实时检测攻击或问题：

- 确保记录并检查所有的失败问题
- 确保记录并检查所有的密码失效问题
- 确保记录并检查所有的账号锁定问题



# 使用无密码的认证协议

虽然通过用户/密码组合进行身份验证并使用多因素身份验证通常被认为是安全的，但有有些情况下这不被认为是安全的。比如有第三方应用要连到web应用，无论是从一个移动设备、其它网站、或其它情况。当这个发生时，允许第三方应用存储账号/密码组合被认为是不安全的，这扩展了攻击面，并处于控制之外。对此，有下面的认证协议可以来保护不将数据暴力给攻击者。



## OAuth

Open Authorization (OAuth)是一个协议，它允许应用程序以用户身份对服务器进行身份验证，而不需要密码或任何作为身份提供者的第三方服务器。它使用一个服务器产生的令牌，并提供授权流最多如何发生，以便诸如移动应用程序之类的客户端可以告知服务器用户正在使用该服务。

推荐是使用OAuth 1.0a 或 OAuth 2.0，因为第一个版本（OAuth1.0）被发现存在会话固定漏洞。

OAuth 2.0 依靠HTTPS并且当前使用和实施都通过来自，如Facebook、Google、Microsoft，的API。OAuth 1.0a 更难使用，因为它需要数字签名的加密库的使用。然而，由于OAuth1.0a不依赖HTTPS安全可以更适合于高风险交易。



## OpenId

OpenId是一个基于HTTP的协议，使用身份验证程序验证用户是他所说的用户。这是一个非常简单的协议，允许服务提供商启动单点登录（SSO）的方式。这允许用户重新使用给予受信任的OpenId身份提供商的单一身份，并在多个网站中成为同一用户，而不需要向OpenId身份提供者除外提供任何网站的密码。

由于它的简单性，它提供了密码的保护，OpenId已被很好地采用。OpenId的一些知名身份提供商是Stack Exchange，Google，Facebook。

对于非企业环境，OpenId通常被认为是安全的、更好的选择，只要身份提供者是受信任的，。



## SAML

Security Assertion Markup Language (SAML)常常被认为是与OpenId竞争的。最推荐的版本是2.0，因为它功能非常完全并且提供了强壮的安全性。像OpenId，SAML使用身份提供者（identity providers），但不像OpenId的，它是基于XML的并且提供更多的灵活性。SAML是基于浏览器重定向发送XML数据。此外，SAML不仅仅可由服务提供商（service provider）发起；它也可以从身份提供者发起的。这允许用户在不经过验证的情况下通过不同的门户进行导航，而无需执行任何操作，从而使该过程变得透明。

OpenId主要使用在消费市场，而SAML则常常在企业应用中使用。因为很少有OpenId身份提供者是企业级的。更普遍的是在企业内部网络中使用SAML。

[SAML Security Cheat Sheet](https://www.owasp.org/index.php/SAML_Security_Cheat_Sheet)



## FIDO

The Fast Identity Online (FIDO) 联盟已经创建了两个协议来促进在线认证。Universal Authentication Framework （UAF）协议 和 Universal Second Factor（U2F）协议。UAF针对无密码认证，而U2F允许在基于密码认证的基础上额外加入另一个认证因素。这两种协议都是基于公钥密码学挑战应答模型。







# 会话管理的一般指导原则

会话管理直接关系到身份认证，会话管理可以参考[Session Management Cheat Sheet](https://www.owasp.org/index.php/Session_Management_Cheat_Sheet)。



# 密码管理

密码管理器是自动管理大量不同凭据的程序，浏览器插件或Web服务，包括记录和填写，在不同的站点上生成随机密码等。虽然密码管理器的使用受到争议，但他们对认证安全的贡献是积极的。

至少应该通过遵循以下建议，Web应用程序至少不会使密码管理的工作比必要更困难

- 使用标准的HTML表单进行用户名和密码输入使用适当的“type”属性，
- 不要人为地将用户密码限制为“对人类合理”的长度，并允许密码长度最多为128个字符，
- 不要人为地防止在用户名和密码字段上复制粘贴
- 避免基于插件的登录页面（Flash、Silverlight等）





