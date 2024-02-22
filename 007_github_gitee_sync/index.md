# GitHub与Gitee同步本地推送


<!--more-->

>   本文摘自于[Git 多远程仓库管理：GitHub 与 Gitee 双向同步](https://p3terx.com/archives/git-multi-remote-repository-management.html)，详细用法请前往查看

## 一、主仓库和镜像仓库

>   两仓库可同时控制

```bash
# 获取本地仓库已关联仓库
git remote -v

# 添加另一个远程仓库到 oring
git remote set-url --add origin git@github.com:rentianyu/action.git
```

## 二、分别拉取和推送

>   两仓库分别控制

```bash
# 添加 GitHub 远程仓库并命名为 github
git remote add github git@github.com:rentianyu/action.git

# 推送 GitHub 仓库
git push github mster

# 推送原仓库
git push # 或者 git push origin mster
```
