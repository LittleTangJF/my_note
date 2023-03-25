## 关键词

- pendding、rejected、resolved
- 微任务
- then、catch、Promise.resolve()、Promise.reject()、Promise.all() Promise.any()、Promise.race()
- 链式调用

## 定义

promise是一种异步编程的解决方法,Promise是宏任务（同步执行），只有Promise的回调是异步微任务。解决了异步多层嵌套回调的问题，让代码的可读性更高，更容易维护

## Promise A+规范

1.  Promise 会有三种状态
    -   Pending 等待
    -   Fulfilled 完成
    -   Rejected 失败
- 状态只能由 Pending --> Fulfilled 或者 Pending --> Rejected，且一但发生改变便不可二次修改
- Promise 中使用 resolve 和 reject 两个函数来更改状态

## 实现 [参考](https://juejin.cn/post/6945319439772434469)

## 语法

```jsx
new Promise((resolve,reject) => { resolve（）; reject（）; })
```


## async await

async、await很好的解决了这一点，将异步强行转换为同步处理。 async/await与promise不存在谁代替谁的说法，因为async/await是寄生于Promise，Generater的语法糖。


## 区别

1. promise是ES6，async/await是ES7
2. async/await相对于promise来讲，写法更加优雅
3. async/await既可以用.then又可以用try-catch捕捉
4. promise错误可以通过catch来捕捉，建议尾部捕获错误，