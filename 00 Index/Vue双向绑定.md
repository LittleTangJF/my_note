## 关键词

Object.defineProperty 、proxy

## 具体过程

1. `new Observer` 对数据进行观测-- this.data
2. Dep 用来收集依赖的 -- 比如message的dep有1个
3. Watcher：订阅者

`Observer`中进行响应式的绑定 --> 触发`get`方法-->执行`Dep`来收集依赖 -- >收集`Watcher`
数据被改的时候---> 触发`set`方法-->notify---->通过Watcher-->去执行更新update--cb(订阅者绑定的更新函数)

![[Pasted image 20230314230022.png]]
## Vue3

`proxy` ，可直接监听对象数组的变化。

前提：1、vue2时更新数组函数劫持的方式，重写了数组方法 2、初始对象里的属性有监听作用，而对新增的属性无效- $set方法解决


