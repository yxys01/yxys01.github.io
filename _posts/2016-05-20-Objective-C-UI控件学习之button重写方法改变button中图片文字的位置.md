---
layout: post
title: Objective-C-UI控件学习之button重写方法改变button中图片文字的位置
date: 2016-05-20
tag: Objective-C-UI控件学习
---
## button重写方法改变button中图片文字的位置
### 1.重写方法,改变图片的位置在`titleRect`方法后执行  

```
- (CGRect)imageRectForContentRect:(CGRect)contentRect  
{  
    CGFloat imageX=self.frame.size.width/2+boundingRect.size.width/2;  
    UIScreen *s=[UIScreen mainScreen];  
    CGRect rect=s.bounds;  
    CGFloat imageY=contentRect.origin.y+14;  
    CGFloat width=24;  
    CGFloat height=24;  
    return CGRectMake(imageX, imageY, width, height);        
}  
```

### 2.改变title文字的位置,构造title的矩形即可  

```
- (CGRect)titleRectForContentRect:(CGRect)contentRect  
{    
    CGFloat imageX=(self.frame.size.width-boundingRect.size.width)/2;  
    CGFloat imageY=contentRect.origin.y+10;  
    CGFloat width=220;  
    CGFloat height=25;  
    return CGRectMake(imageX, imageY, width, height);  
   
}  
```
