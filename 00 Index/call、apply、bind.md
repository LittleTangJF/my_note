[地址](https://juejin.cn/post/6844903496253177863)
### 关键： this永远指向最后执行他的对象、settimeout是内置函数，this永远指向window

### 如何改变this指向？
- 箭头函数
- call、apply、 bind
- new
- _this = this

1. call: fun.call(thisArg[, arg1[, arg2[, ...]]])
2. apply: fun.apply(thisArg, [argsArray]) ,  thisArg--null 或 undefined 时会自动指向全局对象
3. bind: function.bind(thisArg[, arg1[, arg2[, ...]]])，方法创建一个新的函数, 当被调用时，将其this关键字设置为提供的值