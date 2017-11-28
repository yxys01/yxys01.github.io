---
layout: post
title: Objective-C学习之图片相关（ImageIO）
date: 2016-05-25
tag: Objective-C学习
---
```objectivec
#import <ImageIO/ ImageIo.h>
//创建图像源
CGImageSourceRef source = CGImageSourceCreateWithData((__bridge CFDataRef)data,NULL);
//获取图片的帧数
size_t count =CGImageSourceGetCount(source)
```

###图片格式：
**PNG**：无损压缩；压缩没有JPG高；一般PNG图片会比JPG大。比较清晰，苹果推荐使用，GPU解压缩的效果非常小；解压缩速度比较快
**JPG**：有损压缩；压缩非常高；照相机使用；GPU解压缩的消耗比较大
**GIF**：可动画的图片