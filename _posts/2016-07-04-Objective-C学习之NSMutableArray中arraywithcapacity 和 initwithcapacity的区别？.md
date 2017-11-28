---
layout: post
title: Objective-C学习之NSMutableArray中arraywithcapacity 和 initwithcapacity的区别？
date: 2016-07-04
tag: Objective-C学习
---

 在使用NSMutableArray时，初始化数组有这两个方法：

```objectivec
 arraywithcapacity
 
 initwithcapacity
```

#### 区别：
`arrayWithCapacity`是`class method`是`autorelease`的；
`initWithCapacity`需要自己`release`。

即一个自动释放，一个需要手动释放