---
layout: post
title: Objective-C内存管理学习之block
date: 2016-05-18
tag: Objective-C学习
---

### 简介
&#160; &#160; &#160; &#160;**Block**：带有自动变量（局部变量）的**匿名函数**

&#160; &#160; &#160; &#160;block是一种数据类型，封装代码

&#160; &#160; &#160; &#160; 函数不能在方法内部或函数内部，但是block可以

#### 定义block类型的变量的格式
```objectivec
 返回值类型 （^ block变量名称）(参数列表)；
```
#### 实现格式

&#160; &#160; &#160; &#160; **1. `^ 返回值类型（参数列表）{   语句......   }；`**
 
&#160; &#160; &#160; &#160;eg: 
```
^int(int count){
     return count +1;
}
```
&#160; &#160; &#160; &#160; **2. `^（参数列表）{   语句......   }；`**

&#160; &#160; &#160; &#160;eg: 
```
^(int count){
  return count +1;
}
```
&#160; &#160; &#160; &#160;注意：省略返回值类型时，如果表达式中有return语句就使用该返回值的类型，如果表达式中没有return语句就使用void类型。表达式中含有多个return语句时，所有return的返回值类型必须相同。

&#160; &#160; &#160; &#160; **3. `{   语句......   }；`**

&#160; &#160; &#160; &#160;eg: 
```
^void (void){
printf("Blocks\n");
}
```
&#160; &#160; &#160; &#160;可省略为：`^{printf("Blocks\n");}`


### 定义block类型的变量
&#160; &#160; &#160; &#160;**1、定义一个无参无返回值的block类型的变量**
```
void (^ block) = ^{
    NSLog(@"tesgBlock");
}
block();
```
&#160; &#160; &#160; &#160;**2、有参无返回值**
```
void (^block1)(NSString *name) = ^(NSString *name){
    NSLog@("%@",name);
};
block1(@"damu");
```
&#160; &#160; &#160; &#160;**3、有参有返回值**
```
int (^sum)(int num1,int num2)=^(int num1,int num2)
{
    return num1+num2;
}
int rs = sum(10,30);
NSLog(@"%d",rs);
```
&#160; &#160; &#160; &#160;**4、作为函数参数类型的格式**
```
返回值类型(^)(形参列表)
```
```
-(void)test:(void (^)() ) block; 
```
### 使用条件
&#160; &#160; &#160; &#160;当一些方法里面，有一部分代码是经常变化的，其他部分的代码基本没变，可以把这部分代码写到block里面。


&#160; &#160; &#160; &#160;在Block语法下，可将Block语法赋值给声明为Block类型的变量中。

&#160; &#160; &#160; &#160;声明Block类型变量的示例为：

```
 ^int (^blk)(int);
```
&#160; &#160; &#160; &#160; Block类型变量可用作：
&#160; &#160; &#160; &#160;**自动变量**
&#160; &#160; &#160; &#160;**函数参数**
&#160; &#160; &#160; &#160;**静态变量**
&#160; &#160; &#160; &#160;**静态全局变量**
&#160; &#160; &#160; &#160;**全局变量**


&#160; &#160; &#160; &#160;使用Block语法将Block赋值为Block类型变量。
```
int (^blk)(int) = ^(int count){return count  + 1;};
```
&#160; &#160; &#160; &#160;由"^"开始的Block语法生成的Block被赋值给变量blk中。因为与通常的变量相同，所以当然也可以由Block类型变量向Block类型变量赋值。
```
int (^blk1)(int) = blk;
int (^blk2)(int);
blk2 = blk1;
```
&#160; &#160; &#160; &#160;在函数参数中使用Block类型变量可以向函数传递Block。
```
void func(int (^blk)(int))
```
&#160; &#160; &#160; &#160;在函数返回值中指定Block类型，可以将Block作为函数的返回值返回。
```
int (^func())(int)
{
   return ^(int count){return count + 1;};
}
```
&#160; &#160; &#160; &#160;由此可知，在函数参数和返回值中使用Block类型变量时，记述方式极为复杂。这时，我们可以向使用函数指针类型时那样，使用typedef来解决该问题。
```
typedef int (^blk_t)(int);
```
&#160; &#160; &#160; &#160;通过使用typedef可声明"blk_t"类型变量

```
//原来的记述方式
//void func(int (^blk)(int))

void func(blk_t elk){}

//原来的记述方式
//int (^func() (int) )

blk_t func() {}
```

&#160; &#160; &#160; &#160;Block的“带有自动变量值”在Blocks中表现为“截获自动变量值”。实际上，自动变量截获只能保存执行Block语法瞬间的值。保存后就不能改写该值。

```
int val = 0;
void (^blk)(void) = ^{val = 1;};
blk();
printf("val = %d\n",val);
```
&#160; &#160; &#160; &#160;以上为在Block语法外声明的给自动变量赋值的源代码。该源代码会产生编译错误。

&#160; &#160; &#160; &#160;若想在Block语法的表达式中将值赋给在Block语法外声明的自动变量，需要在该自动变量上附加__block说明符。
```
__block int val = 0;
void (^blk)(void) = ^{val = 1;};
blk();
printf("val = %d\n",val);
```
&#160; &#160; &#160; &#160;该源码执行结果为
`val= 1`

### __block
&#160; &#160; &#160; &#160;使用附有__block说明符的自动变量可在Block中赋值，该变量称为__block变量。


#### 在截获Objective-C对象，调用变更该对象的方法也会产生编译错误吗？

```
id array = [[NSMutableArray alloc] init];
void (^blk)(void) = ^{
        id obj = [[NSObject alloc ] init];
        [array addObject:obj];
}
```
&#160; &#160; &#160; &#160;这是没有问题的，而向截获的变量array赋值则会产生编译错误。该源代码中截获的变量值为NSMutableArray类的对象。虽然赋值给截获的自动变量array的操作会产生编译错误，但使用截获的值却不会有任何问题。下面源代码向截获的自动变量进行赋值，因此会产生编译错误。
```
id array = [[NSMutableArray alloc] init];
void (^blk)(void) = ^{
        array = [[NSObject alloc ] init];
}
```
&#160; &#160; &#160; &#160;编译错误！

```
error: variable is not assignable (missing __block type specifier)
        array = [[NSObject alloc ] init];
        ~~~~~ ^
```

&#160; &#160; &#160; &#160;这种情况下，需要给截获的自动变量附加`__block`说明符
```
__block  id array = [[NSMutableArray alloc] init];
void (^blk)(void) = ^{
        array = [[NSObject alloc ] init];
}
```

&#160; &#160; &#160; &#160;将Block当做Objective-C对象来看时，该Block的类为_NSConcreteStackBlock.

```
类                                     设置对象的存储域
_NSConcreteStackBlock                  栈
_NSConcreteGlobalBlock                 程序的数据区域（.data区）
_NSConcreteMallocBlock                 堆
```

&#160; &#160; &#160; &#160;Block从栈赋值到堆时对__block变量产生的影响

```
__block变量的配置存储域                     Block从栈赋值到堆时的影响
栈                                        从栈复制到堆并被Block持有
堆                                        被Block持有
```