---
layout: post
title: 个人博客搭建之一步步使用Github Page创建博客主页（2）
date: 2017-10-31 
tag: 个人博客搭建
---

&#160; &#160; &#160; &#160;上一节我们讲到如何选型以及Github Page的初步搭建

&#160; &#160; &#160; &#160;今天我们要做的是用jekyll框架来做一个个人博客的**模板**

### 关于jekyll
&#160; &#160; &#160; &#160;在开始之前，有必要详细总结一下这个jekyll是什么。上面提到了它实际上是一个模板转化引擎。它同时也是GitHub上的一个开源项目：Jekyll

&#160; &#160; &#160; &#160;jekyll本身基于Ruby，它实际上也可以看成是一种模板引擎liquid的扩展。jekyll对liquid的主要扩展在于两点：

 - 内建专用于博客网站的对象，可以在模板中引用这些对象：page、site等
 - 对liquid进行了扩展，方便构建博客网站

&#160; &#160; &#160; &#160;类似其他的模板引擎一样，标记是模板引擎解析的关键，liquid设计了如下两种标记：

 - ``` {{ }} ```：此标记表征的是将其中的变量转化成文本
 - ``` {% %} ```：此标记用于包含控制流关键字，比如：``` {% if %} ```、``` {% for x in xx %}  ```

&#160; &#160; &#160; &#160;显而易见的是，有了这种标记的支持，再加上jekyll内建的对象，构建网站就方便不少了。

&#160; &#160; &#160; &#160;可能有朋友会更其他的服务器端脚本语言比较，比如**asp**、**razor**、**jsp**、**velocity**…，但是一定要记得的是，jekyll对模板的解析仅仅只有一次，它的目标就是将模板一次性的转化成静态网站，而不是上述的动态网站脚本语言。

### 维护流程

 1. 利用本地编辑器编写博客后维护网站其他页面
 2. 使用Jekyll-Bootstrap在本地测试网站功能
 3. 使用Git客户端工具上传模板和页面文件
 4. Git Server会用jekyll转化你的模板，并生成静态页面

&#160; &#160; &#160; &#160;好，简单介绍一下jekyll，然后我们开始搭建jekyll环境

&#160; &#160; &#160; &#160;jekyll本身是基于Ruby的，**第一步**肯定是配置Ruby环境

### Ruby环境配置
&#160; &#160; &#160; &#160;jekyll本身基于Ruby开发，因此，想要在本地构建一个测试环境需要具有Ruby的开发和运行环境。

&#160; &#160; &#160; &#160;我是用的是**Mac**，Mac安装Ruby很简单，可以通过Homebrew直接安装

#### 安装Homebrew：
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
&#160; &#160; &#160; &#160;安装使用可见：[Mac之安装并使用Homebrew](http://blog.csdn.net/yxys01/article/details/77452318)

#### 安装Ruby

