---
layout: post
title: Objective-C弹出模态学习之纯代码跳转到xib界面以及storyboard界面
date: 2016-07-27
tag: Objective-C弹出模态学习
---

&#160; &#160; &#160; &#160;现在在iOS开发中，有三种开发UI的方式，**纯代码**，**xib**，**storyboard**。

&#160; &#160; &#160; &#160;**1，跳转到xib** 

&#160; &#160; &#160; &#160;假设有一个按钮，这个按钮就是实现跳转的，那么在这个按钮的点击事件中，代码可以这样写。 

```objectivec
SCViewController *sc1= [[SCViewController alloc]initWithNibName:@”SCViewController” bundle:[NSBundle mainBundle]]; 
[self.navigationController pushViewController:sc1 animated:YES]; 
```

&#160; &#160; &#160; &#160;**2,跳转到storyboard** 

&#160; &#160; &#160; &#160;如上，代码可以这样写 

```objectivec
  UIStoryboard *storyboard = [UIStoryboard storyboardWithName:@"Main" bundle:nil];
  SCTabBarController *vc = [storyboard instantiateInitialViewController];
  [self presentViewController:vc animated:YES completion:nil];
```