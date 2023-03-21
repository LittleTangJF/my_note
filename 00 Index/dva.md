## 关键词

Reducers、dispatch、action、Effects

## 1  mdoel

- namespace： 名称
- state
- action： 描述对象
- dispatch：触发action
- Reducer：用于描述如何改变state，通过 actions 中传入的值，与当前 reducers 中的值进行运算获得新的值（也就是新的 state）。
- Effect：处理异步操作 -- generator yield
- Subscription

## 2 connect

connect 是一个函数，绑定 State 到 View。

## 3 内部处理函数

- put：用于触发 action
- call：用于调用异步逻辑，支持 promise 。
- select：用于从 state 里获取数据