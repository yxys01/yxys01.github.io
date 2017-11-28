---
layout: post
title: Objective-C学习之常用的类名（持续更新）
date: 2016-05-24
tag: Objective-C学习
---

### 常见的类名
 1. **NSPredicate**：用于查询，原理和用法都类似于SQL中的where，作用相当于数据库
 2. **NSCharacterSet**，以及它的可变版本**NSMutableCharacterSet**，用面向对象的方式来表示一组Unicode字符。它经常与NSString及NSScanner组合起来使用，在不同的字符上做过滤、删除或者分割操作
 3. **NSRange**： 表示范围的结构体
 4. **NSArray**：表示不可变数组
 5. **NSMutableArray**：表示可变数组
 6. **NSMakeRange**：是一个结构体类型，包含两个参数，位置和长度。表示字符串要传进来从哪里开始的位置和需要的长度。`NSMakeRange(loc,len)` 
 7. **NSSet**：到底什么类型，其实它和NSArray功能性质一样，用于存储对象，属于集合； **NSSet**，**NSMutableSet**类声明编程接口对象，无序的集合，在内存中存储方式是不连续的，不像**NSArray**（是有序的集合）类声明编程接口对象是有序集合，在内存中存储位置是连续的；**NSSet**和我们常用**NSArry**区别是：在搜索一个一个元素时**NSSet**比**NSArray**效率高
 8. **NSLocale**：可以获取用户的本地化信息设置，例如货币类型，国家，语言，数字，日期格式的格式化，提供正确的地理位置显示等等。下面的代码获取机器当前语言和国家代码。
 9. **NSBundle**：是一个目录,其中包含了程序会使用到的资源. 这些资源包含了如图像,声音,编译好的代码,`nib`文件(用户也会把`bundle`称为`plug-in`). 对应`bundle`,`cocoa`提供了类**NSBundle**.一个应用程序看上去和其他文件没有什么区别. 但是实际上它是一个包含了nib文件,编译代码,以及其他资源的目录. 我们把这个目录叫做程序的`main bundle`。通过这个路径可以获取到应用的信息，例如应用名、版本号等。
 10. **UIDevice**：提供了多种属性、类函数及状态通知，帮助我们全方位了解设备状况。从检测电池电量到定位设备与临近感应，**UIDevice**所做的工作就是为应用程序提供用户及设备的一些信息。**UIDevice**类还能够收集关于设备的各种具体细节，例如机型及iOS版本等。其中大部分属性都对开发工作具有积极的辅助作用。下面的代码简单的使用**UIDevice**获取手机属性。         
 11. **NSUserDefaults**：适合存储轻量级的本地数据，比如要保存一个登陆界面的数据，用户名、密码之类的，个人觉得使用**NSUserDefaults**是首选。下次再登陆的时候就可以直接从**NSUserDefaults**里面读取上次登陆的信息咯。
 12. **NSGregorianCalendar**：公历
 13. **NSDateFormatter**：调整时间格式的代码
 14. **NSDateComponents**：封装在一个可扩展的，面向对象的方式的日期组件。它是用来弥补时间的日期和时间组件提供一个指定日期：小时，分钟，秒，日，月，年，等等。它也可以用来指定的时间，例如，5小时16分钟。一个**NSDateComponents**对象不需要定义所有组件领域。当一个**NSDateComponents**的新实例被创建，日期组件被设置为**NSUndefinedDateComponent**。
 15. **NSLocalizedString**：国际化
 16. **NSLayoutConstraint**：自动布局
 17. **UIImagePickerController**： 是系统提供的用来获取图片和视频的接口；
 18. **UIGraphicsBeginImageContext**：创建一个基于位图的上下文(`context`),并将其设置为当前上下文(`context`)。
 19. **NSCache**：是苹果官方提供的缓存类，用法与**NSMutableDictionary**的用法很相似，在**AFNetworking**和**SDWebImage**中，使用它来管理缓存
 20. **NSNumber**:数字对象
 21. **NSString**：字符串对象
 22. **NSDictionary**：不可变字典
 23. **NSMutableDictionary**：可变字典
 24. **NSFileManager**：文件管理器
 25. **NSFileHandle**：提供处理文件IO的相关方法
 26. **NSDate**：日期与时间
 27. **NSCalendarDate**：**NSCalendarDate**对象包含了日期和时间、时区以及一个带有格式的字符串，它从**NSDate**继承而来。
**NSCalendarDate**对象是`immutable`的，一旦被创建，无法修改其中的时间和日期，当然可以修改那个带格式的字符串和时区。
 28. **NSCalendar**：日历
 29. **NSTimeZone**：时区
 30. **NSTimer**：定时器
 31. **NSProcessInfo**：可用于获取该进程的相关信息，包括获取运行该程序的参数、进程标识符等。除此之外，**NSProgressInfo**还用于获取该进程所在系统的主机名、操作系统名、操作系统版本等信息。
 32. **NSThread**：线程对象，相对轻量级，但需要管理线程的生命周期、同步、加锁问题，这会导致一定的性能开销
 33. **NSLock**：线程锁
 34. **NSData**：不可变数据对象
 35. **NSMutableData**:可变数据对象
 36. **NSKeyedArchiver**：归档
 37. **UIWindow**：窗口对象
 38. **UIColor**：颜色对象
 39. **UIView**：自定义视图对象
 40. **UITextFiled**：文本框控件
 41. **UITextView**：多行文本控件
 42. **UIImage**：图像
 43. **UIImageView**：图像视图
 44. **UITableView**：表格
 45. **UIButton**：按钮控件
 46. **UIDatePicker**：日期选择器
 47. **UIProgressView**：进度条
 48. **UIScrollView**：滚动视图（**UIScrollView**）通常用于显示内容尺寸大于屏幕尺寸的视图。滚动视图有以下两个主要作用：
