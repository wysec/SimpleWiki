# 1 关于APK文件
Android应用程序包 （Android application package，APK） 是Android操作系统使用的一种应用程序包文件格式。一个Android应用程序的代码想要在Android设备上运行，必须先进行编译，然后被打包成为一个被Android系统所能识别的文件才可以被运行，而这种能被Android系统识别并运行的文件格式便是“APK”。 一个APK文件内包含被编译的代码文件(.dex 文件)，文件资源（resources）， assets，证书（certificates），和清单文件（manifest file）。

APK 文件基于 ZIP 文件格式，它与JAR文件的构造方式相似。它的互联网媒体类型是application/vnd.android.package-archive。


# 2 APK文件结构
一个APK文件通常包含以下文件：
* META-INF/ ：此目录包含以下文件，
  * MANIFEST.MF: 清单文件
  * CERT.RSA: 记录应用程序的证书信息
  * CERT.SF: 记录资源列表和其SHA-1摘要信息
* libs/：此目录包含针对特定处理器软件层的编译代码
  * armeabi：针对所有基于ARM处理器的编译代码
  * armeabi-v7a：针对所有基于ARMv7及以上处理器的编译代码
  * arm64-v8a：针对所有基于ARMv8 arm64 及以上处理器的编译代码
  * x86：针对所有基于x86处理器的编译代码
  * x86_64：针对所有基于x86 64位处理器的编译代码
  * mips：针对所有基于MIPS处理器的编译代码
* res/：此目录包含未被编译进resources.arsc文件的资源
* assets/：此目录包含应用程序资产
* AndroidManifest.xml：另外一个Android清单文件，用于描述该应用程序的名字、版本号、所需权限、注册的服务、链接的其他应用程序
* classes.dex：classes文件被编译成dex的文件格式，用于在Dalvik虚拟机上运行
* resources.arsc：该文件包含了预编译资源，如二进制XML
