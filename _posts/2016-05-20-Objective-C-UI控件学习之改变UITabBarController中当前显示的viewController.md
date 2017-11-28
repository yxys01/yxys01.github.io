---
layout: post
title: Objective-C-UI控件学习之改变UITabBarController中当前显示的viewController
date: 2016-05-20
tag: Objective-C-UI控件学习
---

### 改变UITabBarController中当前显示的viewController
&#160; &#160; &#160; &#160;**1、selectedIndex属性**

&#160; &#160; &#160; &#160;通过该属性可以获得当前选中的**viewController**，设置该属性，可以显示**viewControllers**中对应的**index**的**viewController**。如果当前选中的是**MoreViewController**的话，该属性获取出来的值是**NSNotFound**，而且通过该属性也不能设置选中**MoreViewController**。设置**index**超出**viewControllers**的范围，将会被忽略。

&#160; &#160; &#160; &#160;**2、selectedViewController属性**

&#160; &#160; &#160; &#160;通过该属性可以获取到当前显示的**viewController**，通过设置该属性可以设置当前选中的**viewController**，同时更新**selectedIndex**。可以通过给该属性赋值`tabBarController.moreNavigationController`可以选中**moreViewController**。

&#160; &#160; &#160; &#160;**3、viewControllers属性**

&#160; &#160; &#160; &#160;设置**viewControllers**属性也会影响当前选中的**viewController**，设置该属性时**UITabBarController**首先会清空所有旧的**viewController**，然后部署新的**viewController**，接着尝试重新选中上一次显示的**viewController**，如果该**viewController**已经不存在的话，会接着尝试选中**index**和**selectedIndex**相同的**viewController**，如果该**index**无效的话，则默认选中第一个**viewController**。
