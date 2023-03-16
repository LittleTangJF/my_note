## 关联

Object.defineProperty、Object.getPrototypeOf(obj)

## for in

### 语法

> FOR IN 迭代一个对象 **除symbol以外**的可枚举属性 包括**继承**的


- JS中的对象类型包括Object，Array，Function，Date，Math....

## for of

for of是ES6新出的一个用于遍历可迭代对象（实现了[`Iterator`](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FSymbol%2Fiterator "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol/iterator")接口）的语法-

- **语句**在[可迭代对象](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FIteration_protocols "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols")（包括 [`Array`](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array")，[`Map`](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FMap "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Map")，[`Set`](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FSet "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set")，[`String`](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FString "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String")，[`TypedArray`](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FTypedArray "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/TypedArray")，[arguments](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FFunctions%2Farguments "https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/arguments") 对象等等）

对于`for...of`的循环，可以由 `break`, `throw` 或 `return` 终止

## 区别

- `for in遍历的是数组元素key，而且`for of`遍历的只是数组内的元素
- `for of`适用遍历数/数组对象/字符串/`map`/`set`等拥有迭代器对象
- 对于普通的对象，`for...of`结构不能直接使用，会报错，必须部署了 Iterator 接口后才能使用。