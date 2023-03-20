## 关键词

`CommonJS`模块化、.mjs->ESModule

## 1. url

url模块可以用于处理url和file协议

- url模块可以用于解析url

### 1.1 Parse和format

- parse：将url.parse转换为对象格式
- format: 使用 url.format 同样可以将其转换为url字符串

### 1.2 fileURLToPath和 pathToFileURL

- fileURLToPath：file协议 转换为系统路径格式
- pathToFileURL： 统路径格式转换为 file协议

## 2 path

path模块可以用于处理文件路径
### 关键词
__filename、__dirname

- __dirname： 表示当前正在执行的脚本的目录
- __filename： 表示当前正在执行的脚本的文件名

```js
// CommonJS 直接用
console.log(__dirname); // C:\Users\33153\Desktop\hello

// ESModule
const __filename = url.fileURLToPath(import.meta.url);
const __dirname = path.resolve();
```

- join： 用于连接路径
- resolve：将 **to** 参数解析为绝对路径, 给定的路径的序列是从右往左被处理的,会把 **/** 或 **\** 开头的字符串片段解析成**根目录**
- basename： 返回路径的最后一部分
- dirname：	返回路径的父级目录部分
- extname：返回路径中文件的后缀名
- parse、format

## 3 fs

fs模块可以用于操作系统文件，fs模块的API都分为同步和异步的(带`Sync`后缀的是同步), 而异步的回调函数的参数node统一约定了**第一个参数为错误对象**