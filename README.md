#节操视频播放器 [![Platform](https://img.shields.io/badge/platform-android-green.svg)](http://developer.android.com/index.html) [![Maven Central](https://img.shields.io/badge/Maven%20Central-1.6-green.svg)](http://search.maven.org/#artifactdetails%7Cfm.jiecao%7Cjiecaovideoplayer%7C1.6%7Caar) [![Licenses](https://img.shields.io/badge/license-MIT-green.svg)](http://choosealicense.com/licenses/mit/) [![GitHub stars](https://img.shields.io/github/stars/lipangit/jiecaovideoplayer.svg?style=social&label=Star)]()

真正实现Android的全屏功能，励志成为Android平台使用最广泛的视频播放控件，GitFlow流程开发develop分支是最新版本

##主要特点
1. 全屏时启动新`Activity`实现播放器真正的全屏功能
2. 可以在加载、暂停、播放等各种状态中正常进入全屏和退出全屏
3. 播放MP3时现实缩略图片
4. 能在`ListView`、`ViewPager`和`ListView`、`ViewPager`和`Fragment`的多重嵌套模式下全屏工作
5. `ListView`的拖拽和`ViewPager`的滑动时如果划出屏幕会自动重置视频
6. 根据自己应用的颜色风格换肤
7. 视频大小的屏幕适配，宽或长至少有两个对边是充满屏幕的，另外两个方向居中

##效果

![Demo Screenshot][1]

视频演示 : http://v.youku.com/v_show/id_XMTQ2NzUwOTcyNA==.html?firsttime=0&from=y1.4-2


##使用
1.引入类库
```gradle
compile 'fm.jiecao:jiecaovideoplayer:1.6'
```

2.添加布局
```xml
<fm.jiecao.jcvideoplayer_lib.JCVideoPlayer
    android:id="@+id/videocontroller1"
    android:layout_width="match_parent"
    android:layout_height="200dp" />
```

3.设置视频地址、缩略图地址、标题
```java
JCVideoPlayer videoController = (JCVideoPlayer) findViewById(R.id.videocontroller);
videoController.setUp("http://2449.vod.myqcloud.com/2449_43b6f696980311e59ed467f22794e792.f20.mp4",
    "http://p.qpic.cn/videoyun/0/2449_43b6f696980311e59ed467f22794e792_1/640",
    "嫂子别摸我");
```
4.在包含播放器的`Fragment`或`Activity`的`onPause()`方法中调用`JCVideoPlayer.releaseAllVideos();`

其他接口

设置皮肤，可以指定某个播放器的皮肤，也可以设置全局皮肤，优先级:某个播放器皮肤>全局皮肤>默认皮肤
```java
JCVideoPlayer.setGlobleSkin();//设置全局皮肤
videoController.setSkin();//设置这一个播放器的皮肤
```

修改缩略图的scalType，默认的缩略图的scaleType是fitCenter，这时候图片如果和屏幕尺寸不同的话左右或上下会有黑边，可以根据客户端需要改成fitXY或这其他模式
```java
JCVideoPlayer.setThumbImageViewScalType(ImageView.ScaleType.FIT_XY);
```

    在ListView和ViewPager中将视频移除屏幕外，会在onDetachedFromWindow时重置视频。
    目标是在库外只需要添加布局，添加配置，其他的问题都在库内判断和操作。

混淆
```
##Eventbus混淆
-keepclassmembers class ** {
    public void onEvent*(***);
}
# Only required if you use AsyncExecutor
-keepclassmembers class * extends de.greenrobot.event.util.ThrowableFailureEvent {
    public <init>(java.lang.Throwable);
}
# Don't warn for missing support classes
-dontwarn de.greenrobot.event.util.*$Support
-dontwarn de.greenrobot.event.util.*$SupportManagerFragment
```

##下载
 * **[jiecaovideoplayer-1.6-demo.apk](https://raw.githubusercontent.com/lipangit/jiecaovideoplayer/develop/downloads/jiecaovideoplayer-1.6-demo.apk)**
 * **[jiecaovideoplayer-1.6.aar](https://raw.githubusercontent.com/lipangit/jiecaovideoplayer/develop/downloads/jiecaovideoplayer-1.6.aar)**
 * **[jiecaovideoplayer-1.6-javadoc.jar](https://raw.githubusercontent.com/lipangit/jiecaovideoplayer/develop/downloads/jiecaovideoplayer-1.6-javadoc.jar)**
 * **[jiecaovideoplayer-1.6-sources.jar](https://raw.githubusercontent.com/lipangit/jiecaovideoplayer/develop/downloads/jiecaovideoplayer-1.6-sources.jar)**

## License

    The MIT License (MIT)
    
    Copyright (c) 2015-2016 jiecao.fm:Nathen
    
    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:
    
    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.
    
    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.


[1]: ./screenshots/j1.png
