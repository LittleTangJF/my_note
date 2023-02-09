[参考地址](https://github.com/beichensky/Blog/issues/5)
## hooks链路图

![[Pasted image 20230204195027.png]]
## useState

与class中使用setState的异同点
1. 相同： 一次渲染周期中调用多次setState，数据只会改变一次
2. 不同1： class中setState是合并，而函数组件中setState是替换
3. 不同2: 修改state时，useState设置相同的值不会re-render, 而setState会
知识点：setState是同步还是异步

## useEffect

### 执行生命周期

对于callback回调，react都会像setTimeout一样，将它放到任务队列，等待主任务线程先执行完--- DOM更新，js执行，视图绘制完毕，才执行；所以effect回调函数不会阻塞浏览器绘制视图


1. 第一个是函数的副作用
	1. 1. 返回值也是一个函数，代表组件销毁时被执行
2. 第二个是数组，存放的是第一个函数中使用的某些副作用的属性
	1. 仅运行一次，使用空数组[]

## useContext

### 语法
>const context = useContext(ThemeContext);

使用方法，在顶层创建一个context（createContext），Provider包裹，传递value，子组件useContext可以获取到传入的context值
1. useContext必须是上下文对象本身的参数 useContext(MyContext)

## useReducer

### 语法:
> const [state, dispatch] = useReducer(reducer, initialArg, init);接受类型为 `(state, action) => newState 的reducer`

useState的替代方案，当你涉及多个子值的复杂state逻辑时

### 优化：延迟初始化

第三个参数init，可以惰性地创建初始化状态，初始化状态设置为init(initialArg), 对于重置状态相应操作非常方便

### 与useState的区别

1. 状态结构复杂使用useReducer更有优势
2. useState更新数据是异步的，而useReducer获取的dispatch方法更新数据是同步的

## useCallback

### 语法
>const memoizedCallback = useCallback(() => { doSomething(a, b); }, [a, b]);

传递内联回调和一系列依赖项，useCallback返回一个回忆的memoized，他只会在其中一个依赖项发生改变时才会更改

### 优化

1. 配合使用pureComponent、memo时，可以减少子组件不必要的渲染次数
2. 当传递给子组件function时（父组件重新渲染会，子组件也会变化），可使用useCallback包裹function
### 使用场景

作为其他hooks的依赖时，比如一个接口请求，放在useEffect的依赖项上，会导致无限render，需要用## useCallback包裹

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

## useRef

返回一个可变的ref对象

1. 不仅适用于DOM引用，它是一个通用的容器，其current值是可变的，可以保存任何可变值
2. useRef具有闭包穿透能力
3. current属性不会导致重新渲染

## useLayoutEffect

### 语法
>useLayoutEffect(() => { doSomething });

与useEffect相似都是执行副作用操作，作用是在所有的DOM更新完成后触发，可以用来执行一些与布局相关的副作用，比如获取DOM元素宽高，窗口滚动距离等

>与DOM无关的尽量使用useEffect

## useImperativeHandle

### 语法
>useImperativeHandle(ref, createHandle, [deps])

与class组件不同，函数组件是如何调用子组件的状态或者方法呢？
1. 第一个参数是ref值，可以配合forwardRef使用
2. 第二个参数是一个函数，返回一个对象，对象中的属性都会被挂载到第一个参数的ref上
3. 第三个是依赖项，变化时函数重新执行，重新挂载到ref

## useDebugValue

### 语法
>useDebugValue(value) // or useDebugValue(date, date => date.toDateString());


作用：1、可用于在开发者工具中显示自定义hook的标签 2、延迟格式化 debug 值

## useDefferredValue  （react18）

[地址](https://codesandbox.io/s/usedeferredvalue-3-demo-forked-w2ig5o)
### 问题

解决长列表性能问题

作用：就是 **useDeferredValue** 可以让我们延迟渲染不紧急的部分，延迟的渲染会在紧急的部分先出现在浏览器屏幕以后才开始，并且可中断不会阻塞用户输入

## useId（react18）

### 问题

如果应用是`CSR`（客户端渲染），`id`是稳定的，`App`组件没有问题。

但如果应用是`SSR`（服务端渲染），那么`App.tsx`会经历：

1.  `React`在服务端渲染，生成随机`id`（假设为`0.1234`），这一步叫`dehydrate`（脱水）
2.  `<div id="0.12345">Hello</div>`作为`HTML`传递给客户端，作为首屏内容
3.  `React`在客户端渲染，生成随机`id`（假设为`0.6789`），这一步叫`hydrate`（注水）

客户端、服务端生成的`id`不匹配！

出了useId ， 但背后的原理却很有意思 —— 每个`id`代表该组件在组件树中的层级结构。

## useTransition （react18）
[参考](https://juejin.cn/post/7126481115203780638)
### 语法
>const [isPending, startTransition] = useTransition();

1. isPending 布尔值: 它指示低优先级状态更新是否仍处于挂起状态
2. startTransition函数: 您可以将状态更新包装起来告诉 React这是一个低优先级的更新。

## useInsertionEffect（react18）

### 语法：
>跟useEffect一样

### 解决问题
useInsertionEffect 的执行时机要比 useLayoutEffect 提前，useLayoutEffect 执行的时候 DOM 已经更新了，但是在 useInsertionEffect 的执行的时候，DOM 还没有更新。本质上 useInsertionEffect 主要是解决 CSS-in-JS 在渲染中注入样式的性能问题。

```jsx
import React, {useInsertionEffect } from "react";

const App = () => {
  useInsertionEffect(() => {
    /* 动态创建 style 标签插入到 head 中 */
    const style = document.createElement("style");
    style.innerHTML = `
         .css-in-js{
           color: pink;
           font-size: 12px;
         }
       `;
    console.log("style: " , style);
    document.head.appendChild(style);
  }, []);

  return <div className="css-in-js"> useInsertionEffect使用场景 </div>;
};

export default App;
```

## useSyncExternalStore（react18）
[参考地址](https://juejin.cn/post/7149140019326746654)
### 问题：
当一个 Hooks 返回的数据我们并没有用到时，React 组件仍然会重新渲染。例子：react-router
所以我们订阅许多外部的数据源（react-router， 浏览器的 history，window）来改善应用性能

### 语法
```jsx
function useSyncExternalStore<Snapshot>(
  subscribe: (onStoreChange: () => void) => () => void,
  getSnapshot: () => Snapshot,
  getServerSnapshot?: () => Snapshot
): Snapshot;
```
1. subcribe: 注册回调函数，每当store更改时调用该回调函数
2. getSnapshot： 返回store当前值的函数
3. getServerSnapshot： 返回服务器渲染期间使用的快照的函数

### 解决
```jsx
function useHistorySelector(selector) {
  const history = useHistory();
  return useSyncExternalStore(history.listen, () =>
    selector(history)
  );
}

function CurrentPathname() {
  const pathname = useHistorySelector(
    (history) => history.location.pathname
  );
  return <div>{pathname}</div>;
}

function CurrentHash() {
  const hash = useHistorySelector(
    (history) => history.location.hash
  );
  return <div>{hash}</div>;
}
```

