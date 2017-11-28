---
layout: post
title: Objective-C-UI控件学习之UIButton详解
date: 2016-05-19
tag: Objective-C-UI控件学习
---

## UIButton详解：
### 一、UIButton的定义
&#160; &#160; &#160; &#160;两种创建方法
&#160; &#160; &#160; &#160;**（1）常规的initWithFrame的方式** 

```
UIButton *btn1 = [[UIButton alloc]initWithFrame:CGRectMake(100, 50, 100, 75)];
[btn1 setTitle:@"close" forState:UIControlStateNormal];
btn1.backgroundColor = [UIColor greenColor];//button的背景颜色
[btn1 setBackgroundImage:[UIImage imageNamed:@"1.png"] forState:UIControlStateNormal];//button的背景图片
```



&#160; &#160; &#160; &#160;**（2）UIButton 的一个类方法（也可以说是静态方法）buttonWithType** 

```
UIButton *btn2 = [UIButton buttonWithType:UIButtonTypeRoundedRect];//创建一个圆角矩形的按钮
btn2.frame = CGRectMake(200, 20, 50, 60);
btn2.backgroundColor = [UIColor blackColor];
[btn2 setTitle:@"clicke" forState:UIControlStateNormal];
[self.window addSubview:btn1];
[self.window addSubview:btn2];
```
&#160; &#160; &#160; &#160;**创建一个自定义的按钮**

```
   UIButton *button1=[UIButton buttonWithType:UIButtonTypeCustom];

```

&#160; &#160; &#160; &#160;**能够定义的button类型有以下6种，**

```
  typedef enum {
       UIButtonTypeCustom = 0,          自定义风格
       UIButtonTypeRoundedRect,         圆角矩形
       UIButtonTypeDetailDisclosure,    蓝色小箭头按钮，主要做详细说明用
       UIButtonTypeInfoLight,           亮色感叹号
       UIButtonTypeInfoDark,            暗色感叹号
       UIButtonTypeContactAdd,          十字加号按钮
     } UIButtonType;
```

   
### 二、设置frame

```
    //给定button在view上的位置
    button1.frame = CGRectMake(20, 20, 280, 20);
    [button setFrame:CGRectMake(20,20,50,50)];
```
### 三、button背景色
```
    //button背景色
    button1.backgroundColor = [UIColor clearColor];
    
    [button setBackgroundColor:[UIColor blueColor]];
```
### 四、设置button填充图片和背景图片

```
    //设置button填充图片和背景图片
    [button1 setImage:[UIImage imageNamed:@"btng.png"] forState:UIControlStateNormal];
    
    [button setBackgroundImage:[UIImageimageNamed:@"btng.png"]forState:UIControlStateNormal];
```
### 五、设置button标题和标题颜色

```
    //设置button标题和标题颜色
    [button1 setTitle:@"点击" forState:UIControlStateNormal];
    
    [button setTitleColor:[UIColorredColor]forState:UIControlStateNormal];

    [button setTitleShadowColor:[UIColor grayColor] forState:UIControlStateNormal ]; //阴影
```

### 六、state状态
&#160; &#160; &#160; &#160;`forState:` 这个参数的作用是定义按钮的文字或图片在何种状态下才会显现

&#160; &#160; &#160; &#160;以下是几种状态
```
    enum {
        UIControlStateNormal       = 0,         常规状态显现             
        UIControlStateHighlighted  = 1 << 0,    高亮状态显现   
        UIControlStateDisabled     = 1 << 1,    禁用的状态才会显现
        UIControlStateSelected     = 1 << 2,    选中状态             
        UIControlStateApplication  = 0x00FF0000, 当应用程序标志时           
        UIControlStateReserved     = 0xFF000000  为内部框架预留，可以不管他            
    };                     
```

```
    @property(nonatomic,getter=isEnabled)BOOL enabled; // default is YES. if NO, ignores touch events and subclasses may draw differently

    @property(nonatomic,getter=isSelected)BOOL selected;  // default is NO may be used by some subclasses or by application

    @property(nonatomic,getter=isHighlighted)BOOL highlighted;     
```
### 七、设置按钮按下是否颜色变深
```
   /*
     * 默认情况下，当按钮高亮的情况下，图像的颜色会被画深一点，如果这下面的这个属性设置为no，
     * 那么可以去掉这个功能
    */
    button1.adjustsImageWhenHighlighted = NO;
```

```
   /*跟上面的情况一样，默认情况下，当按钮禁用的时候，图像会被画得深一点，设置NO可以取消设置*/
    button1.adjustsImageWhenDisabled = NO;
```
### 八、设置按钮按下会发光
```
   /* 下面的这个属性设置为yes的状态下，按钮按下会发光*/
    button1.showsTouchWhenHighlighted = YES;

```

### 九、添加或删除事件处理

