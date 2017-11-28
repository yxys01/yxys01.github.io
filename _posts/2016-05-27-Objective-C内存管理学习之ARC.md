---
layout: post
title: Objective-C内存管理学习之ARC
date: 2016-05-27
tag: Objective-C内存管理学习
---

### 简介   
 &#160; &#160; &#160; &#160;自动引用计数（ARC，Automatic Reference Counting）是指内存管理中对引用采取自动计数的计数。以下 摘自苹果的官方说明。
>在Objective-C中采用Automatic Reference Counting（ARC）机制，让编译器来进行内存管理。在新一代Apple LLVM编译器中设置ARC为有效状态，就无需再次键入retain或者release代码，这在降低程序崩溃、内存泄露等风险的同时，很大程度上减少了开发程序的工作量。编译器完全清楚目标对象，并能立刻释放那些不再被使用的对象。如此一来，应用程序将具有可预测性，且能流畅运行，速度也将大幅提升。
  
&#160; &#160; &#160; &#160;**"在新一代Apple LLVM编译器中设置ARC为有效状态，就无需再次键入retain或者release代码"**

### 满足条件：

 - 使用Xcode 4.2 或以上版本。
 - 使用LLVM编译器 3.0或以上版本。
 - 编译器选项设置ARC为有效。
 
&#160; &#160; &#160; &#160; 核心思想：当引用计数 = 0，自动释放对象。

### 内存管理的思考方式

 - 自己生成的对象，自己持有。
 - 非自己生成的对象，自己也能持有。
 - 不再需要自己持有的对象时释放。
 - 非自己持有的对象无法释放。

### 对象操作与Objective-C方法的对应

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>对象操作</td>
    <td>Objective-C方法</td>
    </tr>
    <tr>
        <td>生成并持有对象 </td>
    <td>alloc/new/copy/mutableCopy等方法</td>
    </tr>
     <tr>
        <td>持有对象</td>
    <td>retain方法</td>
    </tr>
     <tr>
        <td>释放对象</td>
    <td>release方法</td>
    </tr>
         <tr>
        <td>废弃对象</td>
    <td>dealloc方法</td>
    </tr>
</table>


