# 017_zsh与Oh-My-Zsh的简单配置


<!--more-->

# 017_ZSH与Oh-My-Zsh的配置

```bash
# 安装 zsh
apt install zsh

# 无人值守安装 Oh-My-Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
# 设置默认shell为zsh
whoami | grep root && chsh -s $(which zsh) || chsh -s zsh

# 克隆插件
# zsh-autosuggestions
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
# zsh-syntax-highlighting 
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
# ys 主题
sed -i 's/ZSH_THEME=.*/ZSH_THEME="ys"/' ~/.zshrc
# 启用插件
sed -i 's/plugins=.*/plugins=(extract z zsh-autosuggestions zsh-syntax-highlighting)/' ~/.zshrc
# extract  解压文件用的，所有的压缩文件，都可以直接 x filename


# 编辑ZSH配置文件
vim ~/.zshrc
# 查看主题
ls ~/.oh-my-zsh/themes
# 更新配置
source ~/.zshrc
# 更新omz
omz update
# 卸载omz
uninstall_oh_my_zsh

```

> [ohmyzsh官网](https://github.com/ohmyzsh/ohmyzsh)


