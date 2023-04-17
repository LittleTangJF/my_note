
fs模块可以用于操作系统文件，fs模块的API都分为同步和异步的(带`Sync`后缀的是同步), 而异步的回调函数的参数node统一约定了**第一个参数为错误对象**

 - read、write
 - append
 - unlink
 - rmdir
 - copy

### 3.1 [[stream]]

流： 创建可读流fs.createWriteStream:根据给定的路径创建一个**可写流**对象并返回；
创建可写流：fs.createWriteStream
- on: 监听open、write、end、close
- pipe：可以直接将可读流读取的内容输入到指定的可写流中