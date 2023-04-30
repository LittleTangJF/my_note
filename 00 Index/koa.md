
## 核心


- 轻量
- 更好的处理异步
- 中间件

## 使用


```js
const Koa = require('koa');
const app = new Koa();

app.use(async (ctx, next) => {
    ctx.body = 'Hello World';
});

app.listen(3000);
```


## 中间件


所有的信息放到ctx内

1. ctx.requst、ctx.req
2. koa-router
3. ctx.respose、ctx.res
4. multer: 文件上传
5. ctx.respose.end
6. ctx.body、ctx.query


## 路由


```js
// 创建
const Router = require('koa-router');
const router = new Router({prefix?});
// 使用
router.get('/', async (ctx, next) => {
    // `ctx.query`中对查询参数进行了缓存，这样可以避免每次访问查询参数时都要重新解析查询字符串。
    const query = ctx.query();
    //ctx.body你不需要手动设置响应头的Content-Type属性，Koa会自动根据内容类型设置它。
    ctx.body = 'Hello World';
});

// 生效
app.use(router.routes());
app.use(router.allowedMethods()); // 返回405 Method Not Allowed
```