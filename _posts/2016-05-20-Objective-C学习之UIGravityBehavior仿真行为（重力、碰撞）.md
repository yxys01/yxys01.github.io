---
layout: post
title: Objective-C学习之UIGravityBehavior仿真行为（重力、碰撞)
date: 2016-05-20
tag: Objective-C学习
---

## 重力特性UIGravityBehavior

UIDynamicBehavior：仿真行为，是动力学行为的父类，基本的动力学行为类

UIGravityBehavior、UICollisionBehavior、UIAttachmentBehavior、UISnapBehavior、UIPushBehavior以及UIDynamicItemBehavior均继承自该父类

#### UICollisionBehavior 碰撞检测
隐式的调用了一个UICollisionBehavior的属性translatesReferenceBoundsIntoBoundary，将这个属性设置为YES之后。会使边界引用使用视图提供的UIDynamicAnimator边界。

（1）谁要进行物理仿真？
　　**物理仿真元素（Dynamic Item）**
（2）执行怎样的物理仿真效果？怎样的动画效果？
　　**物理仿真行为（Dynamic Behavior）** 
（3）让物理仿真元素执行具体的物理仿真行为
　　**物理仿真器（Dynamic Animator）**

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>UIGravityBehavior</td>
    <td>重力行为</td>
    </tr>
    <tr>
        <td>UICollisionBehavior</td>
    <td>碰撞行为</td>
    </tr>
     <tr>
        <td>UISnapBehavior</td>
    <td>捕捉行为</td>
    </tr>
     <tr>
        <td>UIPushBehavior</td>
    <td>推动行为</td>
    </tr>
         <tr>
        <td>UIAttachmentBehavior</td>
    <td>附着行为</td>
    </tr>
     <tr>
        <td>UIDynamicItemBehavior</td>
    <td>动力元素行为</td>
    </tr>
</table>
