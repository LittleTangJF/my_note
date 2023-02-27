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
- -   **`secure`**： 只能https