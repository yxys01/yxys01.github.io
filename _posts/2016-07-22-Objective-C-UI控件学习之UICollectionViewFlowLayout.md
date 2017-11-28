---
layout: post
title: Objective-C-UI控件学习之UICollectionViewFlowLayout（
date: 2016-07-22
tag: Objective-C-UI控件学习
---

&#160; &#160; &#160; &#160;UICollectionView中有个重要的内容 UICollectionViewLayout ，UICollectionView的显示是由其布局文件决定的。

### 定义
&#160; &#160; &#160; &#160;**UICollectionViewFlowLayout** ：系统提供的**流水布局**，如果要自定义流水布局的效果可以自定义这个类。

&#160; &#160; &#160; &#160;布局决定每一个**cell**的**尺寸，位置，间距**等等。

&#160; &#160; &#160; &#160;每一个**cell/item**都有自己**UICollectionViewLayoutAttributes**

&#160; &#160; &#160; &#160;每一个**indexPath**也都有自己**UICollectionViewLayoutAttributes**

### 开始

&#160; &#160; &#160; &#160;这次做的吸附效果也完全是自定义了 UICollectionViewFlowLayout ，

&#160; &#160; &#160; &#160;下面对这个类的主要方法进行大体介绍：

&#160; &#160; &#160; &#160;**1、prepareLayout**

&#160; &#160; &#160; &#160;一些**初始化**的工作最好这里完成，比如item的大小等等
```
-(void)prepareLayout
{
[super prepareLayout];//需要调用super方法

//初始化
self.itemSize = CGSizeMake(90, 90);//设置item的大小
self.scrollDirection = UICollectionViewScrollDirectionHorizontal;//设置滚动防线
self.minimumLineSpacing = 10;//设置cell的间距
self.sectionInset = UIEdgeInsetsMake(0, 10, 0, 10);//设置四周的间距
}
```

&#160; &#160; &#160; &#160;**2、targetContentOffsetForProposedContentOffset** 

&#160; &#160; &#160; &#160;控制最后UICollectionView的最后去哪里，我们这里需要做的吸附效果的逻辑代码就需要在这里完成。参数介绍 proposedContentOffset :原本UICollectionView停止滚动那一刻的位置； velocity ：滚动速度

```
-(CGPoint)targetContentOffsetForProposedContentOffset:(CGPoint)proposedContentOffset withScrollingVelocity:(CGPoint)velocity
{
    //TODO
}
```

&#160; &#160; &#160; &#160;**3、shouldInvalidateLayoutForBoundsChange** 

&#160; &#160; &#160; &#160;边界发生改变时，是否需要重新布局，返回YES就需要重新布局(会自动调用**layoutAttributesForElementsInRect**方法，获得所有**cell**的布局属性)

```
-(BOOL)shouldInvalidateLayoutForBoundsChange:(CGRect)newBounds
{

return YES;

}
```

&#160; &#160; &#160; &#160;**4、layoutAttributesForElementsInRect** 

&#160; &#160; &#160; &#160;返回所有cell的布局属性

```
-(NSArray<UICollectionViewLayoutAttributes *> *)layoutAttributesForElementsInRect:(CGRect)rect
{
    return [super layoutAttributesForElementsInRect:rect];
}
```

&#160; &#160; &#160; &#160;方法介绍完毕，我们再 prepareLayout

```
-(CGPoint)targetContentOffsetForProposedContentOffset:(CGPoint)proposedContentOffset withScrollingVelocity:(CGPoint)velocity
{
    //1.计算scrollview最后停留的范围
    CGRect lastRect ;
    lastRect.origin = proposedContentOffset;
    lastRect.size = self.collectionView.frame.size;
    
    //2.取出这个范围内的所有属性
    NSArray *array = [self layoutAttributesForElementsInRect:lastRect];
    
    //起始的x值，也即默认情况下要停下来的x值
    CGFloat startX = proposedContentOffset.x;
    
    //3.遍历所有的属性
    CGFloat adjustOffsetX = MAXFLOAT;
    for (UICollectionViewLayoutAttributes *attrs in array) {
        CGFloat attrsX = CGRectGetMinX(attrs.frame);
        CGFloat attrsW = CGRectGetWidth(attrs.frame) ;

        if (startX - attrsX  < attrsW/2) {
            adjustOffsetX = -(startX - attrsX+ItemMaigin);
        }else{
            adjustOffsetX = attrsW - (startX - attrsX);
        }
    
        break ;//只循环数组中第一个元素即可，所以直接break了
    }
    return CGPointMake(proposedContentOffset.x + adjustOffsetX, proposedContentOffset.y);
}
```

&#160; &#160; &#160; &#160;这样我们要做的吸附效果的Layout文件就完成了。

&#160; &#160; &#160; &#160;我们在初始化UICollectionView的时候选择带有Layout参数的init方法即可。

```
UICollectionView *collectionView = [[UICollectionView alloc]initWithFrame:rect collectionViewLayout:viscosityLayout];
```

