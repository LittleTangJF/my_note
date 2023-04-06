## Proxy

```javascript
var proxy = new Proxy(target, handler);
```

- get/set
- has
- **deleteProperty**
- **ownKeys**
- **defineProperty**
- **apply**
- **construct**

一共13种拦截操作

## Reflect

为了方便操作对象而提供的API 

- defineProperty  无法定义属性是，返回false，而不是抛出异常
- 从命令式--> 函数式  has、deleteProperty
- `Reflect`对象的方法与`Proxy`对象的方法一一对应
- 方便地调用对应的`Reflect`方法，完成默认行
- 有了`Reflect`对象以后，很多操作会更易读

## 使用场景

通常都是proxy和reflect一起使用
[三种](https://juejin.cn/post/7153284017511464974)
- **数据绑定与观察者模式** ：vue2和vue3中使用比如vue3 的proxy和reflect
- **可以写函数参数验证**，js动态语言，没有静态校验功能
- **简便的构造函数**--以前写的calss 要写很多重复代码比如construct

### 问题：为什么proxy要使用Reflect？

Proxy因为要保证正确的this上下文指向，所以需要配合Reflect使用。

### 问题： 那么为什么必须要使用Reflect？

- 命令式编程-->函数式编程
- 操作对象出现报错返回 false---Reflect.defineProperty  更符合if判断的实际写法 （不会因为报错而中断正常的代码逻辑执行）
- Proxy上所有的方法在Reflect上都有一对一的实现--比如**ownKeys**


