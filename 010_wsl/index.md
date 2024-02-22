# WSL (微软Linux子系统) 的安装与使用




## 一、`WSL`的介绍

1.  `WSL`是什么：运行在win系统下的Linux子系统
2.  `WSL`的版本：版本有两种，`WSL`一代 和`WSL`二代，相比一代而言，二代运行于虚拟机上，更接近于真实的Linux系统
3.  来个截图
-   ![WSL-neofetch](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201107115626669.png)



## 二、`WSL` 的安装

-   以下安装方法为个人总结，有关详细信息和注意问题，请阅读微软官方文档：[适用于 Linux 的 Windows 子系统安装指南 (Windows 10)](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10)
-   `WSL`两个版本的区别，可以阅读有关 [比较WSL2 和WSL1](https://docs.microsoft.com/zh-cn/windows/wsl/compare-versions) 的详细信息。

### （一）安装`WSL`一代

1.  启用`WSL`功能

    以管理员身份打开 PowerShell 并运行：

    ```powershell
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```

2.  去微软商店搜索`Linux`，安装自己适用的系统

![Linux](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201107120334792.png)

3.  重启win系统即可安装完成



### （二）安装`WSL`二代

1.  启用 `WSL`功能和虚拟机功能

    以管理员身份打开 PowerShell 并运行：

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

2.  重启win系统

3.  安装Linux内核更新包

    下载并安装最新包：[适用于 x64 计算机的 WSL2 Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

4.  将 `WSL 2` 设置为默认版本

    以管理员身份打开 PowerShell 并运行：

```powershell
wsl --set-default-version 2
```

5.  在微软商店搜索`Linux`，安装自己适用的系统

6.  重启win系统



## 三、优化建议

​	此为我自己的优化，仅供参考。

### （一）安装`Windows Terminal`来美化终端

1.  在微软商店搜索`Windows Terminal`并安装
2.  其他详细信息请阅读 [安装 Windows 终端](https://docs.microsoft.com/zh-cn/windows/terminal/get-started)

![Windows Terminal](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201107122055798.png)



### （二）设置默认用户为root

1.  先获取已安装的子系统名称和版本

    以管理员身份打开 PowerShell 并运行：

```powershell
wsl -l -v
```

![wsl信息](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201108170133354.png)

​	`NAME`对应的值便是已安装的子系统名称

​	`VERSION`是对应系统的`WSL`版本

2.  设置默认用户为root

    以管理员身份打开 PowerShell 并运行：

```powershell
ubuntu config --default-user root
```

{{< admonition tip "注意"  >}}
上述命令中，`ubuntu`是第一步中获取的`NAME`值
{{< /admonition >}}

### （三）`WSL 1`和`WSL 2`版本的无缝转换

1.  先获取已安装的子系统名称和版本

    以管理员身份打开 PowerShell 并运行：

```powershell
wsl -l -v
```

![wsl信息](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201108171658356.png)

​	`NAME`对应的值便是已安装的子系统名称

​	`VERSION`是对应系统的`WSL`版本

2.  设置对应系统的版本

```powershell
wsl --set-version ubuntu 2
```
![wsl版本转换](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201108170750853.png)

{{< admonition tip "注意"  >}}
上述命令中，是以我的`Ubuntu`系统为例，把`WSL`版本换为二代，两版本转换的前提是`WSL 2`版本环境已正确配置 {{< /admonition >}}


## 四、有关文章

1.  `WSL`的安装：[适用于 Linux 的 Windows 子系统安装指南 (Windows 10)](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10)
2.  有关比较 `WSL 2` 和` WSL 1` 的详细信息：[比较 WSL 2 和 WSL 1](https://docs.microsoft.com/zh-cn/windows/wsl/compare-versions) 
3.  设置`WSL`普通用户账号密码：[为新的 Linux 分发版创建用户帐户和密码](https://docs.microsoft.com/zh-cn/windows/wsl/user-support)
4.  安装`Windows Terminal`：[安装 Windows 终端](https://docs.microsoft.com/zh-cn/windows/terminal/get-started)
5.  `WSL`有关命令：[适用于 Linux 的 Windows 子系统的命令参考](https://docs.microsoft.com/zh-cn/windows/wsl/reference)


