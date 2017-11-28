---
layout: post
title: iOS远程真机之OS X EI Captian 编译 libimobiledevice 错误记录以及解决方法！！
date: 2017-07-25
tag: iOS远程真机
---

&#160; &#160; &#160; &#160;[iOS Crash日志获取工具 idevicecrashreport 功能优化](https://testerhome.com/topics/8060)

&#160; &#160; &#160; &#160;使用idevicecrashreport 处理crash报告，下载优化后的[libimobiledevice](https://github.com/baozhida/libimobiledevice/tree/master/src)

&#160; &#160; &#160; &#160;然后重新编译libimobiledevice

### 1、初次尝试

```
libimobiledevice-master xiatian$ ./autogen.sh [--enable-static 静态编译]
.
.
.
.
checking for pkg-config... /usr/local/bin/pkg-config
checking pkg-config is at least version 0.9.0... yes
checking for libusbmuxd... no
configure: error: Package requirements (libusbmuxd >= 1.0.9) were not met:

Package 'libxml-2.0', required by 'libplist', not found

Consider adjusting the PKG_CONFIG_PATH environment variable if you
installed software in a non-standard prefix.

Alternatively, you may set the environment variables libusbmuxd_CFLAGS
and libusbmuxd_LIBS to avoid the need to call pkg-config.
See the pkg-config man page for more details.
```

&#160; &#160; &#160; &#160;非常遗憾，报错了~~

&#160; &#160; &#160; &#160;首先我确定本机是安装了最新版的libxml2，brew查看一下


```
libimobiledevice-master xiatian$  ~ brew list libxml2
/usr/local/Cellar/libxml2/2.9.4/bin/xml2-config
/usr/local/Cellar/libxml2/2.9.4/bin/xmlcatalog
/usr/local/Cellar/libxml2/2.9.4/bin/xmllint
/usr/local/Cellar/libxml2/2.9.4/include/libxml2/ (47 files)
/usr/local/Cellar/libxml2/2.9.4/lib/libxml2.2.dylib
/usr/local/Cellar/libxml2/2.9.4/lib/cmake/libxml2/libxml2-config.cmake
/usr/local/Cellar/libxml2/2.9.4/lib/pkgconfig/libxml-2.0.pc
/usr/local/Cellar/libxml2/2.9.4/lib/ (3 other files)
/usr/local/Cellar/libxml2/2.9.4/share/aclocal/libxml.m4
/usr/local/Cellar/libxml2/2.9.4/share/doc/ (153 files)
/usr/local/Cellar/libxml2/2.9.4/share/gtk-doc/ (55 files)
/usr/local/Cellar/libxml2/2.9.4/share/man/ (4 files)
```

&#160; &#160; &#160; &#160;按照提示设置一下环境变量
```
libimobiledevice-master xiatian$  export PKG_CONFIG_PATH=/usr/local/Cellar/libxml2/2.9.4/lib/pkgconfig/:$PKG_CONFIG_PATH
```
&#160; &#160; &#160; &#160;再次执行命令
```
libimobiledevice-master xiatian$  ./autogen.sh
Configuration for libimobiledevice 1.2.1:
-------------------------------------------

  Install prefix: .........: /usr/local
  Debug code ..............: no
  Python bindings .........: no
  SSL support backend .....: OpenSSL

  Now type 'make' to build libimobiledevice 1.2.1,
  and then 'make install' for installation.
```

### 2、 再次报错

```
libimobiledevice-master xiatian$  make
../src/idevice.h:30:10: fatal error: 'openssl/ssl.h' file not found
#include <openssl/ssl.h>
         ^
1 error generated.
make[2]: *** [debug.lo] Error 1
make[1]: *** [all-recursive] Error 1
make: *** [all] Error 2
```
![这里写图片描述](http://img.blog.csdn.net/20170725153401303?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
&#160; &#160; &#160; &#160;在`~.bash_profile` 加入以下环境变量

```
$ vi ~/.bash_profile
```
&#160; &#160; &#160; &#160;然后添加环境变量
```
export PATH=/usr/local/opt/openssl/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/opt/openssl/lib:$LD_LIBRARY_PATH
export CPATH=/usr/local/opt/openssl/include:$LD_LIBRARY_PATH
```
&#160; &#160; &#160; &#160;保存环境变量

```
$ source ~/.bash_profile

```

### 3、再次执行

```
libimobiledevice-master xiatian$  make
  CCLD     idevicenotificationproxy
  CC       idevicecrashreport-idevicecrashreport.o
  CCLD     idevicecrashreport
Making all in docs
make[2]: Nothing to be done for `all'.
```
&#160; &#160; &#160; &#160;顺利编译

### 4、安装

```
libimobiledevice-master xiatian$ make install
Making install in common
```

### 5、测试一下：
```
libimobiledevice-master xiatian$ ideviceinfo -k DeviceName
xiatian iPhone6
```

&#160; &#160; &#160; &#160;搞定收工！！
 
### 若在make这一步出现如下错误：

![这里写图片描述](http://img.blog.csdn.net/20170725153522967?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveXh5czAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
```
Undefined symbols for architecture x86_64:
  "_ERR_remove_thread_state", referenced from:
      _internal_idevice_deinit in idevice.o
      _idevice_connection_enable_ssl in idevice.o
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
make[2]: *** [libimobiledevice.la] Error 1
make[1]: *** [all-recursive] Error 1
make: *** [all] Error 2
```

&#160; &#160; &#160; &#160;可尝试下面方法：


```
libimobiledevice-master xiatian$ CFLAGS=-I/usr/local/opt/openssl/include LDFLAGS=-L/usr/local/opt/openssl/lib ./autogen.sh [--enable-static 静态编译]
```

&#160; &#160; &#160; &#160;参考文章：

&#160; &#160; &#160; &#160;[OS X EI Captian 编译 libimobiledevice 错误记录以及解决方法~~~](http://www.dllhook.com/post/169.html)

&#160; &#160; &#160; &#160;[macOS-Sierra编译安装libimobiledevice](http://www.akblog.cn/2017/02/11/macOS-Sierra%E7%BC%96%E8%AF%91%E5%AE%89%E8%A3%85libimobiledevice/)