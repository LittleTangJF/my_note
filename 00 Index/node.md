## 关键词

`CommonJS`模块化、.mjs->ESModule 、libuv

## node是什么

Node.js是一个基于v8 JavaScript引擎的JavaScript运行环境（无论是Chrome还是nodejs--v8引擎）；
此外，还有丰富的模块-文件读写、网络IO、加密、压缩解压等

Node.js是使用CommonJS规范的JavaScript运行环境。

tips: 在Node.js中使用ES6模块规范时，必须将文件扩展名设置为.mjs，而不是.js，否则Node.js将无法正确解析import和export语句。

## 核心架构

- [[libuv]]
- [[数据二进制]]
- [[ASCII 码]]

## 模块

- [[node.url]]
- [[node.path]]
- [[node.fs]]
	- - [[stream]]
- [[node.buffer]]
- [[node.crypto]]
- [[node.http]]

## 事件

- [[node.event loop]]
## 相关技术

- [[brew - nginx安装]]
- [[nginx知识要点]]