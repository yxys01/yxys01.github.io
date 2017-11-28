---
layout: post
title: Objective-C动画学习之视图跳转方式
date: 2016-05-24
tag: Objective-C弹出模态学习
---
## 视图跳转方式：(push pop)

```
[self.navigationController pushViewController:(nonnull UIViewController *)animated:(BOOL)];
popToRootViewControllerAnimated:(BOOL)
popToViewController:(nonnull UIViewController *)#animated:(BOOL)
popViewControllerAnimated:(BOOL)
```
### push和pop区别与联系

 1. 只有push 才会执行 viewDidLoad 等等，pop是不会执行的。
 2. push与present都可以推出新的界面。
 3. present与dismiss对应，push和pop对应。
 4. present只能逐级返回，push所有视图由视图栈控制，可以返回上一级，也可以返回到根vc，其他vc。
 5. present一般用于不同业务界面的切换，push一般用于同一业务不同界面之间的切换。
 6. push就是压栈,pop就是出栈!