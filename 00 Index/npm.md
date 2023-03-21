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

## 6.重要创建命令

npx xxx 和 npm init 和 yarn create 和npm create

### 6.1 npx xxx 

同4

### 6.2 npm init 和 npm create

用 `create-*` 包快速创建项目。和 `yarn create` 的作用和操作完全一样

```js
`npm init react-app my-app` 等同于 `yarn create react-app my-app`
```

### 6.3 yarn create

用 `create-*` 的包快速创建项目。

使用方式 `yarn create <starter-kit-package> [<args>]`

`yarn create react-app my-app` 和下面的脚本等价

```JS
$ yarn global add create-react-app
$ create-react-app my-app
```

## 7 遇到问题

### 7.1 某个版本依赖引入不同版本问题

在默认安装**peerDependencies**。

在很多情况下，这会导致版本冲突，从而[中断](https://so.csdn.net/so/search?q=%E4%B8%AD%E6%96%AD&spm=1001.2101.3001.7020)安装过程。

```js
npm install --legacy-peer-deps // 忽略目的是**绕过peerDependency自动安装**；它告诉NPM 忽略项目中引入的各个modules之间的相同modules但不同版本的问题并继续安装，保证各个引入的依赖之间对自身所使用的不同版本modules共存。
```