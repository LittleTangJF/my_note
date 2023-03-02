## 解读

window.onhashchange` `history.pushState ` `window.onpopstate

## HashRouter

监听location对象hash值变化事件来实现
- hashurl有'#'号
- 通过`window.onhashchange`方法获取新URL中hash值
- 需要兼容低版本的浏览器时，建议使用hash模式

## HistoryRouter

利用浏览历史记录栈的API实现

- history的url没有'#'号
- history会触发添加到浏览器历史记录栈
- history需要后端配合，如果后端不配合刷新新页面会出现404
	- #后面的hash值不会带入请求URL中，所以服务器觉得Hash模式下的URL是不变的
	- 需要后端设置路由永远返回首页
- `history.pushState `使用它做页面跳转不会触发页面刷新
- 使用`window.onpopstate` 监听浏览器的前进和后退

