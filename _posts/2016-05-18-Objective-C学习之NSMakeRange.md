---
layout: post
title: Objective-C学习之NSMakeRange
date: 2016-05-18
tag: Objective-C学习
---

### 简介

```
NSMakeRange(loc,len) 
```

&#160; &#160; &#160; &#160;NSMakeRange是一个结构体类型，包含两个参数，位置和长度。表示字符串要传进来从哪里开始的位置和需要的长度。
### 使用
```
NSString *str = @"1234567890";  
  
 [str stringByReplacingCharactersInRange:NSMakeRange(str.length-1, 1) withString:@""];  
  
NSLog(@"str = %@",  str);  // str = 123456789
```

&#160; &#160; &#160; &#160;解释：`NSMakeRange(str.length-1, 1)`,将字符串str定位到第九个字符即`9`，取长度为1的字符串，即9后第一个字符串 `0`，用字符串`@""`替代`0`，即所得的结果为“123456789”
