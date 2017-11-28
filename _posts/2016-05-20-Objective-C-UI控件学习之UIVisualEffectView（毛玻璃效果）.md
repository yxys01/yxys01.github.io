---
layout: post
title: Objective-C-UI控件学习之UIVisualEffectView（毛玻璃效果）
date: 2016-05-20
tag: Objective-C-UI控件学习
---

### 毛玻璃效果最新方法

```
    UIVisualEffectView *visualEffect = [[UIVisualEffectView alloc]initWithEffect:[UIBlurEffect effectWithStyle:UIBlurEffectStyleExtraLight]];

    visualEffect.frame = CGRectMake(20, 90, 280, 300);

    visualEffect.alpha = 0.9;

    [self.view addSubview:visualEffect];
```