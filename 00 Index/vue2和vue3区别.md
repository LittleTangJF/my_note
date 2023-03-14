## 关键词

`Object.defineProperty`、 反射和代理（Reflect， Proxy）、ref、DSL、composition API


## 过程

- reactive
- runtime
- compiler
	- parse
	- transform
	- generate

## [diff算法](https://juejin.cn/post/7010594233253888013)

### vue2

- -   同级比较
- -   比较标签名
- -   比较key 
- 双端比较
	- 头头
	- 尾尾
	- 头尾
	- 尾头
	- 
### vue3

- 事件缓存 - 变成静态 --cache = func 
- 静态标记 + 非全量diff  
	- PatchFlags  -1
- 静态复用
	- 把不参与更新的元素保存，之后一直复用 -1
- 最长递增子序列
	- 头头
	- 尾尾
	- 拿数组下标 拿到最递增长子序列 [2,3,4]
	- 然后剩余的节点基于子序列进行移动新增删除