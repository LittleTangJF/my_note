在 Node.js 中，Stream（流）是一种处理数据的抽象概念，用于读取或写入连续的数据块（比如文件、网络数据等），而不是一次性读取整个数据。它类似于管道（pipe）的概念，可以将数据流分成多个块（chunks）依次处理，从而避免一次性读取大量数据造成的内存浪费和性能瓶颈。Stream 可以理解为是一种流式传输数据的方式。

在 Node.js 中，Stream 模块提供了基础的 Stream 类以及多种

- 可读流（Readable）、
- 可写流（Writable）、
- 双工流（Duplex）：socket
- 和转换流（Transform）等，

可以用来处理各种类型的数据。通过使用 Stream，可以有效地处理大文件、网络数据传输等场景，并且具有较好的性能和灵活性。Stream 还支持管道操作，可以将多个 Stream 串联起来，实现复杂的数据处理功能。

- [ ] 在nodejs中Request和Response对象都是基于流实现

```js
const fs = require('fs');

// 创建可读流对象
const readable = fs.createReadStream('/path/to/file');

// 监听 data 事件获取流中的数据块
readable.on('data', (chunk) => {
  console.log(chunk.toString());
});

// 监听 end 事件表示读取完毕
readable.on('end', () => {
  console.log('读取完毕');
});

// 监听 error 事件处理读取错误
readable.on('error', (err) => {
  console.error(err);
});
// 还有监听open 和close等
```

- 所有的流都是EventEmitter的实例

在 Node.js 中，可以通过管道（pipe）操作将可读流（Readable）和可写流（Writable）连接起来，实现数据的传输。

```js
const fs = require('fs');

// 创建可读流对象
const readable = fs.createReadStream('/path/to/source');

// 创建可写流对象
const writable = fs.createWriteStream('/path/to/destination');

// 管道操作，将可读流中的数据传输到可写流中
readable.pipe(writable);

// 监听 finish 事件表示写入完毕
writable.on('finish', () => {
  console.log('写入完毕');
});

// 监听 error 事件处理写入错误
writable.on('error', (err) => {
  console.error(err);
});

```