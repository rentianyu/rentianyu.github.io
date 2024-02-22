# curl命令实现坚果云上传下载


**使用curl实现坚果云上传下载坚果云，命令适用于webdav、ftp等**

<!--more-->


> - 1.txt ---- 代表本地文件
> - https://dav.jianguoyun.com/dav/ ---- 坚果云根目录
> - 示例代码是根目录下新建的test目录
> - user:pass ---- 邮箱:应用密码
> - 应用密码获取：登录坚果云 → 账户信息 → 安全选项 → 第三方应用管理 → 添加应用
> - 本命令全部没有输出

## 1. 上传文件

```shell
# 单文件版
curl -s -u 'user:pass' -T '1.txt' 'https://dav.jianguoyun.com/dav/test/'

# 当前目录文件
for i in $(ls)
do 
curl -s -u 'user:pass' -T "$i" 'https://dav.jianguoyun.com/dav/test/'
done
```

## 2. 下载文件

```shell
# 单文件版
curl -s -u 'user:pass' 'https://dav.jianguoyun.com/dav/test/1.txt' -o '1.txt'

# 单目录版
for i in $( curl -s -u 'user:pass' 'https://dav.jianguoyun.com/dav/test/' -X PROPFIND | grep -o 'name>[^<]*'| grep -o '[^>]*$' )
do
curl -s -u 'user:pass' "https://dav.jianguoyun.com/dav/test/$i" -o $i
done
```

## 3. 删除文件

```shell
curl -s -u 'user:pass' 'https://dav.jianguoyun.com/dav/test/1.txt'  -X DELETE
```
## 4. 列出当前目录文件夹及文件

```shell
curl -s -u 'user:pass' 'https://dav.jianguoyun.com/dav/test/' -X PROPFIND | grep -o 'name>[^<]*'| grep -o '[^>]*$'
```

