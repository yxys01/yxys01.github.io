---
layout: post
title: Objective-C学习之NSString
date: 2016-05-20
tag: Objective-C学习
---

### NSString常用创建初始化方法

```
NSString *string0 = @"string";

NSString *string1 = [NSString stringWithFormat:@"it is %@",@"string"];

char *c = "string";

NSString *string2 = [[NSString alloc] initWithCString:c encoding:nil];

const char *utf8 = "utf";

NSString *string3 = [NSString  stringWithUTF8String:utf8];
```

### 数据转换

```
NSString *valueStr = @"112233";
```

**1、字符串转换成bool**

```
    BOOL boolValue = [valueStr boolValue];    
```

**2、字符串转换成整形**

```
    int intValue = [valueStr intValue];    
    NSInteger integer = [valueStr integerValue];
```

**3、字符串转换成单精度 双精度**

```
    float floatValue = [valueStr floatValue];
    double doubleValue = [valueStr doubleValue];
```

**4、其他数据转换为NSString**

```
    NSString *srtingOfValue = [NSString stringWithFormat:@" %d  %d  %ld  %f  %f",boolValue,intValue,integer,floatValue,doubleValue];
```

### 其他方法
**1、获取字符串长度**

```
    NSUInteger length = [string0 length];
```

**2、获取索引下标的字符**

```
    unichar index_char = [string0 characterAtIndex:3];
```

**3、截取字符串，从索引位置到结尾**

```
    NSString *str1 = [string0 substringFromIndex:3];
```

**4、截取字符串，从开始位置到索引位置**

```
    NSString *str2 = [string0 substringToIndex:3];
```

**5、截取字符串，从索引开始，取长度个数组成字符串**

```
    NSRange range = NSMakeRange(1, 3);
    NSString *str3 = [string0 substringWithRange:range];
```

**6、获取字符串在某个字符串中的索引位置和长度**

```
    NSRange range1 = [string0 rangeOfString:@"ing"];
```

### 字符串判断操作

**1、判断字符串是否为空**

   `string0 == nil` 和 `string0.length == 0` 同时成立。
   
**2、判断字符串是否以……开头**
```
    [string0 hasPrefix:@"ing"]
```
**3、判断字符串是否以……结尾**
```
    [string0 hasSuffix:@"ing"]
```
**4、判断两个字符串是否相等**
```
   [string0 isEqualToString:string1]
```

### 字符串转换
**1、将字符串中的字母转换为大写**
```
    [string0 uppercaseString]    
```
**2、将字符串中的字母转换为小写**
```
    [string0 lowercaseString]   
```
**3、将字符串中的首字母变为大写**
```
    string0 capitalizedString]
```

### 字符串操作

**1、拼接字符串**
```
    NSString *string0 = [NSString stringWithFormat:@"%@%@%@",@"aaa",@"bbb",@"ccc"];
```

**2、在字符串的末尾追加新的字符串**

```
    NSString *string1 = [string0 stringByAppendingString:@"xxx"];
```

**3、在制定的范围插入字符串**

```
    NSString *insertStr = @"真好玩";
    NSRange range = {4,0};//location代表从哪个索引开始插入,length代表将覆盖多少个字符
    NSString * string2 = [string0 stringByReplacingCharactersInRange:range withString:insertStr];
```

**4、使用新的字符,替换原有的字符 （可以当删除使用）**

```
    NSString *updateStr = @"我想吃饭";
    NSString *string3 = [updateStr stringByReplacingOccurrencesOfString:@"我" withString:@"你"];
```

