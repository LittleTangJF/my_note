## 背景

JS 也有可能加载失败，导致页面样式错乱，甚至白屏无法使用。

## 一、案例

### 1.1 案例1

出错的原因有以下几种

- 网络不稳定
- 服务器出错
- 跨域问题

可以利用`重试`来解决

#### 如何重试

1. windows监听error
2. 监听的event的type不同，如果是script就是加载错误
3. 维护一个变量对象，保存重试的信息，防止无限重试
4. `document.write()`，这个就会阻塞页面的加载，利用它来写重试

```js
// 全局信息
const retryInfo = {
	[key:url]: {
		times: 0, // 第几次重试从 0 开始  限制次数是域名的长度
		nextIndex: 0, // 重试的域名也从 0 开始
	}
};
//  script 标签，加一个 onerror 事件
window.addEventListener('error', (event) => {})
if (tag.tagName === 'SCRIPT' && !(event instanceof ErrorEvent)) {
	// 重试操作，创建script重试，
	// 因为我们是写在 script 标签里 所以要转译一下，否则会被认为是 script 标签的结束   
	document.write(`<script src="${url.toString()}"></script>`)
}

```

### 1.2 案例2

umijs是如何解决js问题引起白屏问题