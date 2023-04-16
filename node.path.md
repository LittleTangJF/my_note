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
