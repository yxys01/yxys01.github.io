---
layout: post
title: Objective-C学习之用CoreLocation实现地图定位
date: 2016-05-25
tag: Objective-C学习
---
#### 引入库文件
```objectivec
#import "ViewController.h"
#import <CoreLocation/CoreLocation.h>
 
@interface ViewController ()<CLLocationManagerDelegate>
/**
 *  定位管理者
 */
@property (nonatomic ,strong) CLLocationManager *mgr;
@end
 
@implementation ViewController
```

```objectivec
/*
1.创建定位管理者
CLLocationManager *mgr = [[CLLocationManager alloc] init];

2.设置代理
mgr.delegate = self;
*/

3.开始定位
//[mgr startUpdatingLocation];
[self.mgr startUpdatingLocation];
```


//定位到用户的位置会调用该方法（并且该方法调用非常频繁（非常耗电））
```objectivec
-(void)locationManger:(CLLocationManager *)manager didUpdateLocations:(NSArray *)locations{
    CLLocation * location = [locations lastObject];//获取用户位置信息的对象（最后一个即最新一个）
    CLLocationCoordinate2D coordinate = location.coordinate;

    [manager stopUpdatingLocation];//使其停止，减少耗电
}
```

//计算俩个经纬度之间的距离
```objectivec
-(void) countDistance
{
    CLLocation * location1 = [[CLLocation alloc] initwithLatitude:23.23 longitude:113.33];
    CLLocation * location2 = [[CLLocation alloc] initwithLatitude:40.06 longitude:116.39];

    CLLocationDistance distance = [location1 distanceFromLocation:location2]; 

}
```
#### 启用
```objectivec
#pragma mark - 懒加载
-(CLLocationManager *)mgr
{
      
   if(_mgr == nil){
   1.创建定位管理者
      _mgr = [[CLLocationManager alloc] init];
      2.设置代理
      _mgr.delegate = self;
      3.位置间隔之后重新定位
      _mgr.distancaFilter = 10;
      4.定位的精确度
      _mgr.desiredAccuracy = kCLLocationAccuracyBestForNavigation;
   }
   return _mgr;
}  
```

CLLocationCoordinate2D(latitude 纬度;longitude 经度) 结构体
<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>coordinate </td>
    <td>经纬度（拿到经纬度）</td>
    </tr>
    <tr>
        <td>objc_registerClassPair</td>
    <td>海拔；高度</td>
    </tr>
     <tr>
        <td>horizonalAccuracy </td>
    <td>水平误差</td>
    </tr>
     <tr>
        <td>verticalAccuracy  </td>
    <td>垂直误差
</td>
</table>




使用`CLGeocoder`可以完成“**地理编码**”和“**反地理编码**”

**地理编码**：根据给定的地名，获取具体的位置信息（比如经纬度、地址的全称等）

**反地理编码**：根据给定的经纬度，获得具体的位置信息

地理编码方法
```objectivec
- (void)geocodeAddressString:(NSString *)addressString completionHandler:(CLGeocodeCompletionHandler)completionHandler;
```
反地理编码方法
```objectivec
- (void)reverseGeocodeLocation:(CLLocation *)location completionHandler:(CLGeocodeCompletionHandler)completionHandler;
```

```objectivec
import <MapKit/MapKit.h>
<MKMapViewDelegate>
//设置代理
self.mapView.delegate = self;
//跟踪用户位置
self.mapView.userTrackingMode = MKUserTrackingModeFollow;
//设置地图类型
self.mapView.mapType = MKMapTypeSatellite;
```

//定位到用户的位置会执行该方法
```objectivec
//userLocation 大头针模型
-(void) mapView:(MKMapView *)mapView didUpdateUserLocation:(MKUserLocation *)userLocation
{
    //取出用户的位置
     CLLocationCoordinate2D coordinate = userlocation.location.coordinate;
     NSLog(@"纬度：%f 经度：%f", coordinate.latitude,coordinate.longitude);

     //改变大头针显示的内容（通过改变大头针模型的属性）
     //userLocation.title = @"";
     //userLocation.subtitle = @"";
     CLGeocoder *geocoder = [[userLocation alloc] init];
     [geocoder reverseGeocoderLocation:location completionHandler:^(NSArray *placemarks,NSError *error){
     if(placemarks.count == 0 || error)return;
     CLPlacemark *pm = [placemarks firstObject];

     if(pm.locality){
         userLocation.title = pm.locality;
     }else
     {
     userLocation.title = pm.administrativeArea;
     }
     userLocation.subtitle = pm.name;
     } ]

     //设置mapView显示的位置(设置用户的位置为地图的中心点)
     [mapView setCenterCoordinate:coordinate animated:YES];

     //设置显示区域
     MKCoordinateSpan span = MKCoordinateSpanMake(0.01，0.01);//经纬度跨度（缩放大小，越小地方越清晰）
     MKCoordinateRegion region = MKCoordinateRegionMake(coordinate,span);
     [mapView setRegion:region  animated:YES];
}
```
//经纬度跨度已经发生改变
```
-(void)mapView:(MKMapView *)mapView regionDidchangeAnimated:(BOOL)animated
{
    MKCoordinateRegion region = mapView.region;
    CLLocationCoordinate2D center = region.center;
    MKCoordinateSpan span = region.span;
    NSLog(@"纬度：%f 经度：%f", coordinate.latitude,coordinate.longitude);
    NSLog(@"纬度跨度：%f 经度跨度：%f",span.latitudeDelta,span.longitudeDelta);

}
```
```objectivec
// 点击回到中心点
[self.mapView setCenterCoordinate:self.mapView.userlocation.location.coordinate animated:YES];
//或者：
MKCoordinateSpan span = MKCoordinateSpanMake(0.002703,0.001717);
MKCoordinateRegion region = MKCoordinateRegionMake(self.mapView.userlocation.location.coordinate,span);
[self.mapView setRegion:region animated:YES];
```

