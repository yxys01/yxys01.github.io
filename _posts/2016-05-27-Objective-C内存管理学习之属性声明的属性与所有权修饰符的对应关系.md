---
layout: post
title: Objective-C内存管理学习之属性声明的属性与所有权修饰符的对应关系
date: 2016-05-27
tag: Objective-C内存管理学习
---

&#160; &#160; &#160; &#160;ARC有效时，Objective-C类的属性也会发生变化、

```
@property（nonatomic，strong）NSString *name；
```
&#160; &#160; &#160; &#160;属性声明的属性与所有权修饰符的对应关系

```
属性声明的属性                          所有权修饰符
assign                                __unsafe_unretained修饰符
copy                                  __strong修饰符(但是赋值的是被复制的对象)
retain                                __strong修饰符
strong                                __strong修饰符
unsafe_unretained                     __unsafe_unretained修饰符
weak                                  __weak修饰符
```

&#160; &#160; &#160; &#160;注意：在声明类成员变量时，如果同属性声明中的属性不一致则会引起编译错误。
&#160; &#160; &#160; &#160;eg：

```
@property（nonatomic，weak）id obj；
```

&#160; &#160; &#160; &#160;编译器会出现错误。
&#160; &#160; &#160; &#160;此时，成员变量的声明中需要附加__weak修饰符

```
@property（nonatomic，weak）id __weak obj；
```

&#160; &#160; &#160; &#160;或使用strong属性代替weak属性

```
@property（nonatomic，strong）id obj；
```


