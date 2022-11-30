## token放在cookies里

前端可以完全不写代码，设置 cookie 可以依赖后端的 `Set-Cookie` 响应头，同域名的情况下发送所有请求的时候cookie 也是自动带上的

### 安全性

cookie 可以设置 `HttpOnly` 来保护 cookie 无法被 JS 代码捕获，避免 XSS 等攻击，还可以设置 `Secure` 来确保只在 https 环境下传输 token；

问题： cookie 会存在 CSRF 攻击的问题

### 优点

网页中img也会自动带上 cookie，好处是便于控制网络图片的访问权限

### 缺陷

如果网页中的背景图、icon 等资源图片放在相同的域名下，每次请求这些资源图片都会带上 cookie，很浪费带宽和服务器的流量， 所以 CDN 的域名一定要和主域名区分开。

##  token 放在请求头里，用 Authorization

JS 代码来给请求方法添加全局拦截器，因此它天生具备防止 CSRF 的功能
 
前端将 token 持久存储，一般会存储在 LocalStorage 里面，此时存在 XSS 攻击盗取 token 的问题（将 LocalStorage 里的 token 加密可以一定程度上避免此问题），而且它是无法跨域互通的，即使两个网站的一级域名相同也无法互通；

