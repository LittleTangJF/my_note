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

### 4.1 本地bin寻址

我们知道，如果一个包配置了 bin后，当它被安装的时候，在项目的 node_modules/.bin下就会有相应的指令，方便执行。
npx xxx执行过程
- 先在当前目录下找有没有xxx
- 当前目录下node_modules里有没有
- 没有看系统$PATH里有没有 xxx
- 如果没有则从npm仓库安装这个xxx，过后卸载
该依赖包会被存放在 `D:\node\node_cache\_npx` 目录下，当 `npx` 命令执行完完成之后,包就会自动删除了

```JS
npm bin // 获取bin目录
npm config get prefix // 获取当前的node目录
```

## 5.指令

```js
// 查看项目依赖指令
npm list --depth=0
// 查看某个依赖
npm list name --depth=0
// 查看全局依赖
npm list --depth=0 --global 
yarn global list --depth=0
```