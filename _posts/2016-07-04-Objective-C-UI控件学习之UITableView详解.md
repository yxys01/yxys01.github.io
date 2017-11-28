---
layout: post
title: Objective-C-UI控件学习之UITableView详解
date: 2016-07-04
tag: Objective-C-UI控件学习
---

### 风格
&#160; &#160; &#160; &#160;UITableView有两种风格：**UITableViewStylePlain**和**UITableViewStyleGrouped**。这两者操作起来其实并没有本质区别，只是后者按分组样式显示前者按照普通样式显示而已。大家先看一下两者的应用：

&#160; &#160; &#160; &#160;**1、分组样式**
![这里写图片描述](http://img.blog.csdn.net/20160705171014182)
&#160; &#160; &#160; &#160;**2、不分组样式**
![这里写图片描述](http://img.blog.csdn.net/20160705171351011)

&#160; &#160; &#160; &#160;大家可以看到在UITableView中数据只有**行**的概念，并没有**列**的概念，因为在手机操作系统中显示多列是不利于操作的。UITableView中每行数据都是一个UITableViewCell，在这个控件中为了显示更多的信息，iOS已经在其内部设置好了多个子控件以供开发者使用。如果我们查看UITableViewCell的声明文件可以发现在内部有一个UIView控件（contentView，作为其他元素的父控件）、两个UILable控件（textLabel、detailTextLabel）、一个UIImage控件（imageView），分别用于容器、显示内容、详情和图片。使用效果类似于微信、QQ信息列表：
![这里写图片描述](http://img.blog.csdn.net/20160705171612981)

&#160; &#160; &#160; &#160;当然，这些子控件并不一定要全部使用，具体操作时可以通过UITableViewCellStyle进行设置，具体每个枚举表示的意思已经在代码中进行了注释：

```
typedef NS_ENUM(NSInteger, UITableViewCellStyle) { 
    UITableViewCellStyleDefault,    
    // 左侧显示textLabel（不显示detailTextLabel），imageView可选（显示在最左边） 
    UITableViewCellStyleValue1,        
    // 左侧显示textLabel、右侧显示detailTextLabel（默认蓝色），imageView可选（显示在最左边） 
    UITableViewCellStyleValue2,        
    // 左侧依次显示textLabel(默认蓝色)和detailTextLabel，imageView可选（显示在最左边） 
    UITableViewCellStyleSubtitle    
    // 左上方显示textLabel，左下方显示detailTextLabel（默认灰色）,imageView可选（显示在最左边） 
}; 
```


### UITableView使用

 1. 首先，Controller需要实现两个  delegate ，分别是  UITableViewDelegate 和  UITableViewDataSource
 2. 然后 UITableView对象的 delegate要设置为 self。
 3. 然后就可以实现这些delegate的一些方法拉。

```
#pragma mark 返回tableview有多少个section
（1）- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView;   
eg：
//返回有多少个Sections  
 - (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView   
{  
   return 1;  
}  
```

```
#pragma mark 返回对应的section有多少个元素，也就是多少行
（2）- (NSInteger)tableView:(UITableView *)table numberOfRowsInSection:(NSInteger)section;
 eg:
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section   
{  
    return 10；  
}  
```

```
#pragma mark 返回指定的row的高度
（3）- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath;
 eg:
 //计算Cell高度的实现：
- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath { 
    C1 *cell = (C1 *)self.prototypeCell; 
    cell.t.text = [self.tableData objectAtIndex:indexPath.row]; 
    CGSize size = [cell.contentView systemLayoutSizeFittingSize:UILayoutFittingCompressedSize]; 
    NSLog(@"h=%f", size.height + 1); 
    return 1  + size.height; 
} 
```
&#160; &#160; &#160; &#160;看了代码，可能你有点疑问，为何这儿要加1呢？笔者告诉你，如果不加1，结果就是错误的，Cell中UILabel将显示不正确。原因就是因为这行代码`CGSize size = [cell.contentView systemLayoutSizeFittingSize:UILayoutFittingCompressedSize];`由于是在cell.contentView上调用这个方法，那么返回的值将是contentView的高度，UITableViewCell的高度要比它的contentView要高1,也就是它的分隔线的高度。

```
- (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section;
//这个方法返回指定的section的header view 的高度。

- (CGFloat)tableView:(UITableView *)tableView heightForFooterInSection:(NSInteger)section;
//这个方法返回指定的section的footer view 的高度。
```

```
#pragma mark 返回指定的row的cell
（4）- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath;
```
&#160; &#160; &#160; &#160;这个地方是比较关键的地方，一般在这个地方来**定制各种个性化的 cell元素**。这里只是使用最简单最基本的cell 类型。其中有一个主标题 cell.textLabel 还有一个副标题cell.detailTextLabel,  还有一个image在最前头叫 cell.imageView.  还可以设置右边的图标，通过cell.accessoryType 可以设置是饱满的向右的蓝色箭头，还是单薄的向右箭头，还是勾勾标记。

```
eg:
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath   
{  
	 static NSString * showUserInfoCellIdentifier = @"ShowUserInfoCell";  
	 UITableViewCell * cell = [tableView_ dequeueReusableCellWithIdentifier:showUserInfoCellIdentifier];  
	 if (cell == nil)  
	 {  
	  // Create a cell to display an ingredient.  
	     cell = [[[UITableViewCell alloc] initWithStyle:UITableViewCellStyleSubtitle   	                                       reuseIdentifier:showUserInfoCellIdentifier]   
	                autorelease];  
	 }  
	  // Configure the cell.  
	     cell.textLabel.text=@"签名";  
	     cell.detailTextLabel.text = [NSString stringWithCString:userInfo.user_signature.c_str()  encoding:NSUTF8StringEncoding];  
	    }   
```

```
#pragma mark 返回指定的 section 的header的高度
(5）- (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section
eg:
- (CGFloat)tableView:(UITableView *)tableView heightForHeaderInSection:(NSInteger)section  
		{  
		    if (section ==0)  
		        return 80.0f;  
		    else  
		        return 30.0f;  
		} 		
```

```
#pragma mark 返回指定的section 的 header的 title，如果这个section header  有返回view，那么title就不起作用了
  （6）- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section
eg:
- (NSString *)tableView:(UITableView *)tableView titleForHeaderInSection:(NSInteger)section  
	{  
	    if (tableView == tableView_)  
	    {  
	        if (section == 0)   
	        {  
	            return @"title 1";  
	        }   
	        else if (section == 1)   
	        {  
	            return @"title 2";  
	        }   
	        else   
	        {  
	            return nil;  
	        }  
	    }   
	    else   
	    {  
	        return nil;  
	    }  
      }  
```


```   
#pragma mark 返回指定的section header的view，如果没有,这个函数可以不返回view
(7) - (UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section
eg:
- (UIView *)tableView:(UITableView *)tableView viewForHeaderInSection:(NSInteger)section  
{  
    if (section == 0)   
   {  
		          
       UIView* header = [[[NSBundle mainBundle] loadNibNamed: @"SettingHeaderView"   
                                                owner: self  
                                                options: nil] lastObject];  
		       
	else  
    {  
        return nil;  
    }  
}

```

```  
#pragma mark 当用户选中某个行的cell的时候，回调用这个	
   (8)  - (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
      //当用户选中某个行的cell的时候，回调用这个。但是首先，必须设置tableview的一个属性为可以select 才行。
      TableView.allowsSelection=YES;  
      cell.selectionStyle=UITableViewCellSelectionStyleBlue;  
      //如果不希望响应select，那么就可以用下面的代码设置属性：
      TableView.allowsSelection=NO;
      // 下面是响应select 点击函数，根据哪个section，哪个row 自己做出响应就好啦。
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath   
{  
    if (indexPath.section == 1)   
    {  
        return;  
    }  
    else if(indexPath.section==0)  
    {  
        switch (indexPath.row)   
        {  
            //聊天  
            case 0:  
            {  
                [self  onTalkToFriendBtn];  
            }  
                break;                   
	        default:  
                break;  
	        }  
	    }  
	    else   
	    {  
	        return ;  
	    }  	      
}  
		//如何让cell 能够响应 select，但是选中后的颜色又不发生改变呢，那么就设置 
        cell.selectionStyle = UITableViewCellSelectionStyleNone;

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath  
{  
    //cell被选中后的颜色不变  
    cell.selectionStyle = UITableViewCellSelectionStyleNone;  
｝

```

```
（9）如何设置tableview每行之间的分割线            self.tableView.separatorStyle=UITableViewCellSeparatorStyleSingleLine;  
//如果不需要分割线，那么就设置属性为 UITableViewCellSeparatorStyleNone 即可。

```

```
  #pragma mark 设置tableview cell的背景颜色
（10）- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath  
		｛  
		        //设置背景颜色  
		        cell.contentView.backgroundColor=[UIColor colorWithRed:0.957 green:0.957 blue:0.957 alpha:1];  
		｝  
 #pragma mark
  （11） 
  - (void)tableView:(UITableView *)tableView accessoryButtonTappedForRowWithIndexPath:(NSIndexPath *)indexPath
        这个函数响应，用户点击cell 右边的 箭头（如果有的话）
#pragma mark
  （12）如何设置tableview 可以被编辑
        首先要进入编辑模式：
        [TableView setEditing:YES animated:YES];  
         如果要退出编辑模式，肯定就是设置为NO
        - (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath
         返回当前cell  要执行的是哪种编辑，下面的代码是 返回 删除  模式

		- (UITableViewCellEditingStyle)tableView:(UITableView *)tableView editingStyleForRowAtIndexPath:(NSIndexPath *)indexPath  
		{  
		    return UITableViewCellEditingStyleDelete;  
		}  

        -(void) tableView:(UITableView *)aTableView commitEditingStyle:(UITableViewCellEditingStyle) editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath
        通知告诉用户编辑了 哪个cell，对应上面的代码，我们在这个函数里面执行删除cell的操作。

		-(void) tableView:(UITableView *)aTableView  
		commitEditingStyle:(UITableViewCellEditingStyle) editingStyle  
		forRowAtIndexPath:(NSIndexPath *)indexPath  
		｛  
		    [chatArray  removeObjectAtIndex:indexPath.row];  
		    [chatTableView  reloadData];  
		｝ 
#pragma mark 
  （13）如何获得 某一行的CELL对象
        - (UITableViewCell *)cellForRowAtIndexPath:(NSIndexPath *)indexPath;		
typedef NS_ENUM(NSInteger, UITableViewCellStyle) {
    UITableViewCellStyleDefault, // 左侧显示textLabel（不显示detailTextLabel），imageView可选（显示在最左边）
    UITableViewCellStyleValue1,  // 左侧显示textLabel、右侧显示detailTextLabel（默认蓝色），imageView可选（显示在最左边）
    UITableViewCellStyleValue2,  // 左侧依次显示textLabel(默认蓝色)和detailTextLabel，imageView可选（显示在最左边）
    UITableViewCellStyleSubtitle // 左上方显示textLabel，左下方显示detailTextLabel（默认灰色）,imageView可选（显示在最左边）
};
```

&#160; &#160; &#160; &#160;查看UITableView的帮助文档我们会注意到UITableView有两个Delegate分别为：dataSource和delegate。

&#160; &#160; &#160; &#160;dataSource 是UITableViewDataSource类型，主要为UITableView提 供显示用的数据(UITableViewCell)，指定UITableViewCell支持的编辑操作类型(insert，delete和 reordering)，并根据用户的操作进行相应的数据更新操作，如果数据没有更具操作进行正确的更新，可能会导致显示异常，甚至crush。

&#160; &#160; &#160; &#160;delegate 是UITableViewDelegate类型，主要提供一些可选的方法，用来控制tableView的选择、指定section的头和尾的显示以及协助完成cell的删除和排序等功能。

&#160; &#160; &#160; &#160;提到UITableView，就必须的说一说NSIndexPath。UITableView声明了一个NSIndexPath的类别，主要用 来标识当前cell的在tableView中的位置，该类别有section和row两个属性，前者标识当前cell处于第几个section中，后者代 表在该section中的第几行。
　　
&#160; &#160; &#160; &#160;UITableView只能有一列数据(cell)，且只支持纵向滑动，当创建好的tablView第一次显示的时候，我们需要调用其reloadData方法，强制刷新一次，从而使tableView的数据更新到最新状态。