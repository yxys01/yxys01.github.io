---
layout: post
title: Objective-C-UI控件学习之UIViewAutoresizing（自动布局）
date: 2016-05-24
tag: Objective-C-UI控件学习
---
<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>UIViewAutoresizing</td>
    <td>是一个枚举类型，默认是UIViewAutoresizingNone，也就是不做任何处理</td>
    </tr>
    <tr>
        <td>UIViewAutoresizingNone</td>
    <td>不会随父视图的改变而改变</td>
    </tr>
     <tr>
        <td>UIViewAutoresizingFlexibleLeftMargin</td>
    <td>自动调整view与父视图左边距，以保证右边距不变</td>
    </tr>
     <tr>
        <td>UIViewAutoresizingFlexibleWidth</td>
    <td>自动调整view的宽度，保证左边距和右边距不变</td>
    </tr>
    <tr>
        <td>UIViewAutoresizingFlexibleRightMargin</td>
    <td>自动调整view与父视图右边距，以保证左边距不变</td>
    </tr>
    <tr>
        <td>UIViewAutoresizingFlexibleTopMargin</td>
    <td>自动调整view与父视图上边距，以保证下边距不变</td>
    </tr>
     <tr>
        <td>UIViewAutoresizingFlexibleHeight</td>
    <td>自动调整view的高度，以保证上边距和下边距不变</td>
    </tr>
     <tr>
        <td>UIViewAutoresizingFlexibleBottomMargin</td>
    <td>自动调整view与父视图的下边距，以保证上边距不变</td>
    </tr> 
</table>

```
[self.pageViewController.view setAutoresizingMask:(UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight)];//自动调整view的宽度，保证上下左右边距不变
```
更多资料参考：
[自动布局之autoresizingMask使用详解（Storyboard&Code）](http://www.cocoachina.com/ios/20141216/10652.html)



