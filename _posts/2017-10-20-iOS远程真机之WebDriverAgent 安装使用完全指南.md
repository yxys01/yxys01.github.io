---
layout: post
title: iOS远程真机之WebDriverAgent 安装使用完全指南
date: 2017-10-20
tag: iOS远程真机
---
&#160; &#160; &#160; &#160;iOS-remote是结合[WebDriverAgent](https://github.com/facebook/WebDriverAgent) 和 [ios-minicap](https://github.com/openstf/ios-minicap) 开源项目做出来的基于JAVA的iOS远程真机控制的项目。

&#160; &#160; &#160; &#160;基本思路可见：https://testerhome.com/topics/9681

&#160; &#160; &#160; &#160;然后安装iOS-minicap的步骤可见：https://testerhome.com/topics/10456

&#160; &#160; &#160; &#160;接下来我介绍一下iOS远程真机实现的核心——**WebDriverAgent**，简称**WDA**的安装使用过程

&#160; &#160; &#160; &#160;整个安装过程主要参考**Testerhome**的三篇文章（感谢社区各种意义上的帮助）：

* [WebDriverAgent简介](https://testerhome.com/topics/4904)

* [iOS 真机如何安装 WebDriverAgent](https://testerhome.com/topics/7220)

* [WebDriverAgent天坑记](https://testerhome.com/topics/9666)（这个算是我自己安装过程中总结出的一部分Q&A）

&#160; &#160; &#160; &#160;后文有部分也有参考这三篇文章，如果有地方不清楚的话，可以去原贴所在查看。

### WebDriverAgent简介

&#160; &#160; &#160; &#160;首先介绍一下**WebDriverAgent**吧

>WebDriverAgent 在 iOS 端实现了一个 WebDriver server ，借助这个 server 我们可以远程控制 iOS 设备。
你可以启动、杀死应用，点击、滚动视图，或者确定页面展示是否正确。
>This makes it a perfect tool for application end-to-end testing or general purpose device automation.（它说它是iOS上一个完美的e2e的自动化解决方案）
>It works by linking XCTest.framework and calling Apple's API to execute commands directly on a device.（链接XCTest.framework调用苹果的API直接在设备上执行命令）
>WebDriverAgent is developed and used at Facebook for end-to-end testing and is successfully adopted by Appium. （Appium封装工作正在进行中，如果一旦封装好，那么以后就可以直接用Appium提供的binding了。）It is currently maintained by Marek Cirkos and Mehdi Mulani.


### WebDriverAgent特性

&#160; &#160; &#160; &#160;它有如下**特性**：

* 真机和模拟器都支持
* 实现了大部分的 WebDriver spec
* USB support for devices，所谓的usb支持，指的是设备不需要上网，目前client binding 还没有。
* 提供了一个 Inspector
* Easy development cycle as it can be launched & debugged directly via Xcode
* Unsupported yet, but works with tvOS & OSX

&#160; &#160; &#160; &#160;这里我就**WDA安装步骤**和**遇到的一些问题以及解决方案**做个总结帖

&#160; &#160; &#160; &#160;闲话不多说，直接上干货

### 安装步骤

&#160; &#160; &#160; &#160;**1、准备工作**
```bash
$ brew install carthage

$ brew install node
```

&#160; &#160; &#160; &#160;**2、clone项目（要安装有git `brew install git`）**

```bash
$ git clone https://github.com/facebook/WebDriverAgent
```

&#160; &#160; &#160; &#160;**3、下载依赖**

```bash
$ cd /Users/yourname/WebDriverAgent

$ mkdir -p Resources/WebDriverAgent.bundle

$ sh ./Scripts/bootstrap.sh
```

&#160; &#160; &#160; &#160;该脚本会使用Carthage下载所有的依赖，使用npm打包响应的js文件 

&#160; &#160; &#160; &#160;执行完成后，直接双击打开WebDriverAgent.xcodeproj这个文件。

&#160; &#160; &#160; &#160;**4、设置证书**

&#160; &#160; &#160; &#160;因为安装到真机上都是需要证书签名的，~~用免费的证书我没有搞定，最后用的还是99美元的开发者证书。~~
![这里写图片描述](http://img.blog.csdn.net/20171020115512832?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
&#160; &#160; &#160; &#160;画圈的地方，从左向右依次点击。最后Team那一栏，选择你买到的开发者证书帐号。（个人证书也可以）

&#160; &#160; &#160; &#160;接着在TARGETS里面选中WebDriverAgentRunner，用同样的方法设置好证书（这里参考了https://testerhome.com/topics/7220）
![这里写图片描述](http://img.blog.csdn.net/20171020115550265?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;如果是免费版的个人证书，还需要修改下WebDriverAgent的BundleID，随便加点后缀，只要不跟其他人的重名就好 （这里参考了macaca的一篇文章 https://testerhome.com/topics/8085 ）
![这里写图片描述](http://img.blog.csdn.net/20171020115620097?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;**5、配置WebDriverAgent.xcodeproj**

&#160; &#160; &#160; &#160;双击打开WebDriverAgent.xcodeproj这个文件

&#160; &#160; &#160; &#160;**WebDriverAgentLib->Build Setting->Runpath Search Paths->添加变量：**

```
$(SRCROOT)/../Carthage/Build/iOS
$(PROJECT)/Carthage/Build/iOS
```

&#160; &#160; &#160; &#160;如图所示
![这里写图片描述](http://img.blog.csdn.net/20170810113959038?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;Then

&#160; &#160; &#160; &#160;**WebDriverAgentLib->Build Setting->Build Active Architecture Only->No**

如图所示
![这里写图片描述](http://img.blog.csdn.net/20170810114016404?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;按道理讲，到这里就基本可以直接Run了，大家也可以先Run一下试试

&#160; &#160; &#160; &#160;如果实在还是无法在真机里面使用，可以尝试下面的步骤：

&#160; &#160; &#160; &#160;把 WebDriverAgent/Inspector/webpack.config.js 中的

```js
loaders: [
      { test: /\.js?$/, loaders: ['babel-loader'], exclude: /node_modules/ },
      { test: /\.css?$/, loader: 'style-loader!css-loader' },
    ]
```
改为

```js
loaders: [
      { test: /\.js?$/, loaders: ['babel-loader'] },
      { test: /\.css?$/, loader: 'style-loader!css-loader' },
    ]
```
&#160; &#160; &#160; &#160;把` , exclude: /node_modules/ `这部分去掉即可！

&#160; &#160; &#160; &#160;**6、运行与测试**

&#160; &#160; &#160; &#160;启动 WebDriverAgent，官方提供了四种方式：

* 使用 XCode
* 用 xcodebuild
* Using fbsimctl from FBSimulatorControl framework
* Using FBSimulatorControl framework directly

#### XCode运行

&#160; &#160; &#160; &#160;菜单栏选择目标设备
![这里写图片描述](http://img.blog.csdn.net/20171020115708444?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;Scheme选择WebDriverAgentRunner
![这里写图片描述](http://img.blog.csdn.net/20171020115722916?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
&#160; &#160; &#160; &#160;最后运行 `Product -> Test`

&#160; &#160; &#160; &#160;一切正常的话，手机上会出现一个无图标的WebDriverAgent应用，启动之后，马上又返回到桌面。这是很正常的不要奇怪。

&#160; &#160; &#160; &#160;此时控制台界面可以看到设备的IP。如果看不到的话，使用这种方法打开
![这里写图片描述](http://img.blog.csdn.net/20171020115731981?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
&#160; &#160; &#160; &#160;通过上面给出的IP和端口，加上`/status`合成一个url地址。例如`http://192.168.0.105:8100/status`，然后浏览器打开。如果出现一串JSON输出，说明WDA安装成功了。

#### 终端运行

```bash
# 解锁keychain，以便可以正常的签名应用，
PASSWORD="your password"
security unlock-keychain -p $PASSWORD ~/Library/Keychains/login.keychain

# 获取设备的UDID
UDID=$(idevice_id -l | head -n1)

# 运行测试
xcodebuild -project /Users/yourname/WDA/WebDriverAgent/WebDriverAgent.xcodeproj  -scheme WebDriverAgentRunner -destination "id=$UDID" test
```


&#160; &#160; &#160; &#160;如果弄了很久还是没搞定。可以尝试下这些步骤

1. git pull更新WebDriverAgent的代码
2. 卸载手机上的WebDriverAgent
3. 更新Xcode（尽量使用Xcode8,Xcode9貌似存在使用不当的问题）
4. 更新Mac系统
5. 重启Mac
6. **重启iPhone**（！！！！！最有效，优先级可以放到最高）

### WebDriverAgent  Q&A

&#160; &#160; &#160; &#160;这个主要参见：https://testerhome.com/topics/9666/edit

&#160; &#160; &#160; &#160;如果有什么新的问题，大家也可以在下面留言，我会及时更新上来给大家分享。


### WebDriverAgent 安装终极大招

&#160; &#160; &#160; &#160;最后，放上终极大招——我正在使用的，已经编译好的项目文件:

&#160; &#160; &#160; &#160;WebDriverAgent：链接：http://pan.baidu.com/s/1c1KIFfU 密码：c4dx

&#160; &#160; &#160; &#160;如果百度链接挂了，就去CSDN中下载：[WebDriverAgent](http://download.csdn.net/download/yxys01/10024469)

&#160; &#160; &#160; &#160;注意：

&#160; &#160; &#160; &#160;用户需要在`WebDriverAgentLib`和`WebDriverAgentRunner`中将`Signing`改为自己的开发者证书即可

![这里写图片描述](http://img.blog.csdn.net/20171020115833514?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![这里写图片描述](http://img.blog.csdn.net/20171020115844509?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### iOS-remote 安装篇

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 ios-minicap 安装使用完全指南](https://testerhome.com/topics/10456)

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 WebDriverAgent 安装使用完全指南](https://testerhome.com/topics/10463)

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 iOS-remote安装使用完全指南](https://testerhome.com/topics/10466)

### 参考文献
&#160; &#160; &#160; &#160;iOS-minicap + WDA 实现 ios 远程真机测试  https://testerhome.com/topics/10262

&#160; &#160; &#160; &#160;基于 WebDriverAgent 的 iOS 远程控制  https://testerhome.com/topics/8890

&#160; &#160; &#160; &#160;WebDriverAgent简介  https://testerhome.com/topics/4904

&#160; &#160; &#160; &#160;iOS 真机如何安装 WebDriverAgent  https://testerhome.com/topics/7220

&#160; &#160; &#160; &#160;WebDriverAgent天坑记  https://testerhome.com/topics/9666
