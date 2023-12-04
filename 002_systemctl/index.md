# Linux 进程守护之 systemctl


# Linux 进程管理之 systemctl

## 0.介绍

`systemctl`是systemd的主命令，用于管理系统。

现在只介绍`systemctl`的进程守护`service`功能，首先编写配置文件，然后启用并重载配置。最后开启一下服务。

---

## 1.编写配置文件

- 以下以`bot.service`为配置文件，守护`/usr/bin/python3 /root/bot/main.py`命令运行为例

- 在`/etc/systemd/system/`目录下编写以`.service`结尾的配置文件

```bash
# 在/etc/systemd/system/目录下编写 bot.service 配置文件
echo '
[Unit]
Description=bot    # 服务名称描述
After=network.target sshd-keygen.service  # 在什么服务启动之后运行

[Service]
User=root    # 用户
WorkingDirectory=/root/bot    # 工作目录
ExecStart=/usr/bin/python3 /root/bot/main.py  # 命令
ExecStop=/bin/kill -HUP $MAINPID
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure    # 什么情况下重启服务
RestartSec=10s    # 重启时间间隔

[Install]
WantedBy=multi-user.target  # 实现开机启动
' > /etc/systemd/system/bot.service
```

---

## 2.启用并重载配置

```bash
systemctl enable bot       # 这个主要是设置成系统自启动
systemctl daemon-reload    # 重载所有修改过的配置文件
```

---

## 3.启动服务

```bash
systemctl start bot    # 启动服务
```

---

## 4.修改配置文件后操作

- 配置文件没问题的话，前三步就可以运行起一个守护服务，如果要修改配置文件的话，需要以下操作

```bash
vim /etc/systemd/system/bot.service  # 修改配置文件（用别的软件也可）
systemctl daemon-reload              # 重载所有配置文件
systemctl restart bot                # 重启服务
```

---

## 5.`systemctl`用法汇总

```bash
systemctl start bot      # 启动
systemctl stop bot       # 停止
systemctl restart bot    # 重启
systemctl status bot     # 查看运行状态
systemctl cat bot        # 查看配置文件的内容
systemctl enabled bot    # 启用
systemctl disabled bot   # 禁用
systemctl daemon-reload  # 重载所有修改过的配置文件
systemctl reload bot     # 重载 bot.service 的配置文件

# 以下是不常用命令
systemctl is-active bot  # 显示 bot.service 是否正在运行
systemctl is-failed bot  # 显示 bot.service 是否处于启动失败状态
systemctl is-enabled bot # 显示 bot.service 是否建立了启动链接
systemctl show bot       # 显示 bot.service 的所有底层参数
systemctl show -p ExecStart bot # 显示 bot.service 的指定属性的值
systemctl set-property bot User=root # 设置 bot.service 的指定属性
```



<div>
<div style="padding: 10px 0; margin: 20px auto; width: 100%; font-size:16px; text-align: center;">
<h5>「感谢支持」</h5>
<button id="rewardButton" disable="enable" onclick="var qr = document.getElementById('QR'); if (qr.style.display === 'none') {qr.style.display='block';} else {qr.style.display='none'}">
<span>赞赏</span></button>
<div id="QR" style="display: none;">
<div id="wechat" style="display: inline-block">
<a class="fancybox" rel="group">
<img id="wechat_qr" src="../wx.png" alt="WeChat Pay"></a>
<h3>微信赞赏</h3>
</div>
<div id="alipay" style="display: inline-block">
<a class="fancybox" rel="group">
<img id="alipay_qr" src="../zfb.png" alt="Alipay"></a>
<h3>支付宝赞赏</h3>
</div>
</div>
</div>


