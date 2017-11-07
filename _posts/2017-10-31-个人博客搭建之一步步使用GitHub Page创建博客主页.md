---
layout: post
title: 个人博客搭建之一步步使用Github Page创建博客主页（1）
date: 2017-10-31 
tag: 个人博客
---
&#160; &#160; &#160; &#160;前几天突发奇想，准备完成我以前一直想做却因为各种原因推迟的工作：建立一个技术向的个人博客

&#160; &#160; &#160; &#160;这个想法在我心里已经存在很多年了，这也是我在CSDN，在简书，在Testerhome里面写各种文章的原因之一。

&#160; &#160; &#160; &#160;诸君，我喜欢文字，也喜欢将其分享给大家；再结合工作，在我看来，这是一件再美好不过的事情了。

&#160; &#160; &#160; &#160;最开始我是想找网上已有的博客网站来写自己的文章：

&#160; &#160; &#160; &#160;然后就在知乎中的[目前最好的博客网站是哪个？](https://www.zhihu.com/question/19759810) 和[写技术博客用哪个博客比较好？](https://www.zhihu.com/question/21739407) 两文中看到了很多可选平台：
* TOC
{:123}

* TOC
{:toc}
| 博客       | 优点           | 缺点  |国内外|
| ------------- |:-------------| :-----|:-----|
| 博客中国    |使用方便、界面简洁、速度和稳定性方面做的不错 | 1、管理界面人机交互性不够好；2、目前还不能给其他的博客文章发引用通告；3、文件上传空间太小，才10M；4、访问有时不太稳定。 |国内|
| 知乎专栏     |       |  |国内|
| 新浪博客 | 页面使用要稍好一些    |  乱弹广告|国内|
| 网易博客     |大牛用户多一些 | |国内|
| blogger     |美观简洁方便实用的在线博客工具     |  被墙了 |国外|
| wordpress |美观简洁方便实用的在线博客工具  |     被墙了 |国外|
| 简书     |沉淀心情和思想；支持Markdown语法，写作体验很好|主要是写一些非技术文章比较多，技术类的文章在这里关注度不高，对个人成就感也有一定影响。|国内|
| 豆瓣    |      |    |国内|
| github page |显得比较专业     |因为其专业性，上手比较慢。繁琐的操作有时候会让人花更多的经理在语法上，而不是写文章这件事本身上。 |国外|
|  CSDN     |专业的技术社区| 整体站点比较老了，写博客时的bug很多，且新人流量低 |国内|
|开源中国 |美观简洁方便实用的在线博客工具  |开源中国似乎目前主要精力在做码云，博客区没有在迭代新功能了，使用markdown遇到过好几次崩溃问题，开发人员跟进比较慢。目前流量也比较低了。|国内|
| Github    | |有seo的问题，而且DIY成分比较大，推广也比较困难|国外|
| SegmentFault|流量比较大，目前技术讨论的氛围比较好，文章阅读体验也相对比较好|  |国内|
|cnblog| 界面简洁||国内|
|博客园| 界面简洁||国内|
|gitbook |分门别类很清楚，可以通过 git 管理，支持 md；真有种好像在写书的感觉。||国内|
|自己搭建独立博客|可以有更多的发挥空间，推荐wordpress，结构简单，能很快被搜索引擎收录|||


&#160; &#160; &#160; &#160;总之，各有各的优缺点，要想找一个完全属于自己的博客空间，还是建议自己建一个。

&#160; &#160; &#160; &#160;在比较完几个自己搭建独立博客的方法后，我觉得用Github Page的方式非常适合我这种技术向人员来搭建自己的独立博客。
###github page
####github-page是一个免费的静态网站托管平台，由github提供，它具有以下特点：

 1. 免空间费，免流量费
 2. 具有项目主页和个人主页两种选择
 3. 支持页面生成，可以使用jekyll来布局页面，使用markdown来书写正文
 4. 可以自定义域名

&#160; &#160; &#160; &#160;So，选型完毕后，我们来比较一下Github Page建博客常用的几个框架
|Github Page搭建框架       | 优点          | 
| ------------- |:-------------| 
|Hexo     |  | 
|jekyll     |好用，教程非常详细      |  
| octopress|       |
|Hugo|      |

&#160; &#160; &#160; &#160;对于一个初学者来说，我决定使用jekyll来建立我的第一个独立博客（Ps：我才不会说是因为教程比较多呢！）

&#160; &#160; &#160; &#160;**参考文章：**

&#160; &#160; &#160; &#160;[一步步在GitHub上创建博客主页(1-7)](http://www.pchou.info/ssgithubPage/2013-01-03-build-github-blog-page-01.html)

&#160; &#160; &#160; &#160;[一步步在GitHub上创建博客主页-最新版](http://blog.csdn.net/wave_1102/article/details/41548951)

&#160; &#160; &#160; &#160;以上是一个系列的文章，讲解非常详细，但是Mac上使用还是存在一些出入和问题

&#160; &#160; &#160; &#160;[Jekyll搭建个人博客](https://yxys01.github.io/2016/10/jekyll_tutorials1/)

