# InsecureBankv2分析

Vulnerable Android application for developers and security enthusiasts to learn about Android insecurities

## 1. 准备

### 1.1 下载

> GItHub地址：https://github.com/dineshshetty/Android-InsecureBankv2

### 1.2 导入Android Sutdio

根据本地Android Sutdio应用的配置，修改此应用的以下三个文件：

1. /path/InsecureBankv2/build.gradle，build:gradle: 版本；
2. /path/InsecureBankv2/app/build.gradle，compileSdkVersion、minSdkVersion、targetSdkVersion、dependencies 等；
3. /path/InsecureBankv2/gradle/wrapper/gradle-wrapper.properties，gradle包版本。

最后，打开Android Sutdio，选择“Open an existing Android Studio project”，选择项目所在文件夹导入应用。

## 2. 运行InsecureBankv2

在Android Sutdio中run应用并在模拟器中运行。操作应用，首先是登录页面，任意输入账号密码，点击Sign In进入，会要求配置服务端应用（输入服务端IP和Port），可在本地的AndroLabServer目录中执行python app.py来启用服务端。

## 3. 代码分析

InsecureBankv2有这几个java文件：

- ChangePassword.java
- CryptoClass.java
- DoLogin.java
- DoTransfer.java
- FilePrefActivity.java
- LoginActivity.java
- MyBroadCastReceiver.java
- MyWebViewClient.java
- PostLogin.java
- TrackUserContentProvider.java
- ViewStatement.java
- WrongLogin.java

其中LoginActivity.java是主Activity。

PostLogin.java中进行root和模拟器检测，但是好像都没有成功执行。需要分析原因！