```objectivec
CLPlacemark - 地标
CLLocation *location
NSDictionary *addressDictionary
```
```objectivec
MKUserLocation - 大头针模型
CLLocation *location
NSString *title
NSString *subtitle
```
```
CLLocation - 位置
CLLocationCoordinate2D coordinate
CLLocationDistance altitude海拔；高度
```
```objectivec
typedef struct 
{
    CLLocationCoordinate2D center;
    MKCoordinateSpan span;
}MKCoordinateRegion;  区域

typedef struct 
{
    CLLocationDegrees latitude;
    CLLocationDegrees longitude;
}CLLocationCoordinate2D;  经纬度

typedef struct 
{
    CLLocationDegrees latitudeDelta;
    CLLocationDegrees longitudeDelta;
}MKCoordinateSpan; 跨度
```

**大头针基本操作**

```objectivec
//添加一个大头针
-(void)addAnnotation:(id <MKAnnotation>)annotation;
//添加多个大头针
-(void)addAnnotations:(NSArray *)annotations;
//移除一个大头针
-(void)removeAnnotation:(id <MKAnnotation>)annotation;
//移除多个大头针
-(void)removeAnnotations:(NSArray)annotations;
```

```objectivec
//点击一次添加一个大头针
-(void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)withEvent
{
   //1.获取用户点击的店
    CGPoint point = [[touches anyObject] locationInView:self.view];

   //2.将该点转化为经纬度（地图上的坐标）
    CLLocationCoordinate2D coordinate = [self.mapView convertPoint:point toCoordibateFromView:self.view];
    //@interface MyAnnotation :NSObject<MKAnnotation>
   //3.添加大头针
    MyAnnotation *anno = [[MyAnnotation alloc] init];
    anno.coordinate = coordinate;
    anno.title = @"";
    anno.subtitle = @"";
    [self.mapView addAnnotation:anno];
}
//在地图上添加一个大头针就会执行该方法
//annotation 大头针模型对象
//返回 大头针的View(返回nil表示默认使用系统,默认MKAnnotationView是不可见)
-(MKAnnotationView *)mapView:(MKMapView *)mapView viewForAnnotation:(id<MKAnnotation>)annotation
{  
   //1.如果是用户位置的大头针，直接返回nil，使用系统的
   if([annotation isKindOfClass:[MKUserLocation class]]) return nil;
   //2.创建标识
   static NSString *ID = @"annoView";
   //3.从缓冲池中取出大头针的View
   MKAnnotationView *annoView = [mapView dequeueReusableAnnotationViewWithIdentifier:ID];
   //4.如果为nil，则创建
   if(annoView == nil)
   {
   annoView = [[MKAnnotationView alloc]initWithAnnotation:nil reuseIdentifier:ID];
   //1.设置标题和子标题可以呼出
   annoView.canShowCallout = YES;

   //在左侧放一个View
   annoView.leftCalloutAccessoryView = [UIButton buttonWithType:UIButtonTpyeContactAdd];
   //在右侧放一个View
   annoView.rightCalloutAccessoryView = [UIButton buttonWithType:UIButtonTpyeDetailDisclo];
   //2.设置大头针颜色
   annoView.pinColor = MKPinAnnotationColorPurple;

   //3.掉落效果
   annoView.animatesDrop = YES;

   //设置图片
   //annoView.image = [UIImage imageNamed:@""];
   }
   //5.设置大头针的大头针模型
   annoView.annotation = annotation; 

}
//大头针的View已经被添加mapView会执行该方法
// views  所有大头针的View都存放在该数组中
-(void)mapView:(MKMapView *)mapView didAddAnnotationViews:(NSArray *)views
{
   for(MKAnnotationView *annoView in views)
   {
      //如果是系统的大头针View直接返回
      if([annoView.annotation isKindOfClass:[MKUserLocation class]]) return;

      //取出大头针View的最终应该在的位置
    CGRect endFrame = annoView.frame;

    //给大头针重新设置一个位置
    annoView.frame = CGRectMake(endFrame.origin.x,0,endFrame.size.width,endFrame.size.height);

    //执行动画（y轴掉落动画）
    [UIView animateWithDuration:1.0 animations:^{
        annoView.frame = endFrame;
    }];
   }
}
```