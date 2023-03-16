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