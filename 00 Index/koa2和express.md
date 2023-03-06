## 关键词

中间件、路由、es新特性generator、回调地狱

## express

简介：成了路由、视图处理等功能

- express采用callback来处理异步
- express使用callback捕获异常
- connect中间件，线性模型

## koa2

简介：本身不集成任何中间件，需要配合路由、视图等中间件


- koa2采用async/await、generator和async/await
- koa使用try catch捕获异常
- 洋葱模型，所有的请求在经过中间件的时候都会执行两次，能够非常方便的执行一些后置处理逻辑