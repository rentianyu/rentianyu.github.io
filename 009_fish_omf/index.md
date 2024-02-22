# Fish Shell 的简单使用和Oh-my-fish主题的展示


<!--more-->

## 一、FIsh 的安装与简单配置

-   介绍：ArchLinux 上的 [fish 简体中文](https://wiki.archlinux.org/index.php/Fish_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
-   安装

```bash
apt install fish
```

-   设置为默认shell

```bash
# 完整的Linux系统请使用fish真实路径
chsh -s $(which fish)

# termux设为默认shell
chsh -s fish
```

-   去除欢迎语

```bash
fish -c "set -U fish_greeting"
```

-   定义一些命令到Fish配置文件

```bash
mkdir -p ~/.config/fish

# fish 的配置文件
cat > ~/.config/fish/config.fish <<EOF
alias apti='apt -y install'
alias aptr='apt -y remove'
alias apts='apt search'
alias aa='apt update -y ; apt upgrade -y ; apt autoremove -y'
alias lsa='ls -a'
alias ..='cd ..; ls -a'
alias ll='ls -al'
alias gitc='git clone'
alias gitp='git add . ; git commit -m auto-push ; git push ; echo push成功'
alias myip='curl ifconfig.me'
EOF
```

-   Fish的简单语法

```fish
# 定义变量
set t 123    # 相当于bash的 t=123

# 括号内执行
grep 1 (ls)    # 相当于bash的 grep 1 $(ls)
```

-   `if`语句。

>   ```fish
>   if grep fish /etc/shells
>       echo Found fish
>   else if grep bash /etc/shells
>       echo Found bash
>   else
>       echo Got nothing
>   end
>   ```

-   `switch`语句。

>   ```fish
>   switch (uname)
>   case Linux
>       echo Hi Tux!
>   case Darwin
>       echo Hi Hexley!
>   case FreeBSD NetBSD DragonFly
>       echo Hi Beastie!
>   case '*'
>       echo Hi, stranger!
>   end
>   ```

-   `while`循环。

>   ```fish
>   while true
>       echo "Loop forever"
>   end
>   ```

-   `for`循环。

>   ```fish
>   for file in *.txt
>       cp $file $file.bak
>   end
>   ```

-   Fish 的函数用来封装命令，或者为现有的命令起别名。

>   ```fish
>   function ll
>       ls -lhG $argv
>   end
>   ```

上面代码定义了一个`ll`函数。命令行执行这个函数以后，就可以用`ll`命令替代`ls -lhG`。其中，变量`$argv`表示函数的参数。

下面是另一个例子。

>   ```fish
>   function ls
>       command ls -hG $argv
>   end
>   ```

>   以上引用于阮一峰的 [Fish shell 入门教程](http://www.ruanyifeng.com/blog/2017/05/fish_shell.html)



## 二、Oh-my-fish 的安装与简单用法

-   介绍：[Oh-my-fish 官方中文文档](https://github.com/oh-my-fish/oh-my-fish/tree/master/docs/zh-CN)
-   安装

```bash
curl -L https://get.oh-my.fish | fish
```

-   简单使用

```fish
# 列出已安装的和可安装的主题
omf theme
# 安装 ays 主题
omf install ays
# 更换主题为已安装的 cbjohnson 主题
omf theme cbjohnson
# 检查 omf 是否有错误
omf doctor
# 卸载 omf
omf destroy
```

{{< admonition tip "注意"  >}}
文章最下方有所有主题的截图，完全是手工截图，真的是累啊
{{< /admonition >}}

## 三、Fish 与 Oh-my-fish 的卸载与清理配置文件

{{< admonition tip "注意"  >}}
卸载 `Fish`之前建议先卸载 `Oh-my-fish`{{< /admonition >}}

-   完全卸载`Oh-my-fish`

```fish
# fish 环境下运行以下命令
omf destroy
rm -r (find ~ -name omf)
```

-   完全卸载`fish`

{{< admonition tip "注意"  >}}
卸载 `Fish`之前一定要修改当前默认shell不是fish {{< /admonition >}}

```bash
# 修改默认终端为bash
chsh -s $(which bash)    # Linux 系统
chsh -s bash             # Termux

# 完全卸载fish
# bash 环境下运行
apt purge -y fish
apt autoremove
rm -r $(find ~ -name fish)
```



## 四、Oh-my-fish 的所有主题截图

{{< admonition tip "注意"  >}}
以下是在WSL的Ubuntu20 下的效果，如果你也是，但凡我标注了`Error`的主题，请不要尝试
{{< /admonition >}}

-   我之前用的是`ays`主题，现在用的是`numist`主题

### 1 agnoster

+ ![agnoster](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201104225326041.png)
### 2 aight
+ ![aight](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201104225733557.png)
### 3 ays
+ ![ays](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201104225837458.png)
### 4 barracuda（termux专用）
+ ![barracuda](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201104230006188.png)
### 5 batman
+ ![batman](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105101656281.png)
### 6 beloglazov
+ ![beloglazov](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105101800049.png)
### 7 bira
+ ![bira](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105101841892.png)
### 8 bobthefish
+ ![bobthefish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105101922909.png)
### 9 bongnoster
+ ![bongnoster](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105102018047.png)
### 10 boxfish
+ ![boxfish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105102122508.png)
### 11 budspencer
+ ![budspencer](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105111228079.png)
### 12 cbjohnson
+ ![cbjohnson](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105114702600.png)
### 13 chain
+ ![chain](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105114808620.png)
### 14 clearance
+ ![clearance](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105114915383.png)
### 15 cmorrell
+ ![cmorrell](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105114956353.png)
### 16 coffeeandcode
+ ![coffeeandcode](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105115130366.png)
### 17 cor (emoji-clock Error)
+ 无
### 18 cyan (math: Error)
+ ![cyan](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105115719566.png)
### 19 dangerous ( [I] 提示)
+ ![dangerous](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105120300589.png)
### 20 default
+ ![default](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105121600036.png)
### 21 dmorrell
+ ![dmorrell](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105121640503.png)
### 22 doughsay
+ ![doughsay](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105121732784.png)
### 23 eclm
+ ![eclm](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105121814268.png)
### 24 edan
+ ![edan](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105121856890.png)
### 25 eden
+ ![eden](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105122040115.png)
### 26 emoji-powerline
+ ![emoji-powerline](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105122346033.png)
### 27 es
+ ![es](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105122426476.png)
### 28 fishbone
+ ![fishbone](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105122933273.png)
### 29 fishface
+ ![fishface](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125026283.png)
### 30 fishy-drupal
+ ![fishy-drupal](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125123438.png)
### 31 fisk
+ ![fisk](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125202846.png)
### 32 flash
+ ![flash](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125242785.png)
### 33 fox
+ ![fox](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125332753.png)
### 34 gentoo
+ ![gentoo](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125552404.png)
### 35 gianu
+ ![gianu](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125638369.png)
### 36 gitstatus
+ ![gitstatus](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125719389.png)
### 37 gnuykeaj
+ ![gnuykeaj](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125754433.png)
### 38 godfather
+ ![godfather](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125830343.png)
### 39 graystatus
+ ![graystatus](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105125911664.png)
### 40 harleen
+ ![harleen](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130008061.png)
### 41 idan
+ ![idan](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130109701.png)
### 42 integral
+ ![integral](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130155957.png)
### 43 jacaetevha
+ ![jacaetevha](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130246626.png)
### 44 johanson
+ ![johanson](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130332372.png)

### 45 kawasaki

+ ![kawasaki](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130412888.png)
### 46 krisleech
+ ![krisleech](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130450636.png)
### 47 l
+ ![l](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130526541.png)
### 48 lambda

+ ![lambda](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130615217.png)
### 49 lavender
+ ![lavender](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105130653384.png)

### 50 lolfish

+ ![lolfish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105182028294.png)

### 51 mars

+ ![mars](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105182125815.png)
### 52 mish

+ ![mish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105182233084.png)

### 53 mokou

+ ![mokou](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105182321281.png)

### 54 mtahmed

+ ![mtahmed](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105182417277.png)
### 55 nai
+ ![nai](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105131743505.png)
### 56 nelsonjchen
+ ![nelsonjchen](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105131827401.png)
### 57 neolambda
+ ![neolambda](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105131911614.png)

### 58 numist

+ ![numist](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105132003592.png)
### 59 ocean
+ ![ocean](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105132050849.png)
### 60 one
+ ![one](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105132145334.png)
### 61 pastfish
+ ![pastfish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105132233029.png)
### 62 perryh
+ ![perryh](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105132307685.png)
### 63 pie (Error)
+ ![image-20201105132424126](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105132424126.png)
### 64 plain (Error)
+ 无
### 65 pure
+ ![pure](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135142869.png)
### 66 pygmalion
+ ![pygmalion](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135237394.png)
### 67 random
+ 随机主题
### 68 randomrussel
+ ![randomrussel](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135411235.png)
### 69 redfish
+ ![redfish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135456945.png)
### 70 red-snapper
+ ![red-snapper](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135535867.png)
### 71 rider
+ ![rider](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135613195.png)
### 72 robbyrussell
+ ![robbyrussell](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135714997.png)
### 73 sashimi
+ ![sashimi](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135748723.png)
### 74 scorphish
+ ![scorphish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135830835.png)
### 75 separation
+ ![separation](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135910653.png)
### 76 shellder
+ ![shellder](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105135941856.png)
### 77 simple-ass-prompt
+ ![simple-ass-prompt](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140019391.png)
### 78 simplevi
+ ![simplevi](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140106754.png)
### 79 slacker
+ ![slacker](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140142812.png)
### 80 slavic-cat
+ ![slavic-cat](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140218777.png)

### 81 solarfish

+ ![solarfish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140329202.png)
### 82 spacefish
+ ![spacefish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140405923.png)
### 83 sushi
+ ![sushi](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140447245.png)
### 84 syl20bnr
+ ![syl20bnr](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140619004.png)
### 85 taktoa
+ ![taktoa](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140710721.png)
### 86 technopagan (moonmoji Error)
+ 无
### 87 toaster
+ ![toaster](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140852257.png)
### 88 tomita
+ ![tomita](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105140948212.png)
### 89 trout (有点慢，需要安装rbenv)
+ ![trout](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141240911.png)
### 90 tweetjay
+ ![tweetjay](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141425123.png)
### 91 uggedal
+ ![uggedal](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141536723.png)
### 92 will
+ ![will](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141623356.png)
### 93 wolf-theme
+ ![wolf-theme](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141738021.png)
### 94 yimmy

+ ![yimmy](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141812505.png)
### 95 zeit
+ ![zeit](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141849079.png)
### 96 zephyr
+ ![zephyr](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105141926877.png)
### 97 zish
+ ![zish](https://gitee.com/xiao_beita/tuchuang/raw/master/img/image-20201105142005719.png)

