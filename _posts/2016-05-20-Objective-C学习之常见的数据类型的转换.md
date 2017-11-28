---
layout: post
title: Objective-C学习之常见的数据类型的转换
date: 2016-05-20
tag: Objective-C学习
---

**1、不可变字典转可变字典**

```
    NSDictionary * dict = [[NSDictionary alloc] init];
    NSMutableDictionary * mDict = [NSMutableDictionary dictionaryWithDictionary:dict]; 
```

**2、不可变数组转可变数组**

```
NSArry *array = [NSArray array];
NSMutableArray *mutableArray = [NSMutableArray arrayWithArray:array];
```

```
NSString *valueStr = @"112233";
```

**3、字符串转换成bool**
 

```
   BOOL boolValue = [valueStr boolValue];  
```

  
**4、字符串转换成整形**

```
    int intValue = [valueStr intValue];    
    NSInteger integer = [valueStr integerValue];
```

**5、字符串转换成单精度 双精度**

```
    float floatValue = [valueStr floatValue];
    double doubleValue = [valueStr doubleValue];
```

**6、其他数据转换为NSString**

```
    NSString *srtingOfValue = [NSString stringWithFormat:@" %d  %d  %ld  %f  %f",boolValue,intValue,integer,floatValue,doubleValue];
```
**7、从字典映射到一个对象**
这是KVC中的一个方法所提供的,这个方法就是 `setValuesForKeysWithDictionary`