---
layout: post
title: Objective-C学习之iOS视图控制对象的生命周期
date: 2016-05-23
tag: Objective-C学习
---
### iOS 视图控制对象的生命周期如下：
<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>init</td>
    <td>初始化程序</td>
    </tr>
    <tr>
        <td>viewDidLoad</td>
    <td>加载视图</td>
    </tr>
     <tr>
        <td>viewWillAppear</td>
    <td>UIViewController对象的视图即将加入窗口时调用</td>
    </tr>
     <tr>
        <td>viewDidApper</td>
    <td>UIViewController对象的视图已经加入到窗口时调用</td>
    </tr>
         <tr>
        <td>viewWillDisappear</td>
    <td>UIViewController对象的视图即将消失、被覆盖或是隐藏时调用</td>
    </tr>
         <tr>
        <td>viewDidDisappear</td>
    <td>UIViewController对象的视图已经消失、被覆盖或是隐藏时调用</td>
    </tr>
         <tr>
        <td>viewVillUnload</td>
    <td>当内存过低时，需要释放一些不需要使用的视图时，即将释放时调用</td>
    </tr>
         <tr>
        <td>viewDidUnload</td>
    <td>当内存过低，释放一些不需要的视图时调用</td>
    </tr>
</table>

iOS 开发中手动 `performSegueWithIdentifier` 不生效的原因：
很简单：如果在 `viewDidLoad` 时就启动 `Segue` 的话，依然会被后来填充的视图覆盖，要是在视图载入完成以后的 `viewDidAppear` 中启动 `Segue`，就 OK 了！ 

