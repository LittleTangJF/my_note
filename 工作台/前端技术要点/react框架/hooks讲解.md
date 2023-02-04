## hooks链

![[Pasted image 20230204195027.png]]
## useState

与class中使用setState的异同点
1. 相同： 一次渲染周期中调用多次setState，数据只会改变一次
2. 不同： class中setState是合并，而函数组件中setState是替换
知识点：setState是同步还是异步

## useEffect

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

## useMemo

### 语法：
>const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);

**返回一个memoized值**
传递‘创建’函数和依赖项，useMemo只会在其中一个依赖项发生更改时重新计算memoized值

### 应用：

1. 可以对数据进行缓存，依赖项变化会重新计算
2. 优化子组件的渲染，比如传递给子组件的是Object 非基本类型，可以用useMemo
### 注意
>useCallback(fn, deps) 相当于 useMemo(() => fn, deps)

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




