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

## reacte-redux

提供了两个

将store直接集成到顶层的props里，
```jsx
<顶层组件 store={store}>
  <App />
</顶层组件>
```

### API
1. Provider：  这个组件的目的是让所有组件都能够访问到Redux中的数据。
2. connect: 
	1. connect(mapStateToProps, mapDispatchToProps)(MyComponent)