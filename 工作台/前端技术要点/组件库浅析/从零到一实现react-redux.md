
## 核心API

包含以下核心 `API`

-   `Provider`: 上下文组件
-   `connect`: 带参的高阶函数
-   `useSelector`: 获取需要的 `state` 数据
-   `useDispatch`: 获取 `dispatch`

## 一、Provider

作用： 将store对象下发到多层级的组件中

1. 创建context
```jsx
const StoreContext = React.createContext();
```
2. 创建Provider组件
```jsx
/**
 * Provider 组件，用来传递 Context 中数据，进行跨层级组件通信
 */
const Provider = ({ store, children }) => (
  // 将 store 作为 value 传递下去
  <StoreContext.Provider value={store}>{children}</StoreContext.Provider>
);
```
## 二、connect高阶函数

用来连接当前组件和store

1. 订阅监听事件， state发生变化，更新组件
2. 将state，dispatch，merge合并到组件props中
3. -   `API`：`connect([mapStateToProps],[mapDispatchToProps],[mergeProps],[options])`

### mapStateToProps （返回纯对象）

1. -   `(state[, ownProps]) => ({ count: state.count, todoList: state.todos })`
### mapDispatchToProps（返回纯对象）

### mergeProps

如果指定了这个参数，`mapStateToProps()`与 `mapDispatchToProps()`的执行结果和组件自身的 `props` 将传入到这个回调函数中。
1. -   `mergeProps(stateProps, dispatchProps, ownProps): props`

### 总结源码

```jsx
/**
 * connect 函数，源码中包含四个参数，我们这里只用到这些，所以就暂时只实现了前三个参数
 *
 * @param {*} mapStateToProps 将 state 合并到组件的 props 中的函数
 * @param {*} mapDispatchToProps 将 actionCreator 合并到组件的 props 中的函数
 * @param {*} mergeProps 自定义属性合并到组件的 props
 */
const connect = (
  mapStateToProps,
  mapDispatchToProps,
  mergeProps
) => WrapperComponent => {
  return props => {
    const { getState, dispatch, subscribe } = useContext(StoreContext);
    const [, forceUpdate] = useReducer(x => x + 1, []);
    // 执行 mapStateToProps，获取用户需要的 state 数据
    const stateProps = mapStateToProps(getState());
    // 默认将 dispatch 挂载到 props 上
    let dispatchProps = { dispatch };

    // 判断 mapDispatchToProps 是函数还是对象，函数的话，执行获取返回的对象
    if (typeof mapDispatchToProps === "function") {
      dispatchProps = mapDispatchToProps(dispatch);
    } else if (mapDispatchToProps === "object") {
      // 对象的话，直接将对象中的 actionCreator 使用 dispatch 进行包装
      dispatchProps = bindActionCreators(mapDispatchToProps, dispatch);
    }

    mergeProps = mergeProps(stateProps, dispatchProps, props);

    useEffect(() => {
      // 添加事件订阅，state 发生变化时会触发，更新组件
      const unsubscribe = subscribe(() => forceUpdate());
      return () => {
        unsubscribe();
      };
    }, [subscribe]);

    return (
      <WrapperComponent
        {...props}
        {...stateProps}
        {...dispatchProps}
        {...mergeProps}
      />
    );
  };
};
```