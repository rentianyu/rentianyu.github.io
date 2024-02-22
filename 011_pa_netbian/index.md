# 记一次爬取图片的历程


<!--more-->

## 一、前言

​		[彼岸桌面](http://www.netbian.com) 是一个很好的收集壁纸的网站，壁纸高清，我很喜欢，并且还赞助了会员。这次的爬取对象就是它了。

​		这次的流程是先写爬虫脚本，然后放在`VPS`上爬取地址，最后用`COLAB`下载。

## 二、网站分析与确定爬取流程

1.  分析网页网址

    ​	比如，我想爬取 [风景](http://www.netbian.com/fengjing) 类的壁纸，先进入风景专区，然后点击一张图片的地址，发现此时的图片预览图是原图！！！那就可以确定爬取流程了。先以一张图为例。

    1.1 找到图片分类网址

    `http://www.netbian.com/fengjing`

    ![彼岸桌面-风景分类](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201111104928714.png)

    

    1.2 找到图片介绍地址和真实地址

    图片介绍地址：`http://www.netbian.com/desk/23006.htm`

    图片真实地址：`http://img.netbian.com/file/2020/1108/1da1eab002604a8adcc33d8103b5758d.jpg`

    

    ![彼岸桌面-单图](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201111105226256.png)

2.  确定爬取流程

    2.1 风景分类界面获取介绍图片代号

    2.2 图片介绍界面获取图片真实地址



## 三、写脚本

​	以下为获取[风景](http://www.netbian.com/fengjing/index_2.htm)下图片链接的`bash`脚本，第一页的图片请单独处理。

```bash
#!/bin/bash
# 以下代码只处理第2-203页，第一页的图片请自行处理
# 定义种类kind为fengjing
kind=fengjing
# 定义页码page为2 3 .. 203
for page in $(seq 2 203)
do
	# 拼接种类页面链接kind_link
	kind_link="http://www.netbian.com/$kind/index_$page.htm"
	# 获取该页所有图片编号pic_num_list
	pic_num_list=$(wget -qO- $kind_link | grep -aoP "(?<=href=\"/desk/).*?(?=.htm)")
	# 定义图片编号pic_num
	for pic_num in $pic_num_list
	do
		# 拼接图片信息页面链接pic_info_link
        pic_info_link=http://www.netbian.com/desk/$pic_num.htm
        # 获取图片地址pic_link
        pic_link=$(wget -qO- $pic_info_link | grep -aoP -m 1 "http://img.netbian.com/file/20.*jpg(?=\" alt)")
        # 打印图片地址
        echo $pic_link
        # 保存图片地址到文件
        echo $pic_link >> ${kind}_down.txt
    done
done
```

{{< admonition tip "注意"  >}}
- `grep -a`可以查找二进制中的文字
- `grep -m 1`只保留第一次匹配
- 用`wget -qO-`而不用`curl -s`的原因是之后的`grep -m 1`查找到之后会堵塞通道造成错误
{{< /admonition >}}

## 四、下载图片

​	因为完全下载所需的空间需要几G之上，我的`VPS`不足以持，因此就用到了Google家的`COLAB`

1.  将爬取的下载链接上传到 [谷歌网盘](https://drive.google.com) 的某个目录

2.  登录 [COLAB](https://colab.research.google.com) 并新建笔记本，按照下图配置，然后依次运行即可

{{< admonition tip "注意"  >}}
`COLAB` 中 `!`开头表示运行`SHELL`命令
{{< /admonition >}}

```bash
# 挂载谷歌硬盘
from google.colab import drive
drive.mount('/content/drive')
# 安装aria2
!sudo apt install uget aria2

# cd 到文件夹
!cd "/content/drive/Shared drives/1/fj"

!aria2c -i fengjing_down.txt

!zip fengjing.zip *
```

![colab](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201111135330301.png)

## 五、成品及反思

-   成品：[彼岸桌面(http://netbian.com)_风景图片打包.zip](https://file.beita.workers.dev/2:/%E5%85%B6%E4%BB%96%E4%B8%8B%E8%BD%BD%E6%96%87%E4%BB%B6/)

-   此次抓取中，有几点需要注意，

1.  下载网页源码之后可以找到文字，但用`grep`找不到，就是二进制文件的问题，加参数`-a`即可。
2.  `grep`找到多个匹配，加参数`-m `即可只保留第一个。
3.  `curl`和`grep`连用有时会导致通道堵塞，使用`wget -qO-`全下载之后再`grep`即可。
4.  `COLAB`中使用shell命令极大的增加了能力，并且可以挂载谷歌网盘，极大得方便文件的传输。
