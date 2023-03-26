## 关键词

seo nuxt next、hydrate

## 1 优缺点
优点
- 对seo友好： 返回html
- 减少了http请求
- 响应快（服务端在内网进行请求）、体验好（客户端渲染**白屏**）、渲染快
缺点
- 服务端压力大：是高并发访问的情况，会大量占用服务端 CPU 资源
## 2 实现原理
虚拟DOM
- 客户端：虚拟 DOM 映射成真实 DOM，完成页面挂载
- 服务端：虚拟 DOM 映射成字符串输出(react.renderToString)

## 3 路由差异

- 客户端：客户端需通过浏览器中的网址，找到路由组件BrowserRouter
- 服务端：通过请求路径，找到路由组件StaticRouter

```JS
<StaticRouter location={req.path} context={context}>
```

## 4 过程

1. 1.  后端拦截路由，根据路径找到需要渲染的`react`页面组件`X`
2. 1.  调用组件`X`初始化时需要请求的接口，同步获取到数据后，使用`react`的`renderToString`方法对组件进行渲染，使其渲染出节点字符串。
3. 1.  后端获取基础`HTML`文件，把渲染出的节点字符串插入到`body`之中，同时也可以操作其中的`title`，`script`等节点。返回完整的`HTML`给客户端。
4. 1.  客户端获取后端返回的`HTML`，展示并加载其中的`JS`，最后完成`react`同构hydrate。ReactDOM.hydrate而不是平时用的 `ReactDOM.render`。
### 4.1 hydrate 注水

- 用于二次渲染（代码执行两次步骤，一次在服务端-html，一次在客户端-事件绑定即接管页面交互）
- 复用原本已经存在的`DOM`节点，减少重新生成节点的开销，**只进行事件处理绑定**。
- `hydrate`主要用于二次渲染服务端渲染的节点，提高首次加载体验

## 5  打包差异

- 需要引入 Node 中的一些核心模块target: 'node',
- webpack-node-externals：第三方模块也是不需要被打包到最终的源码
- isomorphic-style-loader：在对应的 DOM 元素上生成 class 类名，然后返回生成的 CSS 样式代码