```
brew install ruby
```
![这里写图片描述](http://img.blog.csdn.net/20171031163359001?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 查看Ruby版本
```
ruby -v

```
![这里写图片描述](http://img.blog.csdn.net/20171031163428764?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;这里可以看见ruby安装版本是2.4.2_1,但是`ruby -v` 显示的还是2.0（Mac自带的ruby版本）

#### 如何解决这个问题呢？

&#160; &#160; &#160; &#160;这个则需要安装rvm

#### 首先查看你是否安装过rvm

```
rvm -v
```

&#160; &#160; &#160; &#160;如果没有则是需要安装。

#### 安装rvm


```
curl -L get.rvm.io | bash -s stable
```
![这里写图片描述](http://img.blog.csdn.net/20171031164926738?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
#### 再输入

```
source ~/.rvm/scripts/rvm
```

#### 再次查看版本
![这里写图片描述](http://img.blog.csdn.net/20171031165020803?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 解决ruby版本不同步的方法

```
__rvm_rm_rf /Users/LL.F/.rvm/rubies/ruby-2.4.2_1
```
#### 再次查看ruby版本

![这里写图片描述](http://img.blog.csdn.net/20171031163711708?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
&#160; &#160; &#160; &#160;具体详情可见：[终端更新Ruby步骤和遇见奇葩问题的解决办法](http://www.jianshu.com/p/8169f5d7f364)

&#160; &#160; &#160; &#160;
总之，经过漫长的奋斗，终于把Ruby在Mac上配置好了

&#160; &#160; &#160; &#160;**第二步**:安装Rubygems

### Rubygems
&#160; &#160; &#160; &#160;Rubygems是类似Radhat的RPM、centOS的Yum、Ubuntu的apt-get的应用程序打包部署解决方案。Rubygems本身基于Ruby开发，在Ruby命令行中执行。我们需要它主要是因为jekyll的执行需要依赖很多Ruby应用程序，如果一个个手动安装比较繁琐。jekyll作为一个Ruby的应用，也实现了Rubygems打包标准。只要通过简单的命令就可以自动下载其依赖。

&#160; &#160; &#160; &#160;[gems下载地址](http://download.csdn.net/download/yxys01/10047058)

&#160; &#160; &#160; &#160;解压后，用终端进入到解压后的目录，执行命令即可：

```
$ruby setup.rb
```
![这里写图片描述](http://img.blog.csdn.net/20171031170521902?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;注意：存在权限不足的情况下用`sudo` 解决

&#160; &#160; &#160; &#160;就像yum仓库一样，仓库本身有很多，如果希望加快应用程序的下载速度，特别绕过“天朝”的网络管理制度，可以选择国内的仓库镜像，taobao有一个：https://ruby.taobao.org/。配置方法这个链接里面很完全。

### 安装jekyll
&#160; &#160; &#160; &#160;有了上面的基础，安装jekyll就十分轻松了，执行下面gem命令即可全自动搞定：

```
$gem install jekyll
```
### 安装Bundle
&#160; &#160; &#160; &#160;直接使用下面命令即可：
```
$ gem install bundle
```
&#160; &#160; &#160; &#160;jekyll依赖的组件会自动下载安装

### Gemfile和Bundle安装

&#160; &#160; &#160; &#160;在根目录下创建一个叫Gemfile的文件，注意没有后缀，输入
```
source 'https://ruby.taobao.org/'
gem 'github-pages'
```
&#160; &#160; &#160; &#160;保存后，在命令行中执行
```
$ bundle install
```
&#160; &#160; &#160; &#160;命令会根据当前目录下的Gemfile，安装所需要的所有软件。这一步所安装的东西，可以说跟github本身的环境是完全一致的，所以可以确保本地如果没有错误，上传后也不会有错误。而且可以在将来使用下面命令，随时更新环境，十分方便
```
$ bundle update
```
&#160; &#160; &#160; &#160;使用下面命令，启动转化和本地服务：
```
$ bundle exec jekyll serve
```

### 注意：
&#160; &#160; &#160; &#160;实际使用中存在很多问题
#### 1、`bundle install` 后报错：
>Could not find gem 'github-pages' in any of the gem sources listed in your Gemfile.

#### **解决方案：**
#### 安装github-pages
```
$ cd
$ sudo gem install github-pages
```
&#160; &#160; &#160; &#160;（Ps：`gem update github-pages`命令可以用来更新 Jekyll，以免 Github 服务器更新导致网站本地和线上表现不同）
#### 2、bundle install时报错
>Could not fetch specs from http://ruby.taobao.org/

#### **解决方案：**
&#160; &#160; &#160; &#160;修改Gemfile下的`http://ruby.taobao.org/`为：
```
https://ruby.taobao.org/
```
#### 3、bundle exec jekyll serve报错
>Could not find liquid-3.0.6 in any of the sources

#### **解决方案：**
&#160; &#160; &#160; &#160;先将bundle更新到最新版本

```
gem install bundler --pre
```
&#160; &#160; &#160; &#160;然后在根目录再次
```
bundle install
```

&#160; &#160; &#160; &#160;解决！

### 使用 Jekyll 模板个性化博客

&#160; &#160; &#160; &#160;博客基于jekyll，而新手往往摸不着头脑，幸好有一些[现成的模板](http://jekyllthemes.org/)可以直接使用：
![这里写图片描述](http://img.blog.csdn.net/20171031172046586?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;以[White Paper](http://jekyllthemes.org/themes/white-paper/)这个模板为例，可以直接下载压缩包，也可以使用如下命令clone到本地：
```
$ git clone https://github.com/vinitkumar/white-paper.git
```
&#160; &#160; &#160; &#160;把克隆下来的文件拷贝到你自己的目录就行了，这样你就有一个现成的网站结构了：

![这里写图片描述](http://img.blog.csdn.net/20171031172238046?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;有了现成的网站结构，还是需要`bundle install` 将相关内容更新下来，然后push给master分支（gh-pages分支的push见[一步步在GitHub上创建博客主页](http://www.pchou.info/ssgithubPage/2013-01-05-build-github-blog-page-02.html) 系列文章）

&#160; &#160; &#160; &#160;然后打开https://yxys01.github.io/ 便可访问到我的个人博客主页(ps:https://www.yxys01.com 也可以访问到哦)




