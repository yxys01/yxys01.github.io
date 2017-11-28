---
layout: post
title: iOS远程真机之wdaproxy使用指南
date: 2017-08-08
tag: iOS远程真机
---
[基于 WebDriverAgent 的 iOS 远程控制](https://testerhome.com/topics/8890)
[WebDriverAgent 安装使用完全指南](https://testerhome.com/topics/10463)

一、命令行启动wdaproxy
![这里写图片描述](http://img.blog.csdn.net/20170808150332277?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;在浏览器打开http://localhost:8100

![这里写图片描述](http://img.blog.csdn.net/20170808150345428?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;**问题**：WDA未启动

&#160; &#160; &#160; &#160;WDA安装依赖报错：

![这里写图片描述](http://img.blog.csdn.net/20170808164448405?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;这个东西神坑，我搞了一天都没找到解决方案，最后在appium讨论中发现，解决方案是：

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

二、`go build main.go`报错
![这里写图片描述](http://img.blog.csdn.net/20170904105319329?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;错误原因：`mockIOSPrivider`、`NewReverseProxyHandlerFunc`、`HTTPLogger` 是package main下的其他.go文件里面的方法函数，要想`go build main.go`，必须先编译其他几个go文件。

&#160; &#160; &#160; &#160;**解决方案**：先`go build *.go`,再`go run *.go`，即可成功运行

&#160; &#160; &#160; &#160;若要**重新打包**：

```
go generate ./web
go build -tags vfs
```

&#160; &#160; &#160; &#160;注：`$ go env` 查看go语言环境

![这里写图片描述](http://img.blog.csdn.net/20170904105523655?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)