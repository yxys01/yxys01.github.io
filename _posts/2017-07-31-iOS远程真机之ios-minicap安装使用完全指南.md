---
layout: post
title: iOS远程真机之ios-minicap安装使用完全指南
date: 2017-07-31
tag: iOS远程真机
---
### ios-minicap简介

&#160; &#160; &#160; &#160;**minicap** 是开源项目 STF 中的高速截图工具。STF利用此工具不断的传输图片信息并在web端绘制实现 

&#160; &#160; &#160; &#160;以前只有Android版本，最近有新的ios版本，现在就安装过程中遇到的一些问题进行分享（ps:感谢sorccu 在issue里面给我的指点）

&#160; &#160; &#160; &#160;github地址：https://github.com/openstf/ios-minicap 

&#160; &#160; &#160; &#160;你可以git clone或者直接下载zip包。

### 安装教程

&#160; &#160; &#160; &#160;**1、准备工作**
```bash
$ brew install libjpeg-turbo

$ brew install cmake
```
&#160; &#160; &#160; &#160;**2、下载ios-minicap**
```bash
$ git clone https://github.com/openstf/ios-minicap
```

&#160; &#160; &#160; &#160;**3、build项目**
```bash
$ cd /User/yourname/ios-minicap

$ ./build.sh

$ ./run.sh
```
&#160; &#160; &#160; &#160;运行成功后，不要关闭该终端窗口

&#160; &#160; &#160; &#160;**4、运行demo**

&#160; &#160; &#160; &#160;重新打开一个终端端口

```bash
$ cd /User/yourname/ios-minicapexample

$ npm install

$ node app.js
```

&#160; &#160; &#160; &#160;全部成功运行后

&#160; &#160; &#160; &#160;**5、打开浏览器，输入网址`http://localhost:9002`**

### Q&A：

&#160; &#160; &#160; &#160;在README.MD中请注意下面的安装需求：

