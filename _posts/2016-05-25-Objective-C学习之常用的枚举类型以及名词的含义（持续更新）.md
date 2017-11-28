---
layout: post
title: Objective-C学习之常用的枚举类型以及名词的含义（持续更新）
date: 2016-05-25
tag: Objective-C学习
---

### 常见名词：

 1. **Tap**：点击
 2. **Pinch**：捏合
 3. **Rotation**：旋转
 4. **Swipe**：滑动，快速移动，是用于监测滑动的方向的
 5. **Pan**：拖移，慢速移动，是用于监测偏移的量的
 6. **LongPress**：长按
 7. **CGFloat**：浮点值的基本类型
 8. **CGPoint**：表示一个二维坐标系中的点
 9. **CGSize**：表示一个矩形的宽度和高度
 10. **CGRect**：表示一个矩形的位置和大小
 11.  **URL**的基本格式 = 协议://主机地址/路径
eg:`http://202.108.22.5/img/bdlogo.gif`
协议：不同的协议，代表着不同的资源查找方式、资源传输方式
主机地址：存放资源的主机的IP地址（域名）
路径：资源在主机中的具体位置
 12. **animationWithKeyPath**的值
 
 <table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>transform.scale</td>
    <td>比例转换</td>
    </tr>
    <tr>
        <td>transform.scale.x</td>
    <td>宽的比例转换</td>
    </tr>
     <tr>
        <td>transform.scale.y</td>
    <td>高的比例转换</td>
    </tr>
     <tr>
        <td>transform.rotation.z</td>
    <td>平面圆的旋转</td>
    </tr>
         <tr>
        <td>opacity </td>
    <td>透明度</td>
    </tr>
     <tr>
        <td>position </td>
    <td>点位移</td>
    </tr>
</table>


