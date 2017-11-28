---
layout: post
title: Objective-C-UI控件学习之下拉刷新
date: 2016-07-07
tag: Objective-C-UI控件学习
---

&#160; &#160; &#160; &#160;在**UITableView**中实现下拉刷新

![这里写图片描述](http://img.blog.csdn.net/20160707101851009)
![下拉时实现](http://img.blog.csdn.net/20160707101903306)

&#160; &#160; &#160; &#160;创建基于UITableViewController类的TableViewController类

&#160; &#160; &#160; &#160;**TableViewController.h**

```
#import <UIKit/UIKit.h>

@interface TableViewController : UITableViewController
@property(nonatomic)int count;
@property(nonatomic,retain)NSMutableArray *countArr;

@end

```
&#160; &#160; &#160; &#160;**TableViewController.m**

```objectivec
#import "TableViewController.h"

@interface TableViewController ()

@end

@implementation TableViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    self.count = 0;
    self.countArr = [[NSMutableArray alloc]initWithCapacity:16];
    
    UIRefreshControl *refresh = [[UIRefreshControl alloc]init];
    //设置颜色
    refresh.tintColor = [UIColor redColor];
    //设置刷新时提示字
    refresh.attributedTitle = [[NSAttributedString alloc] initWithString:@"下拉刷新"];
    //添加动作
    [refresh addTarget:self action:@selector(refreshView:) forControlEvents:UIControlEventValueChanged];
    self.refreshControl = refresh;
 
}

//实现刷新
-(void)refreshView:(UIRefreshControl *)refresh
{
    if(refresh.refreshing){
        refresh.attributedTitle = [[NSAttributedString alloc]initWithString:@"正在加载，请稍后......"];
        [self performSelector:@selector(handleData) withObject:nil afterDelay:2];
        
    }

}
//刷新数据
-(void)handleData{
    NSDateFormatter *formatter = [[NSDateFormatter alloc]init];
    //设置格式
    [formatter setDateFormat:@"MMM d,h:mm:ss a"];
    //创建字符串对象
    NSString *lastUpdated = [NSString stringWithFormat:@"最后加载的内容为： %@", [formatter stringFromDate:[NSDate date]]];
    self.refreshControl.attributedTitle = [[NSAttributedString alloc]initWithString:lastUpdated];
    self.count++;
    //添加对象
    [self.countArr addObject:[NSString stringWithFormat:@"%d. %@",self.count,[formatter stringFromDate:[NSDate date]]]];
    NSLog(@"%@",self.countArr);
    //结束刷新
    [self.refreshControl endRefreshing];
    [self.tableView reloadData];
}


- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

#pragma mark - Table view data source
//获取表视图的块
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}
//获取行数
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return self.countArr.count;
}

//获取某一行的数据
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    static NSString *CellIdentifier = @"Cell";
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:CellIdentifier];
    if(cell ==  nil)
    {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:CellIdentifier];
    }
    //设置文本内容
    cell.textLabel.text = [self.countArr objectAtIndex:indexPath.row];
    cell.textLabel.font = [UIFont systemFontOfSize:17];
    return cell;
}



@end
```
