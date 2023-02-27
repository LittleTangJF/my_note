
## 关键词

diff 、vdom、jsx、组件本质、fiber、render(reconcile + schedule) + commit(before mutation、mutation、layout)的渲染流程

## VUE

- vue 的 template compiler 是自己实现的 --- vdom
- Object.defineProperty、Proxy
	- Object.defineProperty弊端：初始对象里的属性有监听作用，而对新增的属性无效；Vue2中对象新增属性的修改需要使用`Vue.$set`
		- 语法：Object.defineProperty(obj, prop, descriptor) 1、 要添加属性的对象2、 要定义或修改的属性的名称或 [`Symbol`]
	- Proxy


## react [参考](https://juejin.cn/post/7117051812540055588)

-  react 的 jsx 的编译器是 babel 实现的 --- vdom
-  setState 的 api 触发状态更新
- fiber 架构
	- 可打断，有优先级
	- render和commit阶段
		- reconcile（打增删改的标记）是可以打断的，由schdule调度
		- commit的不可以打断，把有 effectTag 的 fiber 都放到了 effectList 队列中，遍历更新即可。


## 组件

对产生 vdom 的逻辑的封装，函数的形式、option 对象的形式、class 的形式