# 提取软件界面Shell命令




<!--more-->

## 前言

此篇文章是关于找开启软件某些界面shell命令的教程。先说几点东西

1. 下文提到的依心所言是 [**酷安 @ l14789**](http://www.coolapk.com/u/768442)

2. 以下教程中提到的文件皆可在 [QQ群](https://jq.qq.com/?_wv=1027&k=LCtkXOpt) `773276432` 下载，或者在其链接中下载



## 一、Activity软件抓

​	此方法比较简单，安装 [Activity](https://www.coolapk.com/apk/l.Activity) 软件，授予剪贴板权限、无障碍权限（如有root，直接一键激活）等权限，然后正常运行到要提取的界面，观察活动名，正确的话点一下悬浮窗提取所需要的的`包名/活动名` 到剪贴板。然后用以下命令拼接可得到所需命令

```bash
am start -n 包名/活动名
```

注意：

1. 如果提取到的含有特殊符号（比如$）,把`包名/活动名`用英文的引号引起来，单、双引号都可，我称之为`引号原则`。

2. 如果`活动名`中含有`包名`，可删去`活动名`中的`包名`（强迫症福音）。

```bash
am start -n '包名/活动名'
am start -n "包名/活动名"
```

{{< bilibili BV1bD4y1X7T7 >}}



## 二、xposed edge pro抓

​	这个比较简单，思路就是利用xposed edge pro的`应用菜单`抓取，再处理其数据就得到命令

1. 设置好edge手势（别的也可）触发`应用菜单`

2. 到要抓的界面调出`应用菜单`-`活动`-`带参数提取活动`

3. 以文本方式打开`/data/user_de/0/com.jozein.xedgepro/prefs/collection`找到最后一行

4. 以空格为界，最后一项为操作的值

5. 如果该值符合`包名/活动名`的特点，就按 `am start -n 包名/活动名`处理即可，   

   否则按如下处理即可得到命令

```bash
am start 'intent:值'
或
am start "intent:值"
```

{{< bilibili BV1Ri4y1c7sb >}}



## 三、抓取桌面图标

这个直接用依心所言的写的shell脚本即可

1. 下载依心所言的脚本：[提取Shortcut与桌面启动器(引号可选版)7.3.sh](https://n802.com/f/18365508-480188501-5d83dc)（访问密码：1234）
2. 发送快捷方式到桌面
3. 运行脚本（可使用[MT管理器]()、FV悬浮球、常规脚本）
4. 查找`/sdcard/A2020/`下文件中的命令

{{< bilibili BV1RA411L7u9 >}}



## 四、抓取系统设置

这个直接用依心所言的写的shell脚本即可

1. 下载依心所言的脚本：[提取系统设置开关命令7.0版[依心所言与小贝塔].sh](https://n802.com/f/18365508-476139177-5207da)（访问密码：1234）
2. 执行一次脚本
3. 改变一次设置开关状态
4. 然后再执行一次脚本
5. 接着查看抓到的信息

{{< bilibili BV1Yf4y1e7Zt >}}



## 五、URL scheme

这个命令的模板有两个

```bash
# 打开 URL scheme 命令 短版
am start -d 'URL Scheme'
或
am start -d "URL Scheme"

# 打开 URL scheme 命令 长版
am start -a android.intent.action.VIEW -d 'URL Scheme'
或
am start -a android.intent.action.VIEW -d "URL Scheme"
```

这个比较麻烦，我就写两种吧

1. 网页中找

   1.1 找可以打开软件的网址

   1.2 特定网址查找

   1.3 网址源码中查找

   1.4 网页`js`中查找

2. 反编译软件碰运气（这里使用MT做演示）

   3.1 打开一个软件包

   3.2 反编译打开软件包根目录下的`AndroidManifest.xml`并搜索`scheme`或者`schema`来确定该软件支持的协议头

3. 有关文章

- [入门 iOS 自动化：读懂 URL Schemes](https://sspai.com/post/44591)

- [URL Schemes 使用详解](https://sspai.com/post/31500)


{{< bilibili BV18i4y1T7zV>}}



## 六、edge联合termux-api一键抓取

这个需要安装termux以及termux-api，并且把termux有关命令安装进系统才行

## 后记

1. 关于双开软件没有介绍，只简单提一句`am start --user 999 `，可以在终端输入`am`查看使用方法.
2. 关于我注明的使用的他人脚本，我（小贝塔）已经取得脚本作者允许这样使用，其他人使用请联系脚本作者。
3. 本教程文章所有权归本人 [小贝塔](https://xiaobeita.vercel.app) 所有，本文仅供学习交流，未经本人许可，严禁用于商业用途，转载请注明出处。
