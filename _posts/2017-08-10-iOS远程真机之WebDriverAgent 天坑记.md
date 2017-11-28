---
layout: post
title: iOS远程真机之WebDriverAgent天坑记
date: 2017-08-10
tag: iOS远程真机
---
### 一、WDA安装依赖报错：
![这里写图片描述](http://img.blog.csdn.net/20170808164448405?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;这个东西神坑，我搞了一天都没找到解决方案，最后在appium讨论中发现，

&#160; &#160; &#160; &#160;**解决方案**是：

&#160; &#160; &#160; &#160;先定位到WebDriverAgent 所在路径
```
$ cd /Users/XXXX/git/WebDriverAgent 
```
&#160; &#160; &#160; &#160;然后运行：

```
mkdir -p Resources/WebDriverAgent.bundle
sh ./Scripts/bootstrap.sh
```
&#160; &#160; &#160; &#160;成功安装

![这里写图片描述](http://img.blog.csdn.net/20170809165055631?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;而不是WebDriverAgent  GitHub上说的`./Scripts/bootstrap.sh`

### 二、WDA运行失败

&#160; &#160; &#160; &#160;通过xcode启动WDA，在控制台可以看到

&#160; &#160; &#160; &#160;![这里写图片描述](http://img.blog.csdn.net/20170809172422556?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;通过终端命令启动

```
PASSWORD="replace-with-your-password"
security unlock-keychain -p $PASSWORD ~/Library/Keychains/login.keychain

UDID=$(idevice_id -l | head -n1)

xcodebuild -project WebDriverAgent.xcodeproj -scheme WebDriverAgentRunner -destination "id=$UDID" test
```
![这里写图片描述](http://img.blog.csdn.net/20170809172434675?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;**错误原因**：没有运行bootstrap

&#160; &#160; &#160; &#160;也有说是：`WebDriver becomes unresponsive after certain number of requests`

&#160; &#160; &#160; &#160;即：在一定数量的请求之后，WebDriver会变得无响应

&#160; &#160; &#160; &#160;**解决方案**：

![这里写图片描述](http://img.blog.csdn.net/20170810113959038?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;图片可能有点看不清

&#160; &#160; &#160; &#160;WebDriverAgentLib->Build Setting->Runpath Search Paths->添加变量：

```
$(SRCROOT)/../Carthage/Build/iOS
$(PROJECT)/Carthage/Build/iOS
```

![这里写图片描述](http://img.blog.csdn.net/20170810114016404?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;WebDriverAgentLib->Build Setting->Build Active Architecture Only->No

&#160; &#160; &#160; &#160;你们以为这样就能运行吗？

&#160; &#160; &#160; &#160;并不是！

&#160; &#160; &#160; &#160;最关键一步来了：

你要用数据线连着电脑重启你的手机！！！！
你要用数据线连着电脑重启你的手机！！！！
你要用数据线连着电脑重启你的手机！！！！

&#160; &#160; &#160; &#160;重要的话要说三遍！

&#160; &#160; &#160; &#160;这个方法我确实不知道原来，我去WDA里面提issue，开发者给我说是Xcode的问题，现在还没解决。。。

&#160; &#160; &#160; &#160;但是用数据线连着电脑重启你的手机后，我确实运行成功了

![这里写图片描述](http://img.blog.csdn.net/20170810114546450?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;而且最神奇的事情是：我由于有点事情，断掉了数据线连接，等我再次用iPhone连接Mac的时候，又报错了，和前面一样。。。这个原理我真是很绝望。。。这里我也只能提供解决思路了，这个问题我真的没弄懂，希望有大神解决后告诉我下！

### 2017-8-16再次更新

&#160; &#160; &#160; &#160;这几天我WDA还是不重启就运行不起，再次尝试将facebook的WDA项目git下来，然后发现：

```bash
$ mkdir -p Resources/WebDriverAgent.bundle
$ sh ./Scripts/bootstrap.sh
```
&#160; &#160; &#160; &#160;已经无法解决问题了，还是会报错，且同
![这里写图片描述](http://img.blog.csdn.net/20171020114504150?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
&#160; &#160; &#160; &#160;然后又是漫长的寻找解决方案，然后发现这个方法可以使用：

&#160; &#160; &#160; &#160;把 `WebDriverAgent/Inspector/webpack.config.js` 中的

```js
loaders: [
      { test: /\.js?$/, loaders: ['babel-loader'], exclude: /node_modules/ },
      { test: /\.css?$/, loader: 'style-loader!css-loader' },
    ]
```
&#160; &#160; &#160; &#160;改为

```js
loaders: [
      { test: /\.js?$/, loaders: ['babel-loader'] },
      { test: /\.css?$/, loader: 'style-loader!css-loader' },
    ]
```
&#160; &#160; &#160; &#160;把 `, exclude: /node_modules/` 这部分去掉即可！