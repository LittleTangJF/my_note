[参考地址](https://juejin.cn/post/6844903793918738440)
-   解决跨域
-   请求过滤
-   配置gzip
-   负载均衡
-   静态资源服务器

nginx是一个高性能的反向代理服务器

## 反向代理和正向代理

正向代理：客户端通过这个代理，可以突破限制，访问到它本身无法访问到的服务器的资源（翻墙）（提高响应速度，加硬盘，设置缓存）

反向代理：客户端不知道访问的是代理还是目标服务器，作用是隐藏了真正的服务器ip（负载均衡，根据不同服务器负载情况，分发到不同的服务器）
### 反向代理**提供安全保障**

反向代理服务器可以作为应用层防火墙，为网站提供对基于Web的攻击行为（例如DoS/DDoS）的防护，更容易排查恶意软件等。还可以为后端服务器统一提供加密和SSL加速（如SSL终端代理），提供HTTP访问认证等。

## 总结 [参考](https://cloud.tencent.com/developer/article/1418457)
1、**正向代理其实是客户端的代理**，帮助客户端访问其无法访问的服务器资源。**反向代理则是服务器的代理**，帮助服务器做负载均衡，安全防护等。
2、**正向代理一般是客户端架设的**，比如在自己的机器上安装一个代理软件。而**反向代理一般是服务器架设的**，比如在自己的机器集群中部署一个反向代理服务器。
3、**正向代理中，服务器不知道真正的客户端到底是谁**，以为访问自己的就是真实的客户端。而在**反向代理中，客户端不知道真正的服务器是谁**，以为自己访问的就是真实的服务器。
4、正向代理和反向代理的作用和目的不同。**正向代理主要是用来解决访问限制问题。而反向代理则是提供负载均衡、安全防护等作用。二者均能提高访问速度。**

-   `main`:nginx的全局配置，对全局生效。
-   `events`:配置影响nginx服务器或与用户的网络连接。
-   `http`：可以嵌套多个server，配置代理，缓存，日志定义等绝大多数功能和第三方模块的配置。
-   `server`：配置虚拟主机的相关参数，一个http中可以有多个server。
-   `location`：配置请求的路由，以及各种页面的处理情况。
-   `upstream`：配置后端服务器具体地址，负载均衡配置不可或缺的部分。

![[Pasted image 20230220115058.png]]

## 解决跨域

```nginx
location / { proxy_pass dev.server.com; }
```

## 配置gzip

```nginx
    gzip                    on;
    gzip_http_version       1.1;    //这导致HTTP1.0中开启持久链接和使用`GZip`只能二选一
    gzip_comp_level         5;
    gzip_min_length         1000;
    gzip_types text/csv text/xml text/css text/plain text/javascript application/javascript application/x-javascript application/json application/xml;
```

## 负载均衡

通过配置项指定策略
1. **最快响应时间策略**
2. **最小连接数策略**
3. 
4. **轮询策略**
5. **客户端ip绑定**

```nginx
upstream balanceServer {
    server 10.1.22.33:12345;
    server 10.1.22.34:12345;
    server 10.1.22.35:12345;
}
```


## 静态资源服务器

```nginx
location ~* \.(png|gif|jpg|jpeg)$ {
    root    /root/static/;  
    autoindex on;
    access_log  off;
    expires     10h;# 设置过期时间为10小时          
}
```