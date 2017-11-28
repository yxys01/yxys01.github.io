---
layout: post
title: iOS学习之非代码获取iPhone型号及其他信息
date: 2017-08-16
tag: iOS
---

首先安装libimobiledevice和ideviceinstaller

```
brew uninstall ideviceinstaller
brew uninstall libimobiledevice
brew install --HEAD libimobiledevice
brew link --overwrite libimobiledevice
brew install ideviceinstaller
brew link --overwrite ideviceinstaller
```
<font color=#000000 size=6 face="黑体">应用相关</font>
1、 安装应用（真机）

```
ideviceinstaller -i xxx.ipa
```

2、 卸载应用（真机）

```
ideviceinstaller -U <bundleId>
```

3、 获取应用唯一标识

```
$ unzip xxx.ipa
$ cd Payload/xxx.app
$ defaults read `pwd`/Info CFBundleIdentifier
com.test
```

4、从源码构建应用安装包

这里只举 debug 包

```
$ cd /source-folder/
$ PROJECT=<your-project-name>
$ xcodebuild clean -project $PROJECT.xcodeproj -configuration Debug -alltargets
$ xcodebuild archive -project $PROJECT.xcodeproj -scheme $PROJECT -archivePath $PROJECT.xcarchive
# 注意，末尾的 exportProvisioningProfile 参数值是在 Xcode 的 Performance->Accounts->Apple ID->View Details 窗口的下半部分看到的名称。如 iOS Team Provisioning Profile: chj.ToDoList
$ xcodebuild -exportArchive -archivePath $PROJECT.xcarchive -exportPath $PROJECT -exportFormat ipa -exportProvisioningProfile "your provision profile"
# build 完的 ipa 包直接就放在当前目录
```

<font color=#000000 size=6 face="黑体">设备相关</font>
1、查看设备中的应用列表


```
$ ideviceinstaller [-u <device-udid>] -l
Total: 46 apps
com.xiaojukeji.didi - 滴滴出行 4.1.5.0
com.tencent.mqq - QQ 6.0.0.424
```
...
2、获取真机实时日志

```
idevicesyslog [-u <device-udid>]
```

3、获取当前连接的设备列表

```
# 注意：这里列出的设备包括模拟器及 mac 电脑本身
$ instruments -s devices
```
<font color=#000000 size=6 face="黑体">iPhone信息相关</font>
1、获取ios手机的udid
```
idevice_id -l
```

2、获取ios手机信息

```
ideviceinfo 
```

3、获取ios手机信息，并以xml形式显示
```
ideviceinfo -x 
```

4、获取手机型号

```
ideviceinfo -k ProductType 
```

5、获取系统版本

```
ideviceinfo -k ProductVersion
```

6、获取手机名称

```
ideviceinfo -k DeviceName 
```


<font color=#000000 size=6 face="黑体">注：获取手机型号与实际手机型号对照</font>

| 获取手机型号    | 实际手机型号    | 
| ------------- |:-------------| 
| iPhone3,1     | iPhone 4 | 
| iPhone3,2     | iPhone 4 | 
| iPhone3,3     | iPhone 4 | 
| iPhone4,1     | iPhone 4S | 
| iPhone5,1     | iPhone 5 | 
| iPhone5,2     | iPhone 5 (GSM+CDMA)| 
| iPhone5,3     | iPhone 5c (GSM) | 
| iPhone5,4     | iPhone 5c (GSM+CDMA) | 
| iPhone6,1     | iPhone 5s (GSM) | 
| iPhone6,2     | iPhone 5s (GSM+CDMA) | 
| iPhone7,1     | iPhone 6 Plus | 
| iPhone7,2     | iPhone 6 | 
| iPhone8,1     | iPhone 6s | 
| iPhone8,2     | iPhone 6s Plus | 
| iPhone8,4     | iPhone SE | 
| iPhone9,1     | 国行、日版、港行iPhone 7 | 
| iPhone9,2     | 港行、国行iPhone 7 Plus | 
| iPhone9,3     | 美版、台版iPhone 7 | 
| iPhone9,4     | 美版、台版iPhone 7 Plus | 

<font color=#000000 size=5 face="黑体">px与pt区别</font>
字体大小的设置单位，常用的有2种：px、pt。这两个有什么区别呢？

先搞清基本概念：

px就是表示pixel，像素，是屏幕上显示数据的最基本的点；
pt就是point，是印刷行业常用单位，等于1/72英寸。
px全称为pixel，是一个点，它不是自然界的长度单位，谁能说出一个“点”有多长多大么？可以画的很小，也可以很大。如果点很小，那画面就清晰，我们称它为“分辨率高”，反之，就是“分辨率低”。所以，“点”的大小是会“变”的，也称为“相对长度”。

pt全称为point，但中文不叫“点”，查金山词霸可以看到，确切的说法是一个专用的印刷单位“磅”，大小为1/72英寸。所以它是一个自然界标准的长度单位，也称为“绝对长度”。

因此就有这样的说法:

 - pixel是相对大小，
 - point是绝对大小。
 

<font color=#000000 size=5 face="黑体">iPhone各种屏幕分辨率</font>
![这里写图片描述](http://img.blog.csdn.net/20170816182652625?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![这里写图片描述](http://img.blog.csdn.net/20170816182709495?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)