## 关键词

高阶组件、复用组件、设计模式、加工强化组件、强化Props、性能优化、条件渲染、**公共化**

## 1 写法

- 装饰器写法 （class）
- 包裹写法（func）

## 2 常用场景

### 2.1 强化props

- 混入props
- 抽离state控制更新

### 2.2 条件渲染

- 懒加载
- 路由懒加载

### 2.3 性能优化

- re-render 
- 切片渲染
- 
### 2.4 事件赋能

- 埋点、

### 2.5 反向继承

- 劫持渲染
- 劫持生命周期
-高阶组件应该是**无副作用的纯函数**,所以不要在`render`中使用，且谨慎修改原型链

[项目地址](https://codesandbox.io/s/virtuallist-jc663l?file=/src/Hoc%E8%B7%AF%E7%94%B1%E6%87%92%E5%8A%A0%E8%BD%BD/index.tsx)

[参考链接](https://juejin.cn/post/7103345085089054727#heading-9)