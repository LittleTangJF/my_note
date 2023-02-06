### 问题
react单向数据流，props向下传递，state组件内部自行管理状态，没有向上回溯的能力
无法让两个组件互相交流

### 解决
需要一个机制，把所有的state集中到组件顶部，然后灵活的将state各取所需分发给所有组件

### 简介
1. 状态管理
2. 将状态存储到一个store
3. store 保存一颗状态树（state tree）
4. 唯一改变state的方法是reducer（dispatch触发一个对应的action，action触发对应的reducer）

### API

1. action
	1. action是个对象，必须有个type参数，定义action的类型
2. reducer
	1. 可以使用一个reducer，也可以将多个reducer合并成一个--combineReducers()
3. store
	1. 使用createStore方法创建
	2. 提供subscribe,dispatch,getState方法

## react-redux

提供了两个

将store直接集成到顶层的props里，
```jsx
<顶层组件 store={store}>
  <App />
</顶层组件>
```

### API
1. Provider：  这个组件的目的是让所有组件都能够访问到Redux中的数据。
2. connect: connect(mapStateToProps, mapDispatchToProps)(MyComponent)
	1. mapStateToProps: **把state映射到props中去**
	2. mapDispatchToProps:**把各种dispatch也变成了props让你可以直接使用**

## redux-thunk

使我们的组件能异步请求

## react-saga

### 产生
如果原始的redux工作流程，产生一个action后会直接触发reducer修改state，reducer又是一个纯函数，也就是不能再reducer中进行异步操作

提供了一些辅助函数

1. takeEvery：**允许多个 fetchData 实例同时启动**，在某个特定时刻，我们可以启动一个新的 fetchData 任务， 尽管之前还有一个或多个 fetchData 尚未结束
2. takeLatest：**在任何时刻 takeLatest 只允许执行一个 fetchData 任务，并且这个任务是最后被启动的那个，如果之前已经有一个任务在执行，那之前的这个任务会自动被取消**

### API

-   take(pattern)： 监听未来的action
-   put(action)： 类似dispatch
-   call(fn, ...args)： **可以调用其他函数的函数**
-   fork(fn, ...args)： **都是用来调用其他函数的，但是fork函数是非阻塞函数**
-   select(selector, ...args)： 指示 middleware调用提供的选择器获取Store上的state数据