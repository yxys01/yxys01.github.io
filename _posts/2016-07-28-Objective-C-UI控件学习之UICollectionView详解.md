---
layout: post
title: Objective-C-UI控件学习之UICollectionView详解
date: 2016-07-28
tag: Objective-C-UI控件学习
---
&#160; &#160; &#160; &#160;**UICollectionView** 和 **UICollectionViewController** 类是iOS6 新引进的API，用于展示集合视图，布局更加灵活，可实现多列布局，用法类似于UITableView 和 UITableViewController 类。

###使用前提
&#160; &#160; &#160; &#160;使用**UICollectionView** 必须实现
`UICollectionViewDataSource,UICollectionViewDelegate,UICollectionViewDelegateFlowLayout`这三个协议。

###常用方法
&#160; &#160; &#160; &#160;下面先给出常用到的一些方法。（只给出常用的，其他的可以查看相关API） 

```
#pragma mark -- UICollectionViewDataSource   
//定义展示的UICollectionViewCell的个数  
-(NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section  
{  
    return 30;  
}   

```

```
//定义展示的Section的个数  
-(NSInteger)numberOfSectionsInCollectionView:(UICollectionView *)collectionView  
{  
    return 1;  
}   

```

```
//每个UICollectionView展示的内容  
-(UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath  
{  
    static NSString * CellIdentifier = @"GradientCell";  
    UICollectionViewCell * cell = [collectionView dequeueReusableCellWithReuseIdentifier:CellIdentifier forIndexPath:indexPath];  
  
    cell.backgroundColor = [UIColor colorWithRed:((10 * indexPath.row) / 255.0) green:((20 * indexPath.row)/255.0) blue:((30 * indexPath.row)/255.0) alpha:1.0f];  
    return cell;  
}   
```

```
#pragma mark --UICollectionViewDelegateFlowLayout   
//定义每个UICollectionView 的大小  
- (CGSize)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout*)collectionViewLayout sizeForItemAtIndexPath:(NSIndexPath *)indexPath  
{  
    return CGSizeMake(96, 100);  
}   
```

```
//定义每个UICollectionView 的 margin  
-(UIEdgeInsets)collectionView:(UICollectionView *)collectionView layout:(UICollectionViewLayout *)collectionViewLayout insetForSectionAtIndex:(NSInteger)section  
{  
    return UIEdgeInsetsMake(5, 5, 5, 5);  
}   
```
```
#pragma mark --UICollectionViewDelegate   
//UICollectionView被选中时调用的方法  
-(void)collectionView:(UICollectionView *)collectionView didSelectItemAtIndexPath:(NSIndexPath *)indexPath  
{  
    UICollectionViewCell * cell = (UICollectionViewCell *)[collectionView cellForItemAtIndexPath:indexPath];  
    cell.backgroundColor = [UIColor whiteColor];  
}   
```

```
//返回这个UICollectionView是否可以被选择  
-(BOOL)collectionView:(UICollectionView *)collectionView shouldSelectItemAtIndexPath:(NSIndexPath *)indexPath  
{  
    return YES;  
}  
```

