# Typora使用图床——以Gitee做图床为例


**Typora 使用 Gitee 图床**

<!--more-->

> 本教程以*`Gitee`*做图床为例

---
---


## 1. 准备软件

### 1.1 安装nodejs (<https://nodejs.org/zh-cn/>)

### 1.2 *`Typora`*里安装**`PiCGo-Core`**命令行版

Typora里，按ctrl＋逗号键 → 图像 → PiCGo-Core(command line) → 下载 （建议使用代理）

![PiCGo-Core(command line)](https://cdn.jsdelivr.net/gh/rentianyu/media@main/img/blog/image-20200804223526238.png)


---
---

## 2. 安装pic-go插件并打开配置文件，也就是执行以下命令

```cmd
# cmd里执行以下两个命令
%APPDATA%\Typora\picgo\win64\picgo.exe install gitee-uploader
%UserProfile%\.picgo\config.json
```

> 最小化打开的窗口，不要关闭

---
---


## 3. 获取*`Gitee`*的用户名、仓库和私人令牌

### 3.1. 注册并登录Gitee  (<https://gitee.com>)，记录用户名

### 3.2. 右上角`+`，新建仓库（建一个公开项目），记录仓库名

### 3.3. [点击创建私人令牌](https://gitee.com/profile/personal_access_tokens/new) ，记录私人令牌的值

---

##  3. 修改配置文件

将以下内容全部复制并替换到第一步里打开的文件，并把第二步生成的值修改为指定值，ctrl+s保存文件退出

```json
{
  "picBed": {
    "uploader": "github", // 代表当前的默认上传图床为 github
    "github": {
      "repo": "rentianyu/media", // 仓库名，格式是 username/reponame
      "token": "ghp_xxxxxxxxxxxxxxxx", // github token
      "path": "img/PicList/", // 自定义存储路径，比如 img/
      "customUrl": "https://cdn.jsdelivr.net/gh/rentianyu/media@main/", // 自定义域名，注意要加 http://或者 https://
      "branch": "main" // 分支名，默认是 main
    }
  },
  "picgoPlugins": {} // 为插件预留
}
```

---
---


## 4. 使用方法

### 4.1 图片直接拖入到Typora里，并右击图片上传

### 4.2 QQ或者微信截图之后，到Typora里粘贴，右击图片上传

![上传图片](https://cdn.jsdelivr.net/gh/rentianyu/media@main/img/blog/image-20200804221430108.png)

---
---


## 5. 本项目说明及手机端图床软件推荐

- PiCGo-Core 不仅支持Gitee还支持GitHub、微博、七牛云、腾讯云COS、又拍云、阿里云OSS、SM.MS、imgur等，具体配置我就不提供了，请自行搜索
- 手机推荐[咕咚云图](https://www.coolapk.com/apk/name.gudong.pic)上传图片做图床，目前支持的图床如下<img src="https://cdn.jsdelivr.net/gh/rentianyu/media@main/img/blog/gudong.png" alt="咕咚云图" style="zoom:50%;" />

---
---

