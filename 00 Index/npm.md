## 关键词

npx、registry、扁平结构、缓存

## 1.npm install原理

- 是否存在于lock文件，没有就获取包信息
- 对比lock是否冲突（版本），冲突也获取包信息
- 获取包信息后，构建依赖树---扁平化
- 查看本地缓存---有的话直接解压到node_modules--生成package-lock
- 本地无缓存，下载包
- 压缩包后添加到缓存
- 解压到node_modules---生成package-lock

## 2.扁平结构化

- 如果存在依赖一样
- 检查依赖版本允许范围，得到一个兼容版本，将冗余模块清理

## 3.缓存

- 检查本地中是否存在缓存,如果是直接将缓存解压到 `node_modules` 目录下,如果不存在则通过网络去下载包
```js
// 查看缓存目录
npm config get cache
// /Users/tking/.npm
// content-v2 存放的二进制解压后是我们的依赖包
```

## 4.npx

