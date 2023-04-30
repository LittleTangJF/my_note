http模块可以开启一个http服务器

- createServer : 创建一个 http 实例
- listen :监听 8888 端口
- setHeader : 设置头
- writeHead: 指定头


```js
const http = require('http');
// 创建一个 HTTP 服务器
const server = http.createServer((req, res) => {
    // 处理请求
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello World\n');
});
// 监听端口
server.listen(3000, () => {
   console.log('服务器正在运行，端口为 3000');
});
```

## 工具

- nodemon：监听、检测
- JSON.stringtify() 转json数据
- 

## request

所有的流都是EventEmitter的实例，request也是继承于EventEmitter

- request.url [[node.url]]
- request.method
- 