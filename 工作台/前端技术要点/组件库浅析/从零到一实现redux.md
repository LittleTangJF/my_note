
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

## 二、combineReducers； ## 合并多个 `reducer` 函数

-   接受一个对象参数，对象的属性值是 `reducer` 函数
    
-   返回一个新的 `reducer` 函数
    
-   调用新的 `reducer` 函数的时候，会依次调用原始的 `reducer` 函数，并将各个属性对应的 `state` 合并到一个 `state` 对象上

```jsx
/**
 * combineReducers 将多个 reducer 合成一个新的 reducer 函数
 * @param {object} reducerTarget 包含多个 reducer 的对象
 */
export function combineReducers(reducerTarget) {
  const finalReducer = {};

  // 将 reducerTarget 中值不是 function 的属性过滤掉
  Object.entries(reducerTarget).forEach(([key, reducer]) => {
    if (typeof reducer === "function") {
      finalReducer[key] = reducer;
    }
  });

  // 返回一个新的 reducer 函数
  return (state = {}, action) => {
    let hasChange = false;

    // 将各个 reducer 对应的 state 值合并到同一个对象中
    let nextState = {};

    // 遍历所有的 reducer
    for (const [key, reducer] of Object.entries(finalReducer)) {
      const prevStateForKey = state[key];

      // 执行 reducer 函数，设置最新的 state 值
      const nextStateForKey = reducer(prevStateForKey, action);
      nextState[key] = nextStateForKey;

      hasChange = hasChange || nextStateForKey !== prevStateForKey;
    }
    return hasChange ? nextState : state;
  };
}
```

## 三、 `applyMiddleware` ： 应用插件


### compose

```js
function compose(...fun){
	if(!fun){
		return
	}
	if(fun.length ===1 ){
		return fun[0]
	}
    return fun.reduce((fn1, fn2)=> (...args)=> fn1(fn2(...args)))
}
```

回到`applyMiddleware`

