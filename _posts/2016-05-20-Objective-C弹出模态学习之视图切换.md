---
layout: post
title: Objective-C弹出模态学习之视图切换
date: 2016-05-20
tag: Objective-C弹出模态学习
---

### 视图切换
&#160; &#160; &#160; &#160;没有NavigationController的情况下，一般会使用`presentViewController`来切换视图并携带切换时的动画

### 切换方法
&#160; &#160; &#160; &#160;其中**切换方法**如下：

&#160; &#160; &#160; &#160;`– presentViewController:animated:completion:` 弹出，出现一个新视图 可以带动画效果，完成后可以做相应的执行函数经常为nil

&#160; &#160; &#160; &#160;`– dismissViewControllerAnimated:completion:`退出一个新视图 可以带动画效果，完成后可以做相应的执行函数经常为nil
