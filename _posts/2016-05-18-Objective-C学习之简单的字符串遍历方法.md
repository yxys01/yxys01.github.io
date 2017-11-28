---
layout: post
title: Objective-C学习之简单的字符串遍历方法
date: 2016-05-18
tag: Objective-C学习
---

### 字符串遍历

```
- (void)viewDidLoad
{
    [super viewDidLoad];
    
    //经典的字符串赋值
    NSString *str = @"YUSONGMOMO";
    
    //字符串的长度
    int count = [str length];
    
    NSLog(@"字符串的长度是%d",count);
    
    //遍历字符串中的每一个字符
    for(int i =0; i < count; i++)
    {
        char c = [str characterAtIndex:i];
        NSLog(@"字符串第 %d 位为 %c",i,c);
    }
    
}
```