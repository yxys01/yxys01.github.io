---
layout: post
title: Objective-C内存管理学习之所有权修饰符
date: 2016-05-27
tag: Objective-C内存管理学习
---

&#160; &#160; &#160; &#160;Objective-C编程中为了处理对象，可将变量类型定义为id类型或各种对象类型。

&#160; &#160; &#160; &#160;所谓对象类型就是指向NSObject这样的Objective-C类的指针，例如`NSObject *`。id类型用于隐藏对象的类名部分，相当于C语言中常用的`void *`。

&#160; &#160; &#160; &#160;ARC有效时，id类型和对象类型同C语言其他类型不同，其类型上必须附加所有权修饰符。

&#160; &#160; &#160; &#160;所有权修饰符一共有**4种**：

 - `__strong`修饰符
 - `__weak`修饰符
 - `__unsafe_unretained`修饰符
 - `__autoreleasing`修饰符

### 一、`__strong修饰符`
&#160; &#160; &#160; &#160;`__strong`修饰符是id类型和对象类型默认的所有权修饰符。即代码中id变量，实际上被附加了所有权修饰符。

&#160; &#160; &#160; &#160;`__strong`修饰符表示对对象的“强引用”。持有强引用的变量在超出其作用域时被废弃，随着强引用的失效，引用的对象会随之释放。

&#160; &#160; &#160; &#160;注：附有`__strong`修饰符的变量之前可以相互赋值。

__strong修饰符、 __weak修饰符、 __autoreleasing修饰符一起可以保证将附有这些修饰符的自动变量初始化为nil。

### 二、`__weak修饰符`
&#160; &#160; &#160; &#160;注意：`__strong`修饰符的成员变量在持有对象时，很容易发生循环引用。

```
@interface Test ：NSObject
{
  id __strong obj1;
}
-(void)setObject:(id __strong)obj;
@end

@implementation Test
-(id)init
{
  self = [super init];
  return self;
}
-(void)setObject:(id __strong)obj
{
  obj1 = obj;
}
@end

//下面为循环引用(互相强引用)
{
   id test0 = [[Test alloc] init];//对象A
   //test0持有Test对象A的强引用
   id test1 = [[Test alloc] init];//对象B
   //test1持有Test对象B的强引用
   [test0 setObject:test1];
   //Test对象A的obj1成员变量持有Test对象B的强引用
   //此时，持有Test对象B的强引用的变量为：Test对象A的obj1 和test1.
   [test1 setObject:test0];
   //Test对象B的obj1成员变量持有Test对象A的强引用
   //此时，持有Test对象A的强引用的变量为：Test对象B的obj1 和test0.
}
/**
  因为test0变量超出其作用域，强引用失效，所以自动释放Test对象A。
  因为test1变量超出其作用域，强引用失效，所以自动释放Test对象B。
  此时，持有Test对象A的强引用的变量为 Test对象B的obj1.
  此时，持有Test对象B的强引用的变量为 Test对象A的obj1.
 
  发生内存泄露！！！！
*/
//(对自身的强引用)
{
  id test = [[Test alloc]init];
  [test setObject: test];
}
```
&#160; &#160; &#160; &#160;循环引用容易发生内存泄露。所谓内存泄露就是应当废弃的对象在超出其生存周期后继续存在。

&#160; &#160; &#160; &#160;`__weak修饰符`与`__strong`修饰符相反，提供弱引用。弱引用不能持有对象实例。

&#160; &#160; &#160; &#160;因为`__weak`修饰符的变量（即弱引用）不持有对象，所以在超出其变量作用域时，对象即被释放。即可以避免循环引用。

&#160; &#160; &#160; &#160;`__weak`修饰符还有一个优点。在持有某对象的弱引用时，若该对象被废弃，则此弱引用将自动失效且处于nil被赋值的状态（空弱引用）。如以下代码所示。

```objectivec
id __weak obj1 = nil；

{
  id __strong obj0 = [[NSObject alloc] init];//因为obj0变量为强引用，所以自己持有对象
  obj1 = obj0;//obj1变量持有对象的弱引用
  NSLog(@"A:%@",obj1);//输出obj1变量持有的弱引用的对象
}
/**
  因为obj0变量超出其作用域，强引用失效，所以自动释放自己持有的对象。
  因为对象无持有者，所以废弃该对象。
  废弃对象的同时，持有该对象弱引用的obj1变量的弱引用失效，nil赋值给obj1.
*/
NSLog(@"B:%@",obj1)；//输出赋值给obj1变量中的nil
```

