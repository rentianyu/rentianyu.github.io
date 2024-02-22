# 激活 Windows 和 Office


<!--more-->

##  一、kms激活Windows系统，(推荐)

### 1.1 数字激活`Windows 10`

- 下载 [云萌 Windows 10 激活工具](https://cmwtat.cloudmoe.com) 激活

> 参考网址：[CMWTAT_Digital_Edition](https://github.com/TGSAN/CMWTAT_Digital_Edition)

### 1.2 `kms`激活`Windows`系统

```cmd
# 以管理员权限的CMD或PowerShell运行以下命令
slmgr /skms kms.v0v.bid
slmgr /ato
```

> 参考网址：[Windows系统一句命令激活](https://v0v.bid/kms.html)

## 二、激活`Office`

- 只适用于默认安装位置的64位版本的2010、2013、2016、2019、365版本

```cmd
# 以管理员权限的CMD或PowerShell运行以下命令
cd "C:\Program Files\Microsoft Office\Office*"
cscript ospp.vbs /sethst:kms.v0v.bid
cscript ospp.vbs /act
```

> 参考网址：[Windows系统一句命令激活](https://v0v.bid/kms.html)
>
> 激活脚本：便捷KMS一键激活脚本 [点击下载](https://v0v.bid/kmspro.zip) （解压密码：`https://v0v.bid` ）
>
> ​				或我提供的官方副本（免解压）：[kmspro.bat](/images/kmspro.bat)
>
> 安装`Office`：[Office Tool Plus](https://otp.landian.vip)


