[参考地址](https://blog.csdn.net/weixin_41850404/article/details/93509600)
### 安装

```js
brew install php@[version]
```

### 配置文件

```js
/usr/local/etc/php/
```
### 启动PHP-FPM

```js
sudo php-fpm -D  或者  brew services start php72(php版本号)
```

停止PHP-FPM

```js
sudo kill -INT cat /usr/local/var/run/php-fpm.pid
```

重启PHP-FPM

```js
sudo kill -USR2 cat /usr/local/var/run/php-fpm.pid
```

