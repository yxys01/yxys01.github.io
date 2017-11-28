---
layout: post
title: Objective-C-UI控件学习之UIScreenEdgePanGestureRecognizer
date: 2016-05-26
tag: Objective-C-UI控件学习
---
### 简介
**UIScreenEdgePanGestureRecognizer**名字很长，而且关于其文档也是少的的可怜，苹果官方给的唯一的一个属性是**edges**，文档中的解释是这样的: 
>A UIScreenEdgePanGestureRecognizer looks for panning (dragging) gestures that start near an edge of the screen. The system uses screen edge gestures in some cases to initiate view controller transitions. You can use this class to replicate the same gesture behavior for your own actions.

&#160; &#160; &#160; &#160;大概的意思就是**UIScreenEdgePanGestureRecognizer**跟**pan**(平移)手势差不多，需要从边缘进行拖动，在控制器转换的时候是有用的，看文档的话我们会发现 **UIScreenEdgePanGestureRecognizer**是 **UIPanGestureRecognizer**的子类，理解会更方便一点。
### 例子讲解
&#160; &#160; &#160; &#160;例子：（可从[InteractiveViewControllerTransitions](https://github.com/PeteC/InteractiveViewControllerTransitions)中得到）

&#160; &#160; &#160; &#160;例子原文是讲iOS7交互式过渡的：http://www.cocoachina.com/industry/20140623/8918.html

&#160; &#160; &#160; &#160;这里我截取其中关于UIScreenEdgePanGestureRecognizer的内容来学习UIScreenEdgePanGestureRecognizer
```
- (void)viewDidLoad { 
    [super viewDidLoad]; 
    
    ...
//在用户手指从屏幕左边边缘划入时产生互动
    UIScreenEdgePanGestureRecognizer *popRecognizer = [[UIScreenEdgePanGestureRecognizer alloc] initWithTarget:self action:@selector(handlePopRecognizer:)];
    popRecognizer.edges = UIRectEdgeLeft;
    [self.view addGestureRecognizer:popRecognizer];
    }
```
&#160; &#160; &#160; &#160;现在我们可以识别该手势了，我们用它来设置并更新一个 iOS 7 新加入的类的对象。 UIPercentDrivenInteractiveTransition。这个类的对象会根据我们的手势，来决定我们的自定义过渡的完成度。我们把这些都放到手势识别器的 action 方法中去，具体就是：
 
&#160; &#160; &#160; &#160;当手势刚刚开始，我们创建一个 UIPercentDrivenInteractiveTransition 对象，然后让 navigationController 去把当前这个 viewController 弹出。
 
&#160; &#160; &#160; &#160;当手慢慢划入时，我们把总体手势划入的进度告诉 UIPercentDrivenInteractiveTransition 对象。
 
&#160; &#160; &#160; &#160;当手势结束，我们根据用户的手势进度来判断过渡是应该完成还是取消并相应的调用 finishInteractiveTransition 或者 cancelInteractiveTransition 方法.
```
#pragma mark UIGestureRecognizer handlers

- (void)handlePopRecognizer:(UIScreenEdgePanGestureRecognizer*)recognizer {
    // 计算用户手指划了多远
    CGFloat progress = [recognizer translationInView:self.view].x / (self.view.bounds.size.width * 1.0);
    progress = MIN(1.0, MAX(0.0, progress));

    if (recognizer.state == UIGestureRecognizerStateBegan) {
        // Create a interactive transition and pop the view controller
        // 创建过渡对象，弹出viewController
        self.interactivePopTransition = [[UIPercentDrivenInteractiveTransition alloc] init];
        [self.navigationController popViewControllerAnimated:YES];
    }
    else if (recognizer.state == UIGestureRecognizerStateChanged) {
        // Update the interactive transition's progress
        // 更新 interactive transition 的进度
        [self.interactivePopTransition updateInteractiveTransition:progress];
    }
    else if (recognizer.state == UIGestureRecognizerStateEnded || recognizer.state == UIGestureRecognizerStateCancelled) {
        // Finish or cancel the interactive transition
        // 完成或者取消过渡
        if (progress > 0.5) {
            [self.interactivePopTransition finishInteractiveTransition];
        }
        else {
            [self.interactivePopTransition cancelInteractiveTransition];
        }

        self.interactivePopTransition = nil;
    }

}
```
&#160; &#160; &#160; &#160;现在我们可以创建并更新 UIPercentDrivenInteractiveTransition 对象了，我们需要告诉 navigationController 去用它。为此，我们需要实现另一个 UInavigationControllerDelegate 的方法。

```
- (id<UIViewControllerInteractiveTransitioning>)navigationController:(UINavigationController *)navigationController 
                         interactionControllerForAnimationController:(id<UIViewControllerAnimatedTransitioning>)animationController { 
    // 检查是否是我们的自定义过渡 
    if ([animationController isKindOfClass:[DSLTransitionFromSecondToFirst class]]) { 
        return self.interactivePopTransition; 
    } 
    else { 
        return nil; 
    } 
} 
```