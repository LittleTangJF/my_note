## 关键词

render、 reconcile、schdule、commit、silbing、 return

## 过程

### reconcile
- 一个 workLoop 循环，每次循环做一个 `fiber` 的 `reconcile`，当前处理的 `fiber` 会放在 `workInProgress` 这个全局变量上
- 每个 `fiber` 的 `reconcile` 是根据类型来做的不同处理。处理完了当前 `fiber` 节点，就把 `wip` 指向 `sibling`、`return` 来切到下个 `fiber` 节点
- 当循环完了，也就是 `wip` 为空了，那就执行 `commit` 阶段，把 `reconcile` 的结果更新到 `dom`。
可打断reconcile
- `shouldYiled` 方法：循环处理前每次判断下是否打断来实现的

### commit

-  reconcile 的时候把有 effectTag 的节点收集到一个队列里队列叫做 `effectList`
- 会在 `commit` 阶段遍历 `effectList`，根据 `effectTag` 来增删改 `dom`
