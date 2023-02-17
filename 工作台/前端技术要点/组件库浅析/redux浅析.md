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

1. action(描述更新对象)
	1. action是个对象，必须有个type参数，定义action的类型
	2. 使用： store.dispatch(action), 将action传给store
2. reducer
	1. 可以使用一个reducer，也可以将多个reducer合并成一个--combineReducers()
	2. 使用：接受两个参数state， action（dispatch传过来的对象）
3. store
	1. 使用createStore(reducer)方法创建
	2. 提供subscribe,dispatch,getState方法

### 其他方法

 #### combineReducers高阶函数
 合并reducer
 ```jsx
 const reducer = combineReducers({
  count: counterReducer,
  todos: todoReducer
});

```

#### applyMiddleware
应用插件，用来扩展redux的功能

例如
	需要异步执行才能完成才进行state更新的操作，可以使用rendx-thunk插件
```jsx
import thunk from "redux-thunk";
// ...

// 应用插件
const ehancer = applyMiddleware(thunk, logger);

// 创建 store
const store = createStore(reducer, ehancer);

export default store;

```

#### ActionCreator: action 创建函数

是一种思想和实现，通过调用一个函数生成一个对应的action

#### bindActionCreators

个函数是将 `dispatch` 绑定到了 `actionCreator` 方法上，之后只要我们执行 `actionCreator` 就会触发 `store` 更新了，不用每次都 `dispacth` 了。

```jsx
// 生成包装后的 actionCreator，执行之后就会触发 store 数据的更新
const { increment, decrement, getAsyncTodos, addTodo } = bindActionCreators(
  actionCreators,
  store.dispatch
);
```

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

### 用法
```jsx
// createStore的时候传入thunk中间件 const store = createStore(rootReducer, applyMiddleware(thunk));
```

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

## redux-toolkit

[文档](https://juejin.cn/post/7101688098781659172#heading-4)

redux官方推荐的工具，简化了redux的流程，**React Toolkit** 使得编写好的 Redux 应用程序以及加快开发速度变得更加容易。