---
layout: post
title: Objective-C学习之clipsToBounds的应用
date: 2016-05-20
tag: Objective-C学习
---

#### view添加view，并剪边(UIView属性clipsTobounds的应用)

如题，有两个view： view1,view2

view1添加view2到其中，如果view2大于view1，或者view2的坐标不在view1的范围内，view2是盖着view1的，意思就是超出的部份也会画出来

UIView有一个属性，clipsTobounds 默认情况下是NO,
如果，我们想要view2把超出的那部份隐藏起来的话，就得改变它的父视图也就view1的clipsTobounds属性值。

```
view1.clipsTobounds = YES;
```