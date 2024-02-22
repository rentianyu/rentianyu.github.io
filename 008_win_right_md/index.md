# Windows系统右键增加新建MrakDown和sh


<!--more-->

## 一、保证已安装`Typora`

- [Typora官网](https://typora.io)

## 二、新建`.reg`文件并写入以下内容

```powershell
Windows Registry Editor Version 5.00
[HKEY_CLASSES_ROOT\.md]
@="Typora.exe"
[HKEY_CLASSES_ROOT\.md\ShellNew]
"NullFile"=""
[HKEY_CLASSES_ROOT\Typora.exe]
@="Markdown"

[HKEY_CLASSES_ROOT\.sh]
@="notepad3.exe"
[HKEY_CLASSES_ROOT\.sh\ShellNew]
"NullFile"=""
[HKEY_CLASSES_ROOT\notepad3.exe]
@="sh"
```

## 三、运行以上文件

以下为效果图

![右键添加MarkDown效果图](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201115175922221.png)



>   本文代码源自于[Windows下右键新建.md文件教程](https://stepneverstop.github.io/win-rightclick-create-md.html)