![这里写图片描述](http://img.blog.csdn.net/20170731145655771?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;我最开始没能注意这个要求，就直接`./build.sh` 当然是各种报错

&#160; &#160; &#160; &#160;首先安装 `libjpeg-turbo`

&#160; &#160; &#160; &#160;安装方式：`brew install libjpeg-turbo`

&#160; &#160; &#160; &#160;然后`./build.sh`是报这个错误

```bash
./open_xcode.sh: line 5: cmake: command not found
make: *** No targets specified and no makefile found. Stop.
```
&#160; &#160; &#160; &#160;然后我就去点击那个cmake的链接。。。最坑的来了，官网下载的都是APP文件，而`.build.sh` 里面内容如下：

```bash
#!/usr/bin/env bash

mkdir build
cd build
cmake ../
make
```
&#160; &#160; &#160; &#160;因为安装的cmake是APP，根本无法从脚本直接启动`CMakeLists.txt`，我就去issue里面提问题，才发现原来可以通过`brew`直接安装。。。

&#160; &#160; &#160; &#160;安装方法：`brew install cmake`

&#160; &#160; &#160; &#160;安装完成之后，再次运行`./build.sh`，cmake会自动编译配置文件，然后运行`./run.sh`

```bash
$ ./run.sh 

++ system_profiler SPUSBDataType
++ sed -n -E -e '/(iPhone|iPad)/,/Serial/s/ *Serial Number: *(.+)/\1/p'

UDID=0c6cxxxxxxxxxxe76dfdc55b57e0d1502ab92aab
PORT=12345
RESOLUTION=400x600
./build/ios_minicap --udid 0c6cxxxxxxxxxxe76dfdc55b57e0d1502ab92aab --port 12345 --resolution 400x600
EnableDALDevices
2017-07-31 12:24:26.081 ios_minicap[80709:3237274] Available devices:
2017-07-31 12:24:26.081 ios_minicap[80709:3237274] 0c6cxxxxxxxxxxe76dfdc55b57e0d1502ab92aab
2017-07-31 12:24:26.081 ios_minicap[80709:3237274] CC24414NH0XF9T9C7
```
&#160; &#160; &#160; &#160;由于个人隐私原因，将udid部分进行加密（就是用x去替代一部分而已啦）

&#160; &#160; &#160; &#160;我以为这个已经是启用成功

&#160; &#160; &#160; &#160;重新开启一个终端：

&#160; &#160; &#160; &#160;一步一步运行一下代码：

```bash
$ cd example

$ npm install

$ node app.js
```
&#160; &#160; &#160; &#160;运行到最后一步开始报错：

```bash
Listening on port 9002
Got a client
{ Error: connect ECONNREFUSED 127.0.0.1:12345
at Object.exports._errnoException (util.js:1026:11)
at exports._exceptionWithHostPort (util.js:1049:20)
at TCPConnectWrap.afterConnect [as oncomplete] (net.js:1136:14)
code: 'ECONNREFUSED',
errno: 'ECONNREFUSED',
syscall: 'connect',
address: '127.0.0.1',
port: 12345 }
Be sure to run ios-minicap on port 12345
```
&#160; &#160; &#160; &#160;最开始我也不知道怎么回事，后面才发现，或许是其他终端处理干净，12345端口未被启动或者被占用。

&#160; &#160; &#160; &#160;（ps：如果`address: '127.0.0.1',`一栏中提示的不是`127.0.0.1`本地地址，那有同学更改了host然后导致报错，将host改回即可）

&#160; &#160; &#160; &#160;解决方案：

&#160; &#160; &#160; &#160;kill掉所有的进程（或者强制退出终端）

&#160; &#160; &#160; &#160;再次在ios-minicap的目录下`/run.sh` 启动12345端口号：

&#160; &#160; &#160; &#160;启动信息如下

```bash
++ sed -n -E -e '/(iPhone|iPad)/,/Serial/s/ *Serial Number: *(.+)/\1/p'
++ system_profiler SPUSBDataType
+ UDID=0c6cxxxxxxxxxxe76dfdc55b57e0d1502ab92aab 
+ PORT=12345
+ RESOLUTION=400x600
+ ./build/ios_minicap --udid 0c6cxxxxxxxxxxe76dfdc55b57e0d1502ab92aab --port 12345 --resolution 400x600
EnableDALDevices
2017-07-31 14:43:46.851 ios_minicap[82104:3332798] Available devices:
2017-07-31 14:43:46.851 ios_minicap[82104:3332798] 0c6cxxxxxxxxxxe76dfdc55b57e0d1502ab92aab 
2017-07-31 14:43:46.851 ios_minicap[82104:3332798] CC24414NH0XF9T9C7
resolution: 400x600
Allocating 731648 bytes for JPEG encoder
== Banner ==
version: 1
size: 24
pid: 82104
real width: 400
real height: 600
desired width: 400
desired height: 600
orientation: 
quirks: 1
banner: 118b840109010058200901005820001
New client connection
```

&#160; &#160; &#160; &#160;重开一个终端窗口，定位到ios-minicap里面的example文件夹（就是cd到里面那个文件夹中）运行`node app.js`

&#160; &#160; &#160; &#160;提示：

```bash
Listening on port 9002
Got a client
```
&#160; &#160; &#160; &#160;在浏览器中打开`http://localhost:9002`

&#160; &#160; &#160; &#160;即可实时录制屏幕

![这里写图片描述](http://img.blog.csdn.net/20170731151657157?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


&#160; &#160; &#160; &#160;希望我的指南能帮助你们成功安装ios-minicap。

### ios-minicap 终极大招

&#160; &#160; &#160; &#160;最后，放上终极大招——我正在使用的，已经编译好的项目文件:

&#160; &#160; &#160; &#160;ios-minicap：链接：http://pan.baidu.com/s/1skNaatR 密码：rjs2

&#160; &#160; &#160; &#160;同样，如果百度链接挂了，就去CSDN中下载：[ios-minicap](http://download.csdn.net/download/yxys01/10024443)

&#160; &#160; &#160; &#160;如果使用存在问题，应该是路径问题，检查CMakeLists.txt中路径是否更改自己的 ios-minicap的本地路径。


### iOS-remote 安装篇

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 ios-minicap 安装使用完全指南](https://testerhome.com/topics/10456)

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 WebDriverAgent 安装使用完全指南](https://testerhome.com/topics/10463)

&#160; &#160; &#160; &#160;[iOS-remote 安装篇之 iOS-remote安装使用完全指南](https://testerhome.com/topics/10466)

### 参考文献
&#160; &#160; &#160; &#160;iOS-minicap + WDA 实现 ios 远程真机测试  https://testerhome.com/topics/10262

&#160; &#160; &#160; &#160;基于 WebDriverAgent 的 iOS 远程控制  https://testerhome.com/topics/8890

&#160; &#160; &#160; &#160;iOS 远程真机 (仅限屏幕查看)  https://testerhome.com/topics/6470
