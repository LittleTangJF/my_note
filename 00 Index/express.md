## 前言

>created by TJ

使用express需要学习以下几个知识点

- 中间件
- 路由
- 错误处理

## 中间件


中间件的本质是传入express的一个回调函数

具体可以做什么？

- res、req的更改
- 结束请求、结束响应周期-->end|json
- 调用栈中的下一个中间件-->next

使用use

```js
app.use((req,res,next)=>{}) // 最普通的中间件
```

多个中间件

```js
app.get(path?, (req,res,next)=>{}, (res,req,next)=>{})
```

express常用中间件

E = express

1. res. json(): 解析数据
2. E.urlencoded({extend: true}): 解析
3. morgan: 日志中间件
4. multer: 文件上传
5. req.query、req.params


## 路由


express.Router()

主要作用

1. 路由的module


## 静态资源服务器


express.static(__path)

## 错误处理


```js
next(err?)
app.use(err=>{
	 
})
```

## 和koa的区别


next是不返回的promise，是不符合洋葱模型的