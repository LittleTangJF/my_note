## 关键

同步任务执行结束执行队列中的异步任务、任务挂起

## 定义

执行js代码的时候，遇见同步任务，直接推入调用栈中执行，遇到异步任务，将该任务挂起，等到异步任务有返回之后推入到任务队列中，当调用栈中的所有同步任务全部执行完成，将任务队列中的任务按顺序一个一个的推入并执行，重复执行这一系列的行为。

## 异步任务

- 宏任务： 
	- 定义：：任务队列中的任务称为宏任务，每个宏任务中都包含了一个微任务队列。
	- 宏任务有：script标签内部代码、setTimeout/setInterval、ajax请求、postMessageMessageChannel、setImmediate，I/O（Node.js）
- 微任务
	- 定义：等宏任务中的主要功能都完成后，渲染引擎不急着去执行下一个宏任务，而是执行当前宏任务中的微任务
	- 微任务有：Promise、MutonObserver、Object.observe、process.nextTick（Node.js）

## 加分

浏览器和Node 环境下，microtask 任务队列的执行时机不同 - Node端，microtask 在事件循环的各个阶段之间执行 - 浏览器端，microtask 在事件循环的 macrotask 执行完之后执行