
## 渲染过程

### fiber

![[Pasted image 20230218155943.png]]

### 树形结构的过程
![[Pasted image 20230218160017.png]]

## Diff策略

1. 第一点：同级比较，在DOM节点中跨层级的操作比较小；如果出现了，则直接将原DOM树删除，重新创建
2. 第二点：改变组件类型，会生成不同的树结构，所以不同类型的结构也是会重新创建
3. 第三点：通过key来标记改节点，保持渲染稳定性，使用唯一key时，同样的节点不会进行更新

## Fiber思想

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

### 初始化

