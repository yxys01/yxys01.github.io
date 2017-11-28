---
layout: post
title: Objective-C内存管理学习之ARC规则
date: 2016-05-27
tag: Objective-C内存管理学习
---

### ARC规则

 - 不能使用`retain/release/retainCount/autorelease`
 - 不能使用`NSAllocateObject/NSDeallocateObject`
 - 须遵守内存管理的方法命名规则
 - 不要显式调用`dealloc`
 - 使用`@autoreleasepool`块代替`NSAutoreleasePool`
 - 不能使用区域（`NSZone`）
 - 对象型变量不能作为C语言结构体（`struct/union`）的成员
 - 显式转化“`id`”和“`void`”

&#160; &#160; &#160; &#160;不要显式调用`dealloc`：无论ARC是否有效，只要对象的所有者都不持有该对象，该对象就被废弃。对象被废弃时，无论ARC是否有效，都会调用对象的`dealloc`方法。