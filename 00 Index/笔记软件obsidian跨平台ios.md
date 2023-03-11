采用github为公共的仓库，免费

[参考网址](https://zhuanlan.zhihu.com/p/565028534)

## 过程中遇到问题

### 错误一

链接github失败 报错 `kex_exchange_identification: Connection closed by remote host`
 
解决方法：`vim ~/.ssh/config` 输入

```JS
Host github.com
Hostname ssh.github.com
Port 443
User git
```

设置后检验
```JS
$ ssh -T git@github.com
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```
### 错误二

拉取git pull 失败 卡在 resolving  deltas 阶段

参考[issue 943](https://github.com/ish-app/ish/issues/943)j解决

```JS
git config --global pack.threads 1
```
