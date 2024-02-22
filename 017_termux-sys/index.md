# 017_termux Api


**这是一段说明**

<!--more-->

## 一、简介

- 安卓手机自带的Toybox的命令和安卓调试命令能解决一些日常情况下需求，若再装上Busybox，则手机支持的Shell命令就更丰富了。但是这些没有与剪贴板联动的命令，这就造成了极大的局限性。而Termux在Termux-API插件的加持下可以实现丰富的控制安卓的功能，但是只能在Termux内使用，限制了其功能。本篇图文便解决了任意场景使用Termux-API命令的问题。
- 先简单介绍一下Termux-API，安装Termux-API后Termux可以支持很多命令，举几个功能：设置剪贴板内容、获取剪贴板内容、自定义吐司、自定义通知、TTS文字转语音、GPS定位、设置屏幕亮度、开关WiFi、打电话、发短信、拍照、录音等。具体看官方文档吧：
- 官方Termux-API wiki ： https://wiki.termux.com/wiki/Termux:API 

------------------------------------

## 二、Root使用Termux-API命令

- 本节内容提供Root使用Termux-API命令的步骤，请全部看完之后再进行操作，以避免操作到中途发现不满足条件。因机型不同、系统不同，有些手机在非Termux环境中运行Termux-API命令会很慢，有的手机则不支持。

### （一）准备活动
api
1. 安装Termux与Termux-API两个软件并授予两个软件所有权限、自启动权限等

注：Termux及其插件分为Google Play和F-Droid两种版本，版本要统一，不要混用。以下是F-Droid版的下载地址

F-Droid版Termux： https://f-droid.org/packages/com.termux 
F-Droid版Termux-API： https://f-droid.org/packages/com.termux.api 

2. 打开Termux软件（建议科学一下），运行以下命令

```bash
apt update -y && apt install termux-api -y
```

注：至此，Termux内可以使用Termux-API的有关命令

3. Magisk刷入该模块TermuxAPI.zip: https://n802.com/file/18365508-444099897 并重启手机

至此，你可以在任何场景用Root权限使用Termux-API的命令。

### （二）命令介绍

Termux-API支持的命令有很多，我列举几个

● 设置剪贴板为“小贝塔”

termux-clipboard-set "小贝塔"

● 获取剪贴板内容

termux-clipboard-get

● 在屏幕偏下方显示一个黑底的Toast通知，内容为“小贝塔”

termux-toast -g bottom -b black "小贝塔"

还有很多就不一一介绍了，具体看下图

------------------------------------

## 三、Termux-API操作剪贴板的应用命令

这一节主要分享我对Termux-API操作剪贴板的一些应用，主要是靠Xposed edge软件来触发的

1. 获取打开当前界面的Shell命令并设置到剪贴板

termux-clipboard-set "am start -n `dumpsys window|grep mFocusedWindow|grep -o "[^ ]*/[^}]*"`"

2. 剪贴板内容(针对包名/活动名)前加am start -n 并设置到剪贴板

termux-clipboard-set "am start -n `termux-clipboard-get`"

3. 剪贴板内容(针对于URL Scheme)前加am start -d 并设置到剪贴板再执行它

termux-clipboard-set "am start -d `termux-clipboard-get`"&&termux-clipboard-get|bash

4. 剪贴板内容(针对于intent值)，转换为打开的Shell命令并设置到剪贴板

termux-clipboard-set "am start 'intent:`termux-clipboard-get`'"&&termux-clipboard-get|bash

5. 将Xposed edge最后带参数抓取的活动转换为Shell命令并设置到剪贴板

t=`sed -n '$s/.* //p' /data/user_de/0/com.jozein.xedgepro/prefs/collection`;termux-clipboard-set "am start 'intent:$t'"&&termux-clipboard-get|bash

6. (常用)执行剪贴板Shell命令，(Toast会提示执行的内容，执行后剪贴板为命令执行后的文字输出)

termux-toast -g bottom -b black `termux-clipboard-get`;termux-clipboard-set `termux-clipboard-get|bash`

7. 打开剪贴板网址（网址必须要以http或https开头，否则失效，这个可以举一反三，可以指定浏览器打开，我应用集收集了一些，可以参考改一下）

am start -d `termux-clipboard-get`

8. 系统hosts开关（慎用，能看懂的用）

h=/system/etc/hosts
ho=/system/etc/hostsold
if [ ! -f "$h" ]
then
mount -o rw,remount /system&&mv $ho $h&&mount -o ro,remount /system&&termux-toast -g bottom -b black "hosts"
else
mount -o rw,remount /system&&mv $h $ho&&mount -o ro,remount /system&&termux-toast -g bottom -b black "hostsold"
fi

9. 用MX播放器专业版打开剪贴板视频地址

am start -n com.mxtech.videoplayer.pro/.ActivityScreen -d `termux-clipboard-get`

10. 其他

既然与剪贴板联动了，就会有很多的文字操作可以玩了，比如获取剪贴板到文件，设置剪贴板内容为某文件的内容、浏览器搜索剪贴板内容等等。

## 四、致谢

在年前，我就在寻找剪贴板与Shell命令的互动方法，遇到了很多问题，也想过交叉编译一些命令，奈何不会代码，也用过FV悬浮球任务作为中间跳板，但还是有点别扭。之后与我的好朋友@Briefrf 一块想办法解决此类问题，最后我们想到用Termux-API的丰富功能来操作剪贴板是很有操作性的。但还是面临一个问题，就是离开Termux软件就无法操作剪贴板，这极大地限制了应用场景。最后@Briefrf 根据Termux-API的相关内容制作了相关模块一代，其实现方式是将安装在temux里的二进制包和有关文件进行放入`/system/bin/`并进行重定向文件进而实现功能，解决了在其他场景使用Termux-API命令的问题，在此非常感谢@Briefrf 。

注：@Briefrf 已授权我发布此Magisk模块。

最后，预告一下，下一期图文是 任意场景下使用Termux安装的命令 的方法。

#Xposed edge# #高级终端Termux# #Shell命令系列# 
@酷安小编 @八百标兵