&#160; &#160; &#160; &#160;[如何利用github打造博客专属域名](http://blog.csdn.net/lmj623565791/article/details/51319147)

&#160; &#160; &#160; &#160;[创建GitHub技术博客全攻略](http://blog.csdn.net/renfufei/article/details/37725057)

&#160; &#160; &#160; &#160;[我的 Github 个人博客是怎样炼成的](http://www.jianshu.com/p/4fd3cb0a11da)


&#160; &#160; &#160; &#160;这里引用一段[一步步在GitHub上创建博客主页(1-7)](http://www.pchou.info/ssgithubPage/2013-01-03-build-github-blog-page-01.html) 中的话：
>本系列文章将一步步教你如何在GitHub上创建自己的博客或主页，事实上相关的文章网上有很多，这里只是把自己的经验分享给新手，方便他们逐步开始GitHub之旅。
>
>本篇介绍GitHub提供的个人博客及其关键技术，以便读者决策。GitHub十分“给力”，不仅为程序员提供了免费源代码托管空间，还为程序员提供了一个社交平台，允许大家在GitHub上创建自己的博客网站或主页（[github pages](https://pages.github.com/)），而且免费，不限流量，还可以绑定自己的域名。
>
>不过遗憾的是，GitHub提供的主页实际上是基于GitHub的源代码实现的，所以只支持上传静态的网页，不能在上面创建真正的博客系统。不过，不幸中的万幸是，GitHub支持一种叫jekyll的静态页面转换引擎，也就是说只要上传符合jekyll规范的文件，GitHub会用这种模板引擎为你转化静态页面和网站。

&#160; &#160; &#160; &#160;好，废话也吧啦了半天，开始进入正题~~~~

&#160; &#160; &#160; &#160;嗯，第一个部分我们也不讲太多复杂的，简单讲一下在Github网站上的一系列操作吧，也为后面使用jekyll提供准备工作。

## 第一部分

### 第一步

#### 1.1 注册账号
&#160; &#160; &#160; &#160;首先你需要一个github的账号，立志作为一名优秀的程序员，这个账号是应该有的，如果没有赶快申请一个。

&#160; &#160; &#160; &#160;地址: https://github.com/

&#160; &#160; &#160; &#160;输入账号、邮箱、密码,然后点击注册按钮.

![这里写图片描述](http://img.blog.csdn.net/20171031154712938?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 1.2 初始设置

&#160; &#160; &#160; &#160;注册完成后,选择Free免费账号完成设置。

![这里写图片描述](http://img.blog.csdn.net/20171031155005669?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 1.3 验证邮箱

&#160; &#160; &#160; &#160;请打开你的邮箱，查看发送给你的确认邮件，你需要验证邮箱后,后面生成的个人主页才会被接受和发布.

&#160; &#160; &#160; &#160;Ps:这几步实在是简单，我就直接去网上盗的图，请勿吐槽。
### 第二步

#### 2.1 新建仓库

&#160; &#160; &#160; &#160;有了账号以后，首先点击新建仓库，如图：

![这里写图片描述](http://img.blog.csdn.net/20171031155447414?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
#### 2.2 填写仓库信息

&#160; &#160; &#160; &#160;然后到达仓库信息填写界面，如图：

![这里写图片描述](http://img.blog.csdn.net/20171031155522802?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;这里只要注意一个地方，就是**仓库的名称**

&#160; &#160; &#160; &#160;如果后面是在`master`分支中进行建站，仓库名必须是：`你的用户名.github.io`，即为：`yxys01.github.io`

&#160; &#160; &#160; &#160;如果后面是在`gh-pages`分支中进行建站，仓库名则可任意命名为`Myblog`之类的

### 第三步

#### 3.1 管理仓库

&#160; &#160; &#160; &#160;创建了仓库后，我们就需要管理它，无论是管理本地仓库还是远程仓库都需要Git客户端。Git客户端实际上十分强大，它本身就可以offline的创建本地仓库，而本地仓库和远程仓库之间的同步也是通过Git客户端完成的。


![这里写图片描述](http://img.blog.csdn.net/20171031155920820?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

#### 这里存在两种方式来clone项目，且存在两种分支来启用项目（master and gh-pages）

### 第一种：Github Desktop+master分支

&#160; &#160; &#160; &#160;这种要求仓库的名称，必须是：`你的用户名.github.io`，例如我的用户名是yxys01，我填写的仓库名称即为：`yxys01.github.io`。

&#160; &#160; &#160; &#160;我的电脑是 Mac, 选择 GitHub for Mac，然后将线上的 repository 克隆到本地 (我下载了 Github Desktop 用于同步，你也可以使用 Git 同步，看个人喜好)。

&#160; &#160; &#160; &#160;Clone 后，你会看到如下界面。
![这里写图片描述](http://img.blog.csdn.net/20171031160124331?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;打开 sublime 编辑器，新建 index.html，输入你心中此时此刻所想，保存，如下图。

![这里写图片描述](http://img.blog.csdn.net/20171031161824896?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

&#160; &#160; &#160; &#160;更新成功之后，那就要恭喜你了，你的个人站点搭建成功了。

&#160; &#160; &#160; &#160;你肯定又要说，你忽悠谁呢，顶多算你新建了一个仓库，提交了一个html文件而已，这里我要说，No No No，你的个人站点真的搭建好了，你已经可以给你的亲朋好友炫耀了，那么站点总要有个访问的地址吧，不然怎么访问呢？

&#160; &#160; &#160; &#160;恩，是的，默认的地址是:

```
http://yxys01.github.io
```
&#160; &#160; &#160; &#160;通过浏览器打开这个链接http://yxys01.github.io，便可以看到我们建立的一个网站了

&#160; &#160; &#160; &#160;看到没有，我们刚才编写的简单html文件已经可以通过特定的url访问了，恩，你记得修改为你自己的url。

&#160; &#160; &#160; &#160;如果你的html、css、js技术足够好，你完全可以利用这样的方式搭建一个高逼格且实用的个人站点，当然你也可以在上面搭建你的简历，方便打印，不过注意保护个人隐私。

&#160; &#160; &#160; &#160;ok，到这里，我们已经教会大家如何利用github pages去搭建个人站点了，哈，免费的个人站点。如果我大学时候知道这个功能，我至少网页设计可以多拿10分，恩，那会我得了90分。

&#160; &#160; &#160; &#160;至于这个页面好不好看，看你的才华了；这个页面能干什么，看你的想象了。
### 第二种 命令行 + gh-pages分支

&#160; &#160; &#160; &#160;如果你不想用Github Desktop，而是使用命令行

&#160; &#160; &#160; &#160;创建一个目录，该目录与上面的项目名同名，在该目录下启用Git Bash命令行，并输入如下命令

```
$ git init
```

&#160; &#160; &#160; &#160;该命令实际上是在该目录下初始化一个本地的仓库，会在目录下新建一个`.git`的隐藏文件夹，可以看成是一个仓库数据库。

&#160; &#160; &#160; &#160;创建一个没有父节点的分支gh-pages，并自动切换到这个分支上：

```
$git checkout --orphan gh-pages
```

&#160; &#160; &#160; &#160;在Git中，分支(branch)的概念非常重要，Git之所以强大，很大程度上就是因为它强大的分支体系。这里的分支名字必须是`gh-pages`，因为github规定，在项目类型的仓库中，只有该分支中的页面，才会生成网页文件。

&#160; &#160; &#160; &#160;在该目录下手动创建如下文件和文件夹，最终形成这样的结构：
![这里写图片描述](http://img.blog.csdn.net/20171031160416973?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

 - _includes：默认的在模板中可以引用的文件的位置，后面会提到
 - _layouts：默认的公共页面的位置，后面会提到
 - _posts：博客文章默认的存放位置
 - .gitignore：git将忽略这个文件中列出的匹配的文件或文件夹，不将这些纳入源码管理
 - _config.yml：关于jekyll模板引擎的配置文件
 - index.html：默认的主页

&#160; &#160; &#160; &#160;在`_layouts`目录下创建一个`default.html`，在其中输入如下内容，特别注意：文件本身要以`UTF-8 without BOM`的格式保存，以防止各种编码问题，建议使用`notepad++`或`sublime`编辑（Ps：个人强烈推荐`sublime text 3`）
&#160; &#160; &#160; &#160;**default.html**
```
<!DOCTYPE html>
	<html>
	<head>
	　<meta http-equiv="content-type" content="text/html; charset=utf-8" />
	　<title>一步步在GitHub上创建博客主页(2)</title>
	</head>
	<body>
	　{{content }}
	</body>
	</html>
```
&#160; &#160; &#160; &#160;编辑**index.html**

```
---
layout: default
title: test title
---
<p>Hello world!</p>
```

&#160; &#160; &#160; &#160;编辑**_config.yml**

```
encoding: utf-8
```

&#160; &#160; &#160; &#160;再次打开Git Bash，先后输入如下命令：

```bash
# 将当前的改动暂存在本地仓库
$ git add .
# 将暂存的改动提交到本地仓库，并写入本次提交的注释是”first post“
$ git commit -m "first post"
# 将远程仓库在本地添加一个引用：origin
$ git remote add origin https://github.com/username/projectName.git
# 向origin推送gh-pages分支，该命令将会将本地分支gh-pages推送到github的远程仓库，并在远程仓库创建一个同名的分支。该命令后会提示输入用户名和密码。
$ git push origin gh-pages
```

&#160; &#160; &#160; &#160;据网友反应，如果是初次安装git的话，在commit的时候会提示需要配置username和email，请读者注意根据提示配置一下，至于username和email可以随便填

&#160; &#160; &#160; &#160;现在，你可以泡杯咖啡，并等大约10分钟的时间，访问http://username.github.com/projectName就可以看到生成的博客了

&#160; &#160; &#160; &#160;另外上面提到的，无论生成失败还是成功，Github会向你的邮箱发送一封邮件说明，请注意查收。