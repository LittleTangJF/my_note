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

语法
>const context = useContext(ThemeContext);

使用方法，在顶层创建一个context（createContext），Provider包裹，传递value，子组件useContext可以获取到传入的context值
1. useContext必须是上下文对象本身的参数 useContext(MyContext)

## useReducer

语法:
> const [state, dispatch] = useReducer(reducer, initialArg, init);

useState的替代方案，当你涉及多个子值的复杂state逻辑时

## useCallback
