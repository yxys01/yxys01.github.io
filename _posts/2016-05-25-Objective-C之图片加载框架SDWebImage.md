---
layout: post
title: Objective-C之图片加载框架SDWebImage
date: 2016-05-25
tag: Objective-C学习
---

#### 简介
&#160; &#160; &#160; &#160;在iOS的图片加载框架中，SDWebImage可谓是占据大半壁江山。它支持从网络中下载且缓存图片，并设置图片到对应的UIImageView控件或者UIButton控件。在项目中使用SDWebImage来管理图片加载相关操作可以极大地提高开发效率，让我们更加专注于业务逻辑实现。
#### SDWebImage核心方法
```objectivec
//SDWebImage
/**
  @param url            图像的URL
  @param placeholder    占位图
  @param options        选项（枚举）
  @param progressBlock  进度块代码
  @param completedBlock 完成的块代码
*/
- (void)sd_setImageWithURL:(NSURL *)url placeholderImage:(UIImage *)placeholder options:(SDWebImageOptions)options progress:(SDWebImageDownLoaderProgressBlock)progressBlock completed:(SDWebImageCompletionBlocak)completedBlock;
```
<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>receivedSize </td>
    <td>已经接收到的大小</td>
    </tr>
    <tr>
        <td>expectdSize  </td>
    <td>期望的大小，总大小</td>
    </tr>
</table>



#### 进度条：
```
progress:^(NSInteger receivedSize,NSInteger expectdSize){
     float progress = (float)receivedSize/expectdSize;
     NSLog(@"下载进度 %f",progress);
}
options: SDWebImageRetryFailed | SDWebImageLowPriority 
```

//下载失败，重新下载
```
SDWebImageRetryFailed
```
//低优先级。UI交互的时候，暂停下载图片。在滚动的时候，延迟下载
```
SDWebImageLowPriority
```
//仅在内存中缓存，不在沙河里面缓存
```
SDWebImageCacheMemoryOnly
```
//即使图像被缓存，遵守 HTPP 响应的缓存控制，如果需要，从远程刷新图像;仅在无法使用嵌入式缓存清理参数确定图像 URL 时，使用此标记
```
SDWebImageProgressiveDownload
```

<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>SDWebImageManager</td>
    <td>SDWebImage核心类</td>
    </tr>
    <tr>
        <td>SDWebImageDownloader </td>
    <td>图片下载类，管理图像下载操作</td>
    </tr>
     <tr>
        <td>SDImageCache </td>
    <td>图片缓存类，支持内存缓存和磁盘缓存</td>
    </tr>
     <tr>
        <td>SDWebImageDownloaderOperation </td>
    <td>图像下载操作，处理一个单一的图像下载</td>
    </tr>
</table>
 





#### 内存处理：当APP接收到内存警告时，SDWebImage做了什么？
&#160; &#160; &#160; &#160;`SDWebImage`会监听系统的`UIApplicationDidReceiceMemoryWarningNotification`通知，一旦收到通知，就会清理内存
<table class="table table-bordered table-striped table-condensed">
    <tr>
        <td>UIApplicationWillterminateNotification </td>
    <td>应用程序将要终止的通知；接收到该通知，清理磁盘</td>
    </tr>
    <tr>
        <td>UIApplicationDidEnterBackgroundNotification </td>
    <td>应用程序进入后台的通知；也会清理磁盘</td>
    </tr>
