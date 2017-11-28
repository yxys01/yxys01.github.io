---
layout: post
title: Objective-C内存管理学习之autorelease
date: 2016-05-27
tag: Objective-C内存管理学习
---

&#160; &#160; &#160; &#160;调用autorelease方法，可以使取得的对象存在，但自己不持有对象。autorelease提供这样的功能，使对象在超出指定的生成范围时能够自动并正确地释放（调用release方法）。

&#160; &#160; &#160; &#160;autorelease的具体使用方法如下：

 1. 生成并持有NSAutoreleasePool对象；
 2. 调用已分配对象的autorelease实例方法；
 3. 废弃NSAutoreleasePool对象。（自动调用release）

&#160; &#160; &#160; &#160;注意：在大量产生autorelease的对象时，只要不废弃NSAutoreleasePool对象，那么生成的对象就不能被释放，隐藏会产生内存不足的现象。典型的例子是读入大量图像的同时改变其尺寸。图像文件读入NSData对象，并从中生成UIImage对象，改变该对象尺寸后生成新的UIImage对象。这种情况下，就会大量产生autorelease的对象。

&#160; &#160; &#160; &#160;在此情况下，有必要在适当的地方生成、持有或废弃NSAutoreleasePool对象。

&#160; &#160; &#160; &#160;**提问：如果autorelease NSAutoreleasePool对象会如何？**

&#160; &#160; &#160; &#160;回答：发生异常

&#160; &#160; &#160; &#160;通常在使用Objective-C，也就是Foundation框架时，无论调用哪一个对象的autorelease实例方法，实现上是调用的都是NSObject类的autorelease实例方法。但是对于NSAutoreleasePool类，autorelease实例方法已被该类重载，因此运行时就会出错。
