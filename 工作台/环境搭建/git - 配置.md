# mac端配置

## 环境搭建


**1.生成ssh-key**

```bash
// 升级 macos 后出现bug 使用以下命令
ssh-keygen -t ed25519  -C "18681268108@163.com"

ssh-keygen -o -t rsa -b 4096 -C "18681268108@163.com"
```

**2.查看key位置**

```bash
cd ~/.ssh
cat id_rsa.pub
pbcopy < ~/.ssh/id_rsa.pub  // 复制
```

**3.测试是否连接**

```bash
ssh -T git@github.com
```


## 常用命令


1. 对比差异

```json
git fetch
git diff --stat --color remotes/main/master..origin/master // 对比本地和远程分支
git diff <masterbranch_path> <remotebranch_path> // 对比两个远程分支diff
```

