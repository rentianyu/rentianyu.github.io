# Linux定时任务之crontab

# Linux定时任务之crontab

## 1. `crontab`一般用法，`crontab –e`

```bash
# 重启cron服务
service cron restart

# 编辑定时任务（重启cron服务才会生效）
crontab –e

# 重启cron服务,这可能重启一个就行，不放心的话都执行
service cron restart
systemctl restart cron

# 列出定时任务
crontab –l

# 配置文件解读及示例
# minute hour day month week command
#  分    时   日   月    周   命令

# 举例如下
# 实在不会，记得是看Crontab表达式：https://www.toolnb.com/tools/croncreate.html
* * * * * sh /root/hello.sh  # 每1分钟执行 sh /root/hello.s
*/10 * * * * sh /root/hello.sh  # 每10分钟
* */2 * * * sh /root/hello.sh  # 每2小时
0 8 * * * sh /root/hello.sh  # 每天8点0分
0 8,9,10 * * * sh /root/hello.sh  # 每天8、9、10点
0 8-10 * * * sh /root/hello.sh  # 每天8、9、10点
0 8-20/3 * * * sh /root/hello.sh  # 每天8-20点中，每3小时执行一次
# 特殊的：开机触发
@reboot sh /root/hello.sh  # 开机执行

```

---

## 2. `crontab`高级用法，`crontab 配置文件`

- `crontab -e` 其实是生成了个配置文件，我们也可以创建一个 `crontab`配置文件
- 这个配置文件，简单来说是个脚本，可以设置 `shebang`、环境变量、指定用户，不过这几个都可不写
- 允许一些简单的 `shell`语法
- 举例一下配置文件，前两行可以不要

```
#!/bin/env bash
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 开机触发
@reboot wx "PVE 开机了！"

# PVE
#5 8 * * * qm start 101
58 23 * * * /usr/sbin/shutdown -h now
56 23 * * * /usr/sbin/qm list | grep -q "101.*running" && /usr/sbin/qm shutdown 101
54 23 * * * /usr/sbin/qm list | grep -q "102.*running" && /usr/sbin/qm suspend 102 --todisk

# 更新ydns
10 * * * * bash /root/sh/ydns.sh > /dev/null

# 更新crontab
30 8 * * * /usr/bin/crontab ~/sh/cron.list && /usr/sbin/service cron restart && /usr/bin/systemctl restart cron


```

- 使用方法：

  - ```bash
     # 设置配置文件
    crontab ~/sh/cron.list
    
    # 重启cron服务,这可能重启一个就行，不放心的话都执行
    service cron restart
    systemctl restart cron
    ```

---

## 3. 一些坑

1. 一般来讲，`crontab`的前边时间的表达式就只有5位，除非你懂，否则别整花里胡哨的
2. 如果没有导入环境变量(`export PATH`)，一些命令就要用绝对路径，比如：`/usr/sbin/service cron restart`
3. 修改完配置文件后一定要重启一下服务
4. 有一些系统抽风，按常规方法改了也不生效，就得去改动 `cron`相关的底层文件

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

