
## 关键词

diff 、vdom、jsx、组件本质、fiber、render(reconcile + schedule) + commit(before mutation、mutation、layout)的渲染流程

## VUE

- vue 的 template compiler 是自己实现的 --- vdom
- Object.defineProperty、Proxy [参考](https://juejin.cn/post/7069397770766909476)
	- Object.defineProperty弊端：初始对象里的属性有监听作用，而对新增的属性无效；Vue2中对象新增属性的修改需要使用`Vue.$set`
		- 语法：Object.defineProperty(obj, prop, descriptor) 1、 要添加属性的对象2、 要定义或修改的属性的名称或 [`Symbol`]
	- Proxy：
		- 语法：new Proxy(target, handler)；target目标对象；handler:一个通常以函数作为属性的对象
		- 内部除了get、set之外，还支持has、delete/getOwn/defineProperty\setPrototypeOf等13种拦截
### 原理双向绑定
 `数据劫持` + `发布者-订阅者模式`
- 利用`Proxy`或`Object.defineProperty`生成的`Observer`针对对象/对象的属性进行"劫持"
- 属性发生变化后通知订阅者
- 解析器`Compile`解析模板中的`Directive`(指令)，收集指令所依赖的方法和数据,等待数据变化然后进行渲染
- 1.  `Watcher`属于`Observer`和`Compile`桥梁,它将接收到的`Observer`产生的数据变化,并根据`Compile`提供的指令进行视图渲染,使得数据变化促使视图变化

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


## 面试题

### vue 和react 区别

- 组件化 - jsx 、template
- 虚拟DOM-
	- 减少dom操作
	- 跨平台--对接不同平台渲染逻辑
	- 提升性能--数据变化的时候，生成新的DOM，对比新旧虚拟DOM的差异，将差异更新到真实DOM上
- diff算法
	- 同级比较
	- key做唯一标识
	- tag 变化了，认为是不同
	- vue: Vue2的核心Diff算法采用了双端比较--新的新增，旧的删除，新旧比较更新
	- react: React的Diff算法，两次遍历，第一次找更新的节点，第二次处理剩下的不属于更新的节点（移动、删除、新增）
- 更新策略不同
	- vue： set、get 跟踪依赖关系，不需要更改整个组件树
	- react：组件树就会自顶向下的全diff, 重新render页面
		- shouldcompononetupdate
- 数据驱动视图
	- 双向绑定
	- 单向数据流 setState驱动