</table>
#### SDWebImage.h
```objectivec
typedef NS_OPTIONS(NSUInteger, SDWebImageOptions) {
    /**
     * By default, when a URL fail to be downloaded, the URL is blacklisted so the library won't keep trying.
     * 默认情况下，当一个 URL 下载失败，会将该 URL 放在黑名单中，不再尝试下载
     *
     * This flag disable this blacklisting.
     * 此标记取消黑名单
     */
    SDWebImageRetryFailed = 1 << 0,
    
    /**
     * By default, image downloads are started during UI interactions, this flags disable this feature,
     * 默认情况下，在 UI 交互时也会启动图像下载，此标记取消这一特性
     *
     * leading to delayed download on UIScrollView deceleration for instance.
     * 会推迟到滚动视图停止滚动之后再继续下载(这个注释是假的！)
     */
    SDWebImageLowPriority = 1 << 1,
    
    /**
     * This flag disables on-disk caching
     * 此标记取消磁盘缓存，只有内存缓存
     */
    SDWebImageCacheMemoryOnly = 1 << 2,
    
    /**
     * This flag enables progressive download, the image is displayed progressively during download as a browser would do.
     * 此标记允许渐进式下载，就像浏览器中那样，下载过程中，图像会逐步显示出来
     *
     * By default, the image is only displayed once completely downloaded.
     * 默认情况下，图像会在下载完成后一次性显示
     */
    SDWebImageProgressiveDownload = 1 << 3,
    
    /**
     * Even if the image is cached, respect the HTTP response cache control, and refresh the image from remote location if needed.
     * 即使图像被缓存，遵守 HTPP 响应的缓存控制，如果需要，从远程刷新图像
     *
     * The disk caching will be handled by NSURLCache instead of SDWebImage leading to slight performance degradation.
     * 磁盘缓存将由 NSURLCache 处理，而不是 SDWebImage，这会对性能有轻微的影响
     *
     * This option helps deal with images changing behind the same request URL, e.g. Facebook graph api profile pics.
     * 此选项有助于处理同一个请求 URL 的图像发生变化
     *
     * If a cached image is refreshed, the completion block is called once with the cached image and again with the final image.
     * 如果缓存的图像被刷新，会调用一次 completion block，并传递最终的图像
     *
     * Use this flag only if you can't make your URLs static with embeded cache busting parameter.
     * 仅在无法使用嵌入式缓存清理参数确定图像 URL 时，使用此标记
     */
    SDWebImageRefreshCached = 1 << 4,
    
    /**
     * In iOS 4+, continue the download of the image if the app goes to background. This is achieved by asking the system for
     * 在 iOS 4+，当 App 进入后台后仍然会继续下载图像。这是向系统请求额外的后台时间以保证下载请求完成的
     *
     * extra time in background to let the request finish. If the background task expires the operation will be cancelled.
     * 如果后台任务过期，请求将会被取消
     */
    SDWebImageContinueInBackground = 1 << 5,
    
    /**
     * Handles cookies stored in NSHTTPCookieStore by setting
     * 通过设置
     * NSMutableURLRequest.HTTPShouldHandleCookies = YES;
     * 处理保存在 NSHTTPCookieStore 中的 cookies
     */
    SDWebImageHandleCookies = 1 << 6,
    
    /**
     * Enable to allow untrusted SSL ceriticates.
     * 允许不信任的 SSL 证书
     *
     * Useful for testing purposes. Use with caution in production.
     * 可以出于测试目的使用，在正式产品中慎用
     */
    SDWebImageAllowInvalidSSLCertificates = 1 << 7,
    
    /**
     * By default, image are loaded in the order they were queued. This flag move them to
     * 默认情况下，图像会按照在队列中的顺序被加载，此标记会将它们移动到队列前部立即被加载
     *
     * the front of the queue and is loaded immediately instead of waiting for the current queue to be loaded (which
     * 而不是等待当前队列被加载，等待队列加载会需要一段时间
     * could take a while).
     */
    SDWebImageHighPriority = 1 << 8,
    
    /**
     * By default, placeholder images are loaded while the image is loading. This flag will delay the loading
     * 默认情况下，在加载图像时，占位图像已经会被加载。而此标记会延迟加载占位图像，直到图像已经完成加载
     *
     * of the placeholder image until after the image has finished loading.
     */
    SDWebImageDelayPlaceholder = 1 << 9,
    
    /**
     * We usually don't call transformDownloadedImage delegate method on animated images,
     * 通常不会在可动画的图像上调用 transformDownloadedImage 代理方法，因为大多数转换代码会破坏动画文件
     *
     * as most transformation code would mangle it.
     * Use this flag to transform them anyway.
     * 使用此标记尝试转换
     */
    SDWebImageTransformAnimatedImage = 1 << 10,
};
```