让用户可以通过拖拽手势来观看想看到的内容
让用户可以通过捏合手势来放大或缩小观看的内容（**UITableView**继承**UIScrollView**）
 49. **UISwitch**：开关按钮
 50. **UISegmentedControl**：分段控件
 51. **UIActivityIndicatorView**：用于表示任务正在进行时，该控件显示一个旋转的进度环，由于该进度环只是用旋转来表示任务正在进行中，它不会精确显示进度完成的百分比，因此该控件相当于不显示进度的进度环。
 52. **UISlider**：拖动条
 53. **UIAlertView**：警告框
 54. **UIActionSheet**：**UIActionSheet**是在iOS弹出的选择按钮项，可以添加多项，并为每项添加点击事件。
 55. **UIAlertController**：**UIAlertController**在功能上是和**UIAlertView**以及**UIActionSheet**相同的，**UIAlertController**以一种模块化替换的方式来代替这两货的功能和作用。
 56. **UIPickerView**：选择器（单列、多列、自定义）
 57. **UIVisualEffectView**：毛玻璃效果
 58. **UIStepper**：微调器
 59. **UIWebView**：网页控件
 60. **UIToolBar**：工具条
 61. **UITableViewController**：表格控制器
 62. **UITableViewCell**：表格行
 63. **UISearchBar**：搜索条
 64. **UIRefreshController**：刷新控件；当程序创建**UIRefreshController**控件时，可以为该控件的刷新事件指定事件处理方法。当用户通过该刷新控件进行数据刷新时，系统就会激发该事件处理方法，该方法用于从底层数据库、网络、远程应用等地方检索数据，并将这些数据添加、显示到表格中。
 65. **UISearchDisplayController**：该控件整合**UISearchBar**、**UITableView**，内部提供了良好的封装，开发者只要利用该控件，即可实现在UISearchBar下方动态显示一个**UITableView**，让该控件加载、显示查询结果。（即程序可以直接在搜索条下方显示搜索列表）
 66. **UINavigationBar**：导航条
 67. **UINavigationController**：导航控制器
 68. **UICollectionView**：网格
 69. **UICollectionViewController**：网格控制器
 70. **UITabBar**：标签条
 71. **UITabBarController**：标签页控制器
 72. **UIPageControl**：页控件
 73. **UIPageViewController**：页控制器
 74. **UIGestureRecognizer**：手势控制器
 75. **UIApplication**：**UIApplication**对象是应用程序的象征，一个**UIApplication**对象就代表一个应用程序；每一个应用都有自己的**UIApplication**对象，而且是单例的，如果试图在程序中新建一个**UIApplication**对象，那么将报错提示；通过`[UIApplication sharedApplication]`可以获得这个单例对象； 一个iOS程序启动后创建的第一个对象就是**UIApplication**对象，且只有一个（通过代码获取两个**UIApplication**对象，打印地址可以看出地址是相同的）；利用**UIApplication**对象，能进行一些应用级别的操作
 76. **NSOperation**：**NSOperation**的代表计算的单个单元。这是一个抽象类，让子类状态，优先级，依赖，和消除模型等方面的有用的，线程安全的方式。
任务本身的**NSOperation**的例子包括网络请求，调整图像大小，语言处理，或任何其他可重复的，结构性的，长期运行的任务，处理后的数据返回。（可视为向线程池添加的操作**NSOperation**）
 77. **NSOperationQueue**：**NSOperationQueue**调节操作并发执行。它作为一个优先级队列，执行这样的操作大致先入先出的方式，具有较高的优先级（**NSOperation**的`queuePriority`的）那些低优先级的跳跃前进。**NSOperationQueue**执行操作的同时，选项可以同时执行（`maxConcurrentOperationCount`）的最大数量限制。（可以看成线程池）
 78. **NSURLConnection**负责发送请求，建立客户端和服务器的连接。发送**NSURLRequest**的数据给服务器，并收集来自服务器的响应数据
 79. **NSURL**：请求地址
 80. **NSURLRequest**：封装一个请求，保存发给服务器的全部数据，包括一个NSURL对象，请求方法、请求头、请求体....
 81. **NSMutableURLRequest**：**NSURLRequest**的子类；向服务器发送数据
 82. **NSNotificationCenter**：通知中心
 83. **NSJSONSerialization**：负责支持JSON解析或生成
 84. **UIPresentationController**： 从iOS8开始，`controller`之间的跳转特效，需要用新的API **UIPresentationController**来实现。比如希望实现这样一个特效：显示一个模态窗口，大小和位置是自定义的，遮罩在原来的页面上。
 85. **NSZone**：区域。它是为防止内存碎片化而引入的结构。对内存分配的区域本身进行多重化管理，根据使用对象的目的、对象的大小分配内存，从而提高了内存管理的效率。
 但是，如同苹果官方文档Programming With ARC Release Notes中所说，现在的运行时系统只是简单地忽略了区域的概念。运行时系统的内存管理本身已极具效率，使用区域来管理反而会引起内存使用效率低下以及源代码复杂化等问题。
 86. **NSValue**：一个**NSValue**对象是用来存储一个C或者Objective－C数据的简单容器。它可以保存任意类型的数据，比如int，float，char，当然也可以是指pointers, structures, and object ids。**NSValue**类的目标就是允许以上数据类型的数据结构能够被添加到集合里，例如那些需要其元素是对象的数据结构，如**NSArray**或者**NSSet**的实例。需要注意的是NSValue对象一直是不可枚举的。
 87. 持续更新
 










