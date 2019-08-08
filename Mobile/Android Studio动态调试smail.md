# Android Studio动态调试smail


## 0x01. 安装插件

1. 下载插件`smalidea`

地址：https://bitbucket.org/JesusFreke/smali/downloads

2. 安装插件

打开Android Studio的Settings -> Plugins，选择 Install plugin from disk，选择下载的插件文件。


## 0x02. 反编译APK

3. 反编译APK

> java -jar apktool.jar d  -d out/ -o Crackme.apk

4. 修改为调试模式

修改AndroidManifest.xml中的`android:debuggable="true"`

5. 编译APK

修改完成之后，编译回APK
> java -jar apktool.jar b -d out/ -o  Crackme.apk


6. 对APK签名

> apksigner.bat sign --ks debug.keystore  Crackme1.apk
> 或
> jarsigner


## 0x03. Android studio设置

7. 再反编译上面的APK文件（可选择）

> java -jar apktool.jar d Crackme.apk -o /output/

8. 在Android Studio中导入

打开Android Studio，选择`Import project (Eclipse ADT, Gradle. etc.)`，选择项目位置，然后选择`Create project from existing sources`，之后一直选next。

9. 设置smali目录为源码根目录

选中smali目录，鼠标右键点击，在弹出菜单中勾选`Marked Directory As`->`Generated Sources Root`

10. 以调试状态启动APP

> adb shell am start -D -n com.example.simpleencryption/.MainActivity

11. 查看调试端口

通过`Android Device Monitor`或Android SDK安装目录下tools子目录下的`monitor.bat`查看调试程序的调试端口（(每次启动目标程序，端口是系统分配，可能会变化）。

12. Edit Configuration

选择菜单的"Run" -> "Edit Configuration" ->" Remote"，将"Hosts“设置为`localhost`，"Ports"设置为`8700` （上面查看到的调试端口一致）（DDMS共用端口）。

13. 配置JDK

选择菜单的 "File"  -> "Project Structure"，然后选择"Project"，设置"Project SDK"。

14. 启动debug

点击Android Studio的debug进入调试模式，"Run" -> "Debug" (Shift + F9)

15. 下断点

选择要下断点的位置，鼠标点击代码左侧位置，若有个红点，表示已下断点。

## 0x04. 调试面板

1. step over（F8）：点击该图标，程序执行下一行，如果是调用方法，这个方法会被直接执行不会进入该方法内部。
2. step into（F7）：点击该图标，如果当前代码是自定义的方法，会进入方法内部逐步执行，如果是官方库的方法，不会进入方法内部，如果不是将执行下一行。
3. force step into（Alt+Shift+F7）：点击该图标会进入方法内部，不论是自定义方法还是官方库方法。会使你脱离当前断点，从你选择的方法开始调试。
4. step out（Shift+F8）：点击该图标会快速运行完该方法，跳出当前执行的方法内部，执行到该方法调用的下一句代码。
5. drop frame：点击该图标会回到调用该方法的开始处，恢复原始值，可以重新运行该方法。
6. run to cursor（Alt+F9）：点击该图标会使程序跳转到下一个断点处，如果设置多个断点逐句运行会比较麻烦，可以通过这个功能快速跳转到下一个断点。



## 0x05. 参考

1. [Android studio动态调试](http://cstsinghua.github.io/2016/06/13/Android%20studio%E5%8A%A8%E6%80%81%E8%B0%83%E8%AF%95%E6%8C%87%E5%8D%97/)
2. [AndroidStudio 动态调试Smali代码](http://www.jianshu.com/p/c9a7debfbf91)
3. [Android studio动态调试smali](http://www.cnblogs.com/goodhacker/p/5592313.html)
4. [AndroidStudio断点调试和高级调试](http://www.jianshu.com/p/f19ee61126ef)


## 0x06. 备注

如何不修改AndroidManifest.xml中的debug属性就可以进行调试？

在Android系统的根目录中有default.prop文件，其中的ro.debuggable属性值如果是1的话，那么设备中所有应用都可以被调试，即使AndroidManifest.xml中没有android:debuggable=true，还是可以调试的。

可以把mprop程序拷贝到设备目录中，然后运行此命令：`./mprop ro.debuggable 1`，这个工具可以修改内存中所有的属性值。

http://www.wjdiankong.cn/apk%E8%84%B1%E5%A3%B3%E5%9C%A3%E6%88%98%E4%B9%8B-%E8%84%B1%E6%8E%89360%E5%8A%A0%E5%9B%BA%E7%9A%84%E5%A3%B3/