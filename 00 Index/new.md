[地址](https://juejin.cn/post/6844903704663949325)
### 关键技术： Object.create(proto,[propertiesObject])、call/apply、 typeof、target

- 新建空对象，对象[proto]链接到构造函数的prototype
- 新的对象会绑定到函数调用this
- 判断如果函数没有返回对象类型
	- 有就返回该新对象
	- 没有就返回新创建的对象
