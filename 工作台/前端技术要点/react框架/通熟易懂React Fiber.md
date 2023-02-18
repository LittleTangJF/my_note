
## 渲染过程

### fiber （fiber reconcilder）

![[Pasted image 20230218155943.png]]

### 树形结构的过程（stack reconcilder）栈调度器。react 16前
![[Pasted image 20230218160017.png]]

## Diff策略

1. 第一点：同级比较，在DOM节点中跨层级的操作比较小；如果出现了，则直接将原DOM树删除，重新创建
2. 第二点：改变组件类型，会生成不同的树结构，所以不同类型的结构也是会重新创建
3. 第三点：通过key来标记改节点，保持渲染稳定性，使用唯一key时，同样的节点不会进行更新

## Fiber思想

是react 16引入的新架构，将原本不可中断的更新，改成了异步可中断的更新；将原本一个耗时大任务做了时间分片，拆分成一个个小任务，在浏览器空闲的时间执行；此外，添加了优先级的概念，将一些重要的任务优先执行，比如用户交互响应函数
1. 增加异步可中断操作
2. 增加优先级
3. 大任务分片

将树形结构转化为链表结构

>fiber是一个链表元素对象，有以下的基本属性

1. type：节点类型
2. key：节点key
3. props：节点属性
4. child：第一个子fiber
5. node：对应真实dom
6. base：对应上一次的fiber
7. return：父fiber
8. sibling： 下一个兄弟fiber

### `requestIdleCallback` 判断浏览器是否处于空闲


## Fiber reconcilder 如何工作

js单线程，任务过程，阻塞，所以要任务分片，给其他任务执行机会，线程不会被独占-----数据结构fiber node tree

```jsx
{ tag: TypeOfWork, // 标识 fiber 类型 
type: 'div', // 和 fiber 相关的组件类型 
return: Fiber | null, // 父节点 
child: Fiber | null, // 子节点 
sibling: Fiber | null, // 同级节点 
alternate: Fiber | null, // diff 的变化记录在这个节点上 ... }
```



### 知识点深入

[参考地址](https://cloud.tencent.com/developer/article/1882296)

一个react组件的渲染主要经历两个阶段

1. 调度阶段reconciler： 
	1. 新的数据生产新的树
	2. diff算法，遍历旧的树快速找出要更新/替换的元素，放到更新队列中
	3. 得到新的更新队列
2. 渲染阶段renderer：
	1. 遍历更新的队列，通过调用宿主环境的API，实际更新渲染对应的元素
	2. 宿主环境如DOM、Native等，通常有自己命令式的API，而react就是他上面的一层

Fiber 的主要工作流程：

-   `ReactDOM.render()` 引导 React 启动或调用 `setState()` 的时候开始创建或更新 Fiber 树。
-   从根节点开始遍历 Fiber Node Tree， 并且构建 WokeInProgress Tree（reconciliation 阶段）。
    -   本阶段可以暂停、终止、和重启，会导致 react 相关生命周期重复执行。
    -   React 会生成两棵树，一棵是代表当前状态的 current tree，一棵是待更新的 workInProgress tree。
    -   遍历 current tree，重用或更新 Fiber Node 到 workInProgress tree，workInProgress tree 完成后会替换 current tree。
    -   每更新一个节点，同时生成该节点对应的 Effect List。
    -   为每个节点创建更新任务。
-   将创建的更新任务加入任务队列，等待调度。
    -   调度由 scheduler 模块完成，其核心职责是执行回调。
    -   scheduler 模块实现了跨平台兼容的 requestIdleCallback。
    -   每处理完一个 Fiber Node 的更新，可以中断、挂起，或恢复。
-   根据 Effect List 更新 DOM （commit 阶段）。
    -   React 会遍历 Effect List 将所有变更一次性更新到 DOM 上。
    -   这一阶段的工作会导致用户可见的变化。因此该过程不可中断，必须一直执行直到更新完成。


![[Pasted image 20230218215649.png]]