&#160; &#160; &#160; &#160;此源码执行结果如下：

```
A:<NSObject: 0x753e180>
B:(null)
```

&#160; &#160; &#160; &#160;像这样，使用`__weak`修饰符可避免循环引用。通过检查附有`__weak`修饰符的变量是否为nil，可以判断被赋值的对象是否已废弃。

&#160; &#160; &#160; &#160;注意：`__weak`修饰符只能用于iOS5以上及OS X Lion以上版本的应用程序。在iOS4以及OS X Snow Leopard的应用程序中可使用`__unsafe_unretained`修饰符来代替。

### 三、`__unsafe_unretained`修饰符
&#160; &#160; &#160; &#160; `__unsafe_unretained`修饰符是不安全的所有权修饰符。尽管ARC式的内存管理是编译器的工作，但附有 `__unsafe_unretained`修饰符的变量不属于编译器的内存管理的对象，在使用时要注意。

&#160; &#160; &#160; &#160; 附有 `__unsafe_unretained`修饰符的变量同附有 `__weak`修饰符的变量一样，因为自己生成并持有的对象不能继续为自己所有，所以生成的对象会被立刻被释放。
 
```objectivec
id __unsafe_unretained obj1 = nil；

{
  id __strong obj0 = [[NSObject alloc] init];//因为obj0变量为强引用，所以自己持有对象
  obj1 = obj0;//虽然obj0变量赋值给obj1，但是obj1变量既不持有对象的强引用也不持有弱引用
  NSLog(@"A:%@",obj1);//输出obj1变量表示的对象
}
/**
  因为obj0变量超出其作用域，强引用失效，所以自动释放自己持有的对象。
  因为对象无持有者，所以废弃该对象。
*/
NSLog(@"B:%@",obj1)；//输出obj1变量表示的对象
//obj1变量表示的对象已经被废弃（悬垂指针）！错误访问！！
```

&#160; &#160; &#160; &#160; 此源码执行结果如下：

```
A:<NSObject: 0x753e180>
B:<NSObject: 0x753e180>
```
&#160; &#160; &#160; &#160; 也就是说，最后一行的NSLog只是碰巧正常运行而已，虽然访问了已经废弃的对象，但是应用程序在个别运行状况下才会崩溃。

&#160; &#160; &#160; &#160; 在使用`__unsafe_unretained`修饰符时，赋值给附有`__strong`修饰符的变量时有必要确保被赋值对象却是存在。

### 四、`__autoreleasing`修饰符

&#160; &#160; &#160; &#160; ARC有效时

&#160; &#160; &#160; &#160; 指定`@autoreleasepool`块来替代”`NSAutoreleasePool`类对象生成、持有以及废弃"这一范围。

&#160; &#160; &#160; &#160; 另外，ARC有效时，要通过将对象赋值给附加了`__autoreleasing`修饰符的变量来替代调用`autorelease`方法。对象赋值给附有`__autoreleasing`修饰符的变量等价于在ARC无效时调用对象的`autorelease`方法，即对象被注册到`autoreleasepool`。

&#160; &#160; &#160; &#160; 即在ARC有效时，用`@autoreleasepool`块替代`NSAutoreleasePool`类。用附有`__autoreleasing`修饰符的变量替代`autorelease`方法。

&#160; &#160; &#160; &#160; 下面两块代码等价

```
NSAutoreleasePool *pool= [[NSAutoreleasePool alloc] init];

[obj autorelease];

[pool drain];
```
&#160; &#160; &#160; &#160; 等价于

```
@autoreleasepool{
id __autoreleasing obj2;
obj2 = obj;
}
```
&#160; &#160; &#160; &#160; 但是，显示地附加`__autoreleasing`修饰符同显示地附加`__strong`修饰符一样罕见。

&#160; &#160; &#160; &#160; **作为`alloc/new/copy/mutableCopy`方法返回值取回的对象是自己生成并持有的，其他情况下便是取得非自己生成并持有的对象。**因此，使用附有`__autoreleasing`修饰符的变量作为对象取得参数，与除`alloc/new/copy/mutableCopy`外其他方法的返回值取得对象完全一样，都会注册到`autoreleasepool`，并取得非自己生成并持有的对象。

&#160; &#160; &#160; &#160; 另外，虽然可以非显示地指定`__autoreleasing`修饰符，但是显示地显示`__autoreleasing`修饰符时们必须注意对象要为自动变量（包括局部变量、函数以及方法参数）。