```
   /* 给button添加事件，事件有很多种
     按下按钮，并且手指离开屏幕的时候触发这个事件，跟web中的click事件一样。
     触发了这个事件以后，执行butClick:这个方法，addTarget:self 的意思是说，这个方法在本类中
     也可以传入其他类的指针*/
    //添加事件
    [button1 addTarget:self action:@selector(butClick:) forControlEvents:UIControlEventTouchUpInside];
    //删除事件
    [button1 removeTarget:nil action:nil forControlEvents:UIControlEventTouchUpInside];

    //显示控件
    [self.view addSubview:button1];

```
### 十、设置按钮内部图片间距和标题间距
```
UIEdgeInsets insets; // 设置按钮内部图片间距
insets.top = insets.bottom = insets.right = insets.left = 10;
bt.contentEdgeInsets = insets;
bt.titleEdgeInsets = insets; // 标题间距
```
### 十一、一些其他的按钮设置

```
btn1.titleLabel.font = [UIFont fontWithName：@“test” size:18];//设置按钮字体大小

[btn1 setTag:101] ;//设置tag值

btn1.layer.cornerRadius = 4.5;//设置圆角——四个圆角半径 
btn1.layer.borderWidth = 0.5;// 按钮边框宽度   
               
CGColorSpaceRef colorSpace = CGColorSpaceCreateDeviceRGB();                                                   // 设置颜色空间为rgb，用于生成ColorRef

CGColorRef borderColorRef = CGColorCreate(colorSpace,(CGFloat[]){ 0, 0, 0, 1 });                        // 新建一个红色的ColorRef，用于设置边框（四个数字分别是 r, g, b, alpha）

btn1.layer.borderColor = borderColorRef;                                                                                        // 设置边框颜色
```
### 十二、重写绘制行为

&#160; &#160; &#160; &#160;你可以通过子类化按钮来定制属于你自己的按钮类。在子类化的时候你可以重载下面这些方法，这些方法返回CGRect结构，指明了按钮每一组成部分的边界。

&#160; &#160; &#160; &#160;注意：不要直接调用这些方法， 这些方法是你写给系统调用的。
```
backgroundRectForBounds   //指定背景边界 
contentRectForBounds         // 指定内容边界 
titleRectForContentRect       // 指定文字标题边界  
imageRectForContentRect   //指定按钮图像边界 
```

 
&#160; &#160; &#160; &#160;例：

```
- (CGRect)imageRectForContentRect:(CGRect)bounds
{ 
     return CGRectMake(0.0, 0.0, 44, 44); 
} 
 
[btn1 addTarget:self action:@selector(btnPressed:) forControlEvents:UIControlEventTouchUpInside];//添加点击按钮事件
 
-(void)btnPressed:(id)sender
{  
      UIButton* btn = (UIButton*)sender;  
      //开始写你自己的动作 
}
```

```
forControlEvents参数类型
 typedef NS_OPTIONS(NSUInteger, UIControlEvents) 
{
    UIControlEventTouchDown                 = 1 <<  0,      // 单点触摸按下事件：用户点触屏幕，或者又有新手指落下的时候。
    UIControlEventTouchDownRepeat      = 1 <<  1,      // 多点触摸按下事件，点触计数大于1：用户按下第二、三、或第四根手指的时候。
    UIControlEventTouchDragInside         = 1 <<  2,      // 当一次触摸在控件窗口内拖动时。
    UIControlEventTouchDragOutside       = 1 <<  3,      // 当一次触摸在控件窗口之外拖动时。
    UIControlEventTouchDragEnter           = 1 <<  4,      // 当一次触摸从控件窗口之外拖动到内部时
    UIControlEventTouchDragExit             = 1 <<  5,      // 当一次触摸从控件窗口内部拖动到外部时。
    UIControlEventTouchUpInside            = 1 <<  6,      // 所有在控件之内触摸抬起事件
    UIControlEventTouchUpOutside          = 1 <<  7,      // 所有在控件之外触摸抬起事件(点触必须开始与控件内部才会发送通知)。
    UIControlEventTouchCancel                = 1 <<  8,      //所有触摸取消事件，即一次触摸因为放上了太多手指而被取消，或者被上锁或者电话呼叫打断。

    UIControlEventValueChanged             = 1 << 12,     // 当控件的值发生改变时，发送通知。用于滑块、分段控件、以及其他取值的控件。你可以配置滑块控件何时发送通知，在滑块被放下时发送，或者在被拖动时发送。

    UIControlEventEditingDidBegin           = 1 << 16,     // 当文本控件中开始编辑时发送通知
    UIControlEventEditingChanged           = 1 << 17,     // 当文本控件中的文本被改变时发送通知。
    UIControlEventEditingDidEnd              = 1 << 18,     // 当文本控件中编辑结束时发送通知。
    UIControlEventEditingDidEndOnExit    = 1 << 19,     // 当文本控件内通过按下回车键（或等价行为）结束编辑时，发送通知。

    UIControlEventAllTouchEvents             = 0x00000FFF,  // 通知所有触摸事件。
    UIControlEventAllEditingEvents           = 0x000F0000,  // 通知所有关于文本编辑的事件。
    UIControlEventApplicationReserved    = 0x0F000000,  // range available for application use
    UIControlEventSystemReserved          = 0xF0000000,  // range reserved for internal framework use
    UIControlEventAllEvents                      = 0xFFFFFFFF   // 通知所有事件
}; 
```