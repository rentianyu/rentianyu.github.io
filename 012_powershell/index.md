# PowerShell的美化


##  一、说明

​	PowerShell的美化从两方面入手，一是命令行方面，这个安装 [oh-my-posh](https://github.com/JanDeDobbeleer/oh-my-posh) 来解决，另一个就是字体和配色，按照我的设置解决。

​	上个图

![powershell-show](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201112171542446.png)

## 二、`oh-my-posh`的安装与配置

### 2.1 安装 `posh-git` 和 `oh-my-posh` 模块

​	`PowerShell`运行以下命令

```powershell
Install-Module posh-git -Scope CurrentUser
Install-Module oh-my-posh -Scope CurrentUser
```

### 2.2 修改`PowerShell`配置文件

​	`PowerShell`运行以下命令

```powershell
# 如果之前没有配置文件，就新建一个 PowerShell 配置文件
if (!(Test-Path -Path $PROFILE )) { New-Item -Type File -Path $PROFILE -Force }
# 修改配置文件
echo 'Import-Module posh-git 
Import-Module oh-my-posh 
Set-Theme Star
cd ~\Desktop
' > $PROFILE
```

## 三、字体和配色

### 3.1 使用更纱黑体

​	[微软商店](https://www.microsoft.com/store/productId/9MW0M424NCZ7) 或者 [GitHub](https://github.com/be5invis/Sarasa-Gothic) 下载更纱黑体。然后右击`PowerShell`窗口的左上角图标，点击属性，如下图。

​	![powershell-属性](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201112170321990.png)

​	再按下图启用字体。

​	![powershell-字体](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201112170937762.png)

### 3.2 修改背景色

​	如下图修改背景色

​	![powershell-背景色](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201112170716244.png)

​	最好将布局也改一下

​	![powershell-布局](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201112170835550.png)
