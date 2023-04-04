## 关键词

增强hooks

## 1 [useCreation](https://codesandbox.io/s/virtuallist-jc663l?file=/src/ahooks/useCreation/index.ts:430-439)
	-`Object.is` 不会做类型转换。判断两个值是否相同；这与===运算符也不一样，三等会-0=+0
	
## 2 [useReactive](https://codesandbox.io/s/virtuallist-jc663l?file=/src/ahooks/useReactive/index.ts:689-698)
- Proxy去代理，Reflect反射去驱动数据
- useUpdate更新组件


[实现链接](https://codesandbox.io/s/virtuallist-jc663l?file=/src/ahooks/index.ts)
[参考链接](https://juejin.cn/post/7121551701731409934)