## useMemo

### 语法：
>const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

**返回一个memoized值**
传递‘创建’函数和依赖项，useMemo只会在其中一个依赖项发生更改时重新计算memoized值

### 应用：

1. 需要进行大量或者复杂运算时，为了提高性能，可以使用 `useMemo` 进行数据缓存
2. 优化子组件的渲染，比如传递给子组件的是Object 非基本类型，可以用useMemo
### 注意

`useMemo` 和 `useCallback` 的区别

-   `useMemo` 的返回值是一个值，可以是属性，可以是函数（包括组件）
-   `useCallback` 的返回值只能是函数

因此，`useMemo` 一定程度上可以替代 `useCallback`，等价条件：`useCallback(fn, deps) => useMemo(() => fn, deps)`

## useCallback

### 语法
>const memoizedCallback = useCallback(() => { doSomething(a, b); }, [a, b]);

传递内联回调和一系列依赖项，useCallback返回一个回忆的memoized，他只会在其中一个依赖项发生改变时才会更改

### 优化

1. 配合使用pureComponent、memo时，可以减少子组件不必要的渲染次数
2. 当传递给子组件function时（父组件重新渲染会，子组件也会变化），可使用useCallback包裹function
### 使用场景

作为其他hooks的依赖时，比如一个接口请求，放在useEffect的依赖项上，会导致无限render，需要用## useCallback包裹


## React.memo

 React 贴心的提供了 `React.memo` 这个 HOC（**高阶组件**），与 **PureComponent** 很相似，但是是专门给 Function Component 提供的，