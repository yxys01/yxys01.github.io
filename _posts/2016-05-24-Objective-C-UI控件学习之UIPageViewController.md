---
layout: post
title: Objective-C-UI控件学习之UIPageViewController
date: 2016-05-24
tag: Objective-C-UI控件学习
---

### 方法
```
initWithTransitionStyle:navigationOrientation:options:
```
&#160; &#160; &#160; &#160;构造方法用于创建UIPageViewController实例，initWithTransitionStyle用于设定页面翻转的样式。

### 翻转样式

&#160; &#160; &#160; &#160;UIPageViewControllerTransitionStyle枚举类型定义了如下两个翻转样式。
 

 1. UIPageViewControllerTransitionStylePageCurl：翻书效果样式。
 
 2. UIPageViewControllerTransitionStyleScroll：滑屏效果样式。

### 翻页方向
 
&#160; &#160; &#160; &#160;navigationOrientation设定了翻页方向，UIPageViewControllerNavigationDirection枚举类型定义了以下两种翻页方式。
 
 3. UIPageViewControllerNavigationDirectionForward：从左往右（或从下往上）；
 
 4. UIPageViewControllerNavigationDirectionReverse：从右向左（或从上往下）。

&#160; &#160; &#160; &#160;在UIPageViewController中，`setViewControllers:direction:animated:completion:`方法用于设定显示的视图。
```
- (void)pageViewController:(UIPageViewController *)pageViewController didFinishAnimating:(BOOL)finished
previousViewControllers:(NSArray *)previousViewControllers transitionCompleted:(BOOL)completed;
```

&#160; &#160; &#160; &#160;当用户从一个页面转向下一个或者前一个页面,或者当用户开始从一个页面转向另一个页面的途中后悔 了,并撤销返回到了之前的页面时,将会调用这个方法。假如成功跳转到另一个页面时,transitionCompleted 会被置成 YES,假如在跳转途中取消了跳转这个动作将会被置成 NO。

```
#pragma mark - UIPageViewControllerDataSource
/**返回上一个ViewController对象
   返回的ViewController，将被添加到相应的UIPageViewController对象上。
   UIPageViewController对象会根据UIPageViewControllerDataSource协议方法，自动来维护次序。
   不用我们去操心每个ViewController的顺序问题。*/
- (UIViewController *)pageViewController:(UIPageViewController *)pageViewController viewControllerBeforeViewController:(UIViewController *)viewController
{
    NSUInteger index = [self.pages indexOfObject:viewController];
    
    if ((index == NSNotFound) || (index == 0)) {
        return nil;
    }
    
    return self.pages[--index];
}
// 返回下一个ViewController对象
- (UIViewController *)pageViewController:(UIPageViewController *)pageViewController viewControllerAfterViewController:(UIViewController *)viewController
{
    NSUInteger index = [self.pages indexOfObject:viewController];
    
    if ((index == NSNotFound)||(index+1 >= [self.pages count])) {
        return nil;
    }
    
    return self.pages[++index];
}
```