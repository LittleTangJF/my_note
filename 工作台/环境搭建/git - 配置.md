# mac端配置

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
```

**3.测试是否连接**

```bash
ssh -T git@github.com
```
