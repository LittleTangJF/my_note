## 客户端

### 语法
```js
// 的值由 `name=value` 对组成，以 `;` 分隔。每一个都是独立的 cookie
document.cookie = "user=John"
```
### 可选属性

- -   **`path=/mypath`**
- -   **`domain=site.com`**
- [expires，max-age](https://zh.javascript.info/cookie#expiresmaxage)
- -   **`secure`**：cookie 是基于域的，它们不区分协议。如果加上secure就 只能https
- samesite：防止 CSRF（跨网站请求伪造）攻击
- httpOnly: 选项禁止任何 JavaScript 访问 cookie

## 服务端设置

服务器使用响应 `Set-Cookie` HTTP-header 设置的。

```JS
res.setHeader('Set-Cookie', 'isVisit=true;domain=.yourdomain.com;path=/;max-age=1000');
```