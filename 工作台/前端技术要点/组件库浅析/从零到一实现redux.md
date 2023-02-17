
## 核心方法：

1. createStore： 创建store
2. combineReducers： 合并reducer
3. applyMiddleware： 应用插件
4. bindActionCreators： 将一个actionCreator组成的对象转换成dispatch组成的对象


## 一、createStore

特性：
1. reducer参数
2. ehancer应用中间件之后的增强型函数
返回store对象
1. getState
2. dispatch
3. subscribe

```jsx
/**
 * 创建 store 对象
 * @param {function} reducer reducer 更新函数
 * @param {*} prevState 进行服务端渲染时传入的已有的 state 数据（这里我们没有用到，暂时没做处理）
 * @param {function} ehancer 插件应用结果
 */
export function createStore(reducer, prevState, ehancer) {
  // 做一次兼容，可能第二个参数传递的就是 插件应用结果
  if (typeof prevState === "function") {
    ehancer = prevState;
  }

  // 如果 ehancer 确实传入的是一个函数，则在 ehancer 函数中执行 store 的创建
  if (typeof ehancer === "function") {
    return ehancer(createStore)(reducer);
  }

  // 当前 state 数据
  let currentState;

  // 存放订阅监听对象的数组
  let listeners = [];

  // 获取当前 state 数据
  function getState() {
    return currentState;
  }

  /**
   * 订阅 state 数据变化
   * @param {function} listener 订阅监听对象
   */
  function subscribe(listener) {
    const index = listeners.length;
    listeners.push(listener);

    // unsubscribe
    return () => listeners.splice(index, 1);
  }

  /**
   * 派发 action，触发 reducer 更新 state
   * @param {plain object} action
   */
  function dispatch(action) {
    currentState = reducer(currentState, action);
    listeners.forEach(listener => listener());
  }

  // 率先执行一次 dispatch，用来为 state 设置初始值
  dispatch({ type: Math.random() });

  return {
    getState,
    subscribe,
    dispatch
  };
}
```

## 二、combineReducers

6. 


