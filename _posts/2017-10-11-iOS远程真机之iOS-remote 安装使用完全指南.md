---
layout: post
title: iOS远程真机之iOS-remote 安装使用完全指南
date: 2017-10-11
tag: iOS远程真机
---
## 简介
&#160; &#160; &#160; &#160;iOS-remote是结合[WebDriverAgent](https://github.com/facebook/WebDriverAgent) 和 [ios-minicap](https://github.com/openstf/ios-minicap) 开源项目做出来的基于JAVA的iOS远程真机控制的项目。

## 平台
&#160; &#160; &#160; &#160;仅限Mac使用

## 特点

- [√] 启动项目时运行 iproxy
- [√] 为WDA服务创建http代理
- [√] 添加缺失的索引页
- [√] 支持包管理API
- [√] 支持WDA运行
- [√] iOS远程真机控制
- [√] 基于Java开发

## 功能

- [√] iOS远程真机控制（点击拖拽）
- [√] HOME键功能
- [√] iPhone输入框添加文字（中英文--中文还在修复中）
- [√] 设备信息显示
- [√] 从本地安装ipa文件到iPhone真机里
- [√] 卸载已安装APP
- [√] 截图功能

## 安装要求

* 用brew安装libjpeg-turbo (要求版本1.5及以上)
* Xcode (要求版本8及以上,注：9有一定无法使用的风险)
* [cmake](https://cmake.org/)（最好通过brew安装）
* OS X Yosemite (要求版本10.9及以上)
* iOS（要求版本8及以上）
* [Lightning cable](https://en.wikipedia.org/wiki/Lightning_(connector)). 查看设备列表.
* 用[Carthage](https://github.com/Carthage/Carthage) 获取所有依赖项
* 用[npm](https://www.npmjs.com)建立Inspector bundle
* Eclipse IDE for Java EE Developers
* JavaSE (要求版本1.6及以上) 
* Tomcat (要求版本7及以上) 
* libimobiledevice
* ideviceinstaller
* usbmuxd

## 其他帮助文档
[How to install ios-minicap](https://testerhome.com/topics/10456)

[How to install WebDriverAgent](https://testerhome.com/topics/10463)

[WebDriverAgent Q&A](https://testerhome.com/topics/9666)

[Eclipse Import Maven Project](http://blog.csdn.net/yxys01/article/details/78111229)

[Configure Tomcat9 In Mac](http://blog.csdn.net/yxys01/article/details/77715330)
## 安装

### 1、安装Xcode

&#160; &#160; &#160; &#160;Xcode这个可以去官网安装或者去我的网盘下载Xcode8.3.3.xip

&#160; &#160; &#160; &#160;链接：http://pan.baidu.com/s/1hszRESW 密码：yogw

&#160; &#160; &#160; &#160;下载好Xcode，还要下载Command Line Tools

 1. 打开mac终端
 2. 在终端中输入以下命令：`xcode-select --install`  ，按回车。

&#160; &#160; &#160; &#160;然后一路点确定安装即可

&#160; &#160; &#160; &#160;详情可见：http://blog.csdn.net/yxys01/article/details/73456973


### 2、安装Homebrew

&#160; &#160; &#160; &#160;Homebrew的安装很简单，只需在终端下输入如下指令：

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
&#160; &#160; &#160; &#160;Homebrew安装成功后，会自动创建目录 /usr/local/Cellar 来存放Homebrew安装的程序。 这时你在命令行状态下面就可以使用 brew 命令了.

&#160; &#160; &#160; &#160;详情可见：http://blog.csdn.net/yxys01/article/details/77452318

### 3、安装node和npm

&#160; &#160; &#160; &#160;直接打开终端输入如下指令：

```bash
$ brew install node
```

&#160; &#160; &#160; &#160;执行完上面的命令，你就安装好了nodejs和npm 

### 4、安装前准备工作

&#160; &#160; &#160; &#160;**(1)需要安装 [usbmuxd](https://github.com/libimobiledevice/usbmuxd) 以便于通过 USB 通道测试 iOS 真机，不需要测试真机则不用安装**

```bash
$ brew install usbmuxd
```

&#160; &#160; &#160; &#160;**(2)请安装 carthage 来构建 WebDriverAgent.**

```bash
$ brew install carthage
```

&#160; &#160; &#160; &#160;**(3)安装libimobiledevice 和 ideviceinstaller**

```bash
$ sudo brew update
$ sudo brew install libimobiledevice
$ sudo brew install ideviceinstaller
```

### 5、安装ios-minicap

&#160; &#160; &#160; &#160;**(1)打开终端，clone该项目：**

```bash
$ git clone https://github.com/openstf/ios-minicap 
```
&#160; &#160; &#160; &#160;**(2)安装libjpeg-turbo**

```bash
$ brew install libjpeg-turbo 
```
&#160; &#160; &#160; &#160;**(3)安装cmake**

```bash
$ brew install cmake
```
&#160; &#160; &#160; &#160;**(4)启动ios-minicap**

&#160; &#160; &#160; &#160;详情可见：http://blog.csdn.net/yxys01/article/details/76442135 或者 https://testerhome.com/topics/10456

### 6、安装 WebDriverAgent

&#160; &#160; &#160; &#160;安装步骤详情可见：https://testerhome.com/topics/10463

&#160; &#160; &#160; &#160;**(1)打开终端，clone该项目：**

```bash
$ git clone https://github.com/facebook/WebDriverAgent
```
&#160; &#160; &#160; &#160;**(2)运行初始化脚本**

```bash
$ cd /Users/yourname/WebDriverAgent

$ mkdir -p Resources/WebDriverAgent.bundle

$ sh ./Scripts/bootstrap.sh
```

&#160; &#160; &#160; &#160;该脚本会使用Carthage下载所有的依赖，使用npm打包响应的js文件

&#160; &#160; &#160; &#160;执行完成后，直接双击打开WebDriverAgent.xcodeproj这个文件。

&#160; &#160; &#160; &#160;**(3)安装中遇到一些问题，解决方案可见：**

&#160; &#160; &#160; &#160;http://blog.csdn.net/yxys01/article/details/77045359


### 7、安装iOS-remote

&#160; &#160; &#160; &#160;**(1)打开终端，clone该项目：**

```bash
$ git clone https://github.com/weamylady2/iOS_remote
```
&#160; &#160; &#160; &#160;or
```bash
$ git clone https://github.com/yxys01/iOS_remote
```

&#160; &#160; &#160; &#160;**(2)在 Eclipse中打开 iOS_remote**

&#160; &#160; &#160; &#160;打开Eclipse 
```
Import->Maven->Existing Maven Projects->Next->Browse(iOS_remote's path)->Finish
```

&#160; &#160; &#160; &#160;**更改 iOS_remote中的一些设置**

```
Java Resources->src/main/resource->config.properties
```

&#160; &#160; &#160; &#160;**在config.properties中改三个参数:`minicapPath、wdaPath、bashPath`**

```java
minicapPath=/Users/yourname/ios-minicap-master
wdaPath=/Users/yourname/WebDriverAgent
bashPath=/Users/yourname/ios_remote/src/main/resources
wdaPort=8200
minicapPort=12345
```
&#160; &#160; &#160; &#160;**(3)重新构建 ios-minicap**

&#160; &#160; &#160; &#160;为了减少MAC的压力，我们需要减少从minicaps中发送imgs的频率。

&#160; &#160; &#160; &#160;在ios-minicap的文件夹中,编辑 `src/minicap.cpp`

&#160; &#160; &#160; &#160;添加一个方法：

```c++
static void sleep_ms(unsigned int secs)
{
struct timeval tval;
tval.tv_sec=secs/1000;
tval.tv_usec=(secs*1000)%1000000;
select(0,NULL,NULL,NULL,&tval);
}
```
&#160; &#160; &#160; &#160;然后在main中添加`sleep_ms(50);`

```c++
while (gWaiter.isRunning() and gWaiter.waitForFrame() > 0) {
client.lockFrame(&frame);
encoder.encode(&frame);
client.releaseFrame(&frame);
putUInt32LE(frameSize, encoder.getEncodedSize());
if ( pumps(socket, frameSize, 4) < 0 ) {
break;
}
if ( pumps(socket, encoder.getEncodedData(), encoder.getEncodedSize()) < 0 ) {
break;
}
sleep_ms(50);
}
```

&#160; &#160; &#160; &#160;重新构建 ios-minicap, 运行`build.sh`在ios-minicap文件夹中:

```bash
$ ./build.sh 
mkdir: build: File exists
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/waterhuang/Downloads/ios-minicap-master/build
[100%] Built target ios_minicap
```

### 8、运行iOS_remote

&#160; &#160; &#160; &#160;**(1)新建一个终端，打开iproxy** 

```bash
$ iproxy 8200 8100
```
&#160; &#160; &#160; &#160;**(2)再打开一个终端**

```bash
$ cd /Users/yourname/iOS_remote
$ mvn tomcat7:run-war
```
&#160; &#160; &#160; &#160;**(3)打开浏览器，输入网址：http://localhost:8080/ios/ 即可**

### iOS-remote 安装篇

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 ios-minicap 安装使用完全指南](https://testerhome.com/topics/10456)

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 WebDriverAgent 安装使用完全指南](https://testerhome.com/topics/10463)

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 iOS-remote安装使用完全指南](https://testerhome.com/topics/10466)

### 参考文献
&#160; &#160; &#160; &#160;iOS-minicap + WDA 实现 ios 远程真机测试  https://testerhome.com/topics/10262

&#160; &#160; &#160; &#160;基于 WebDriverAgent 的 iOS 远程控制  https://testerhome.com/topics/8890

&#160; &#160; &#160; &#160;iOS 远程真机 (仅限屏幕查看)  https://testerhome.com/topics/6470

&#160; &#160; &#160; &#160;WebDriverAgent简介  https://testerhome.com/topics/4904

&#160; &#160; &#160; &#160;iOS 真机如何安装 WebDriverAgent  https://testerhome.com/topics/7220

&#160; &#160; &#160; &#160;WebDriverAgent天坑记  https://testerhome.com/topics/9666

&#160; &#160; &#160; &#160;STF 框架之 minicap 工具  https://testerhome.com/topics/3115