### 常见枚举类型

 1. **UITableViewCell.h**
 typedef NS_ENUM(NSInteger, UITableViewCellAccessoryType) {
    UITableViewCellAccessoryNone,  // cell没有任何的样式
    UITableViewCellAccessoryDisclosureIndicator, //cell的右边有一个小箭头，距离右边有十几像素；
    UITableViewCellAccessoryDetailDisclosureButton，//cell右边有一个蓝色的圆形button；
    UITableViewCellAccessoryCheckmark, //cell右边的形状是对号
};
 2. **UITableView.h** 
        typedef NS_ENUM(NSInteger, UITableViewRowAnimation) {
        UITableViewRowAnimationFade,//淡入淡出
        UITableViewRowAnimationRight,//从右滑入
        UITableViewRowAnimationLeft,//从左滑入
        UITableViewRowAnimationTop,//从上滑入
        UITableViewRowAnimationBottom,//从下滑入
        UITableViewRowAnimationNone,  //没有动画
        UITableViewRowAnimationMiddle,          
        UITableViewRowAnimationAutomatic = 100  // 自动选择合适的动画 };
        
 3. **UIButton.h** 
        typedef enum {
          UIButtonTypeCustom = 0,          自定义风格
          UIButtonTypeRoundedRect,         圆角矩形
          UIButtonTypeDetailDisclosure,    蓝色小箭头按钮，主要做详细说明用
          UIButtonTypeInfoLight,           亮色感叹号
          UIButtonTypeInfoDark,            暗色感叹号
          UIButtonTypeContactAdd,          十字加号按钮    } UIButtonType;
 4. **UIControl.h**        
       typedef NS_OPTIONS(NSUInteger, UIControlState)  {
            UIControlStateNormal       = 0,         常规状态显现
            UIControlStateHighlighted  = 1 << 0,    高亮状态显现
            UIControlStateDisabled     = 1 << 1,    禁用的状态才会显现
            UIControlStateSelected     = 1 << 2,    选中状态
            UIControlStateApplication  = 0x00FF0000, 当应用程序标志时
            UIControlStateReserved     = 0xFF000000  为内部框架预留，可以不管他
        };
 5. **UIGestureRecognizer.h**
typedef enum {  
    UIGestureRecognizerStatePossible,   //识别器在未识别出它的手势，但可能会接收到触摸时处于这个状态。这是默认状态。
    UIGestureRecognizerStateBegan,   //识别器接收到触摸并识别出是它的手势时处于这个状态。响应方法将在下个循环步骤中被调用。    UIGestureRecognizerStateChanged,  // the recognizer has received touches recognized as a change to the gesture. （不懂怎么翻译，理解上就是识别器识别出一个变化为它的手势的触摸），响应方法将在下个循环步骤中被调用。
    UIGestureRecognizerStateEnded,   //识别器在识别到作为当前手势结束信号的触摸时处于这个状态。响应方法将在下个循环步骤中被调用并且识别器将重置为possible状态。
    UIGestureRecognizerStateCancelled,  //识别器处于取消状态。响应方法将在下个循环步骤中被调用并且识别器将重置为possible状态。
    UIGestureRecognizerStateFailed,    //识别器接收到不能识别为它的手势的一系列触摸。响应方法不会被调用并且识别器将重置为possible状态。
    UIGestureRecognizerStateRecognized = UIGestureRecognizerStateEnded   //识别器已识别到它的手势。响应方法将在下个循环步骤中被调用并且识别器将重置为possible状态。
} UIGestureRecognizerState;  
 6. **NSLayoutConstraint.h**
   typedef NS_ENUM(NSInteger, NSLayoutAttribute) {
NSLayoutAttributeLeft,  //视图的左边
NSLayoutAttributeRight, //视图的右边
NSLayoutAttributeTop,  //   视图的上边
NSLayoutAttributeBottom,  //    视图的下边
NSLayoutAttributeLeading, //    视图的前边
NSLayoutAttributeTrailing,//    视图的后边
NSLayoutAttributeWidth,//   视图的宽度
NSLayoutAttributeHeight,//  视图的高度
NSLayoutAttributeCenterX,// 视图的中点的X值
NSLayoutAttributeCenterY,   //视图中点的Y值
NSLayoutAttributeBaseline   , //视图的基准线
NSLayoutAttributeNotAnAttribute//   无属性
};
 7. **ABAddressBook.h**
   //函数可以查询对通讯录的访问权限
    typedef CF_ENUM(CFIndex, ABAuthorizationStatus) {
    kABAuthorizationStatusNotDetermined = 0,    // 用户还没有决定是否授权你的程序进行访问
    kABAuthorizationStatusRestricted,           // iOS设备上的家长控制或其它一些许可配置阻止程序与通讯录数据库进行交互
    kABAuthorizationStatusDenied,               // 用户明确的拒绝了你的程序对通讯录的访问
    kABAuthorizationStatusAuthorized            // 用户已经授权给你的程序对通讯录进行访问
} AB_DEPRECATED("use CNAuthorizationStatus");
 8. **UIView.h**
     typedef NS_OPTIONS(NSUInteger, UIViewAutoresizing) {
UIViewAutoresizingNone,//不会随父视图的改变而改变
UIViewAutoresizingFlexibleLeftMargin,//自动调整view与父视图左边距，以保证右边距不变
UIViewAutoresizingFlexibleWidth,//自动调整view的宽度，保证左边距和右边距不变
UIViewAutoresizingFlexibleRightMargin,//自动调整view与父视图右边距，以保证左边距不变
UIViewAutoresizingFlexibleTopMargin,//自动调整view与父视图上边距，以保证下边距不变
UIViewAutoresizingFlexibleHeight,//自动调整view的高度，以保证上边距和下边距不变
UIViewAutoresizingFlexibleBottomMargin//自动调整view与父视图的下边距，以保证上边距不变
};
 9. **UIWebView.h**
     typedef NS_ENUM(NSInteger, UIWebViewNavigationType) {
    UIWebViewNavigationTypeLinkClicked，//用户触击了一个链接。
UIWebViewNavigationTypeFormSubmitted，//用户提交了一个表单。
UIWebViewNavigationTypeBackForward，//用户触击前进或返回按钮。
UIWebViewNavigationTypeReload，//用户触击重新加载的按钮。
UIWebViewNavigationTypeFormResubmitted，//用户重复提交表单
UIWebViewNavigationTypeOther，//发生其它行为。
} __TVOS_PROHIBITED;

