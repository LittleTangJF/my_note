[原理](https://juejin.cn/post/6844904046294204429)
## 搭建流程


webpack运行流程是一个串行的过程，从启动到结束会依次执行以下流程

- -   `初始化参数`：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数
- -   `开始编译`：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译
- -   `确定入口`：根据配置中的 entry 找出所有的入口文件
- -   `编译模块`：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理
- -   `完成模块编译`：在经过第4步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系
- -   `输出资源`：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会
- -   `输出完成`：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统

在以上过程中，`Webpack` 会在特定的时间点广播出特定的事件，插件在监听到感兴趣的事件后会执行特定的逻辑，并且插件可以调用 Webpack 提供的 API 改变 Webpack 的运行结果。

## 分包策略

处理第三方库有多种方式，externals、CommonsChunkPlugin、splitChunks、DllPlugin/DLLReferencePlugin 。我们先说说各种的优劣势

-  externals： 操作不是很灵活，需要设置多步，并且会出现意想不到的情况。
-  splitChunks： 使用SplitChunksPlugin是Webpack 4的默认行为
-  DllPlugin/DLLReferencePlugin： 这个依赖库不会跟着你的业务代码一起被 重新打包，只有当依赖自身发生版本变化时才会重新打包。会有一些bug但是我在操作的时候遇到一个很奇葩的坑，element-ui被dllPlugins之后，el-table不生效，是的不生效，页面也么有报错，样式都还存在，但是就是页面展示不出来table。
### splitChunks
[地址](https://juejin.cn/post/6844904195737255943)
- all ： 两个包含
- async： 只抽离属于动态引入的文件。（异步）
- initial：只从入口模块进行拆分（同步）
## source map## 是什么？生产环境怎么用？

`source map` 是将编译、打包、压缩后的代码映射回源代码的过程。打包压缩后的代码不具备良好的可读性，想要调试源码就需要 soucre map。

## 文件监听原理呢？

发现源码发生变化时，自动重新构建出新的输出文件。

Webpack开启监听模式，有两种方式：

-   启动 webpack 命令时，带上 --watch 参数

## 说一下 Webpack 的热更新原理吧

关键： Hot Module Replacement 、 WDS 、 Websocket

1. 本地资源变化，WDS向浏览器推送更新
2. 客户端对比差异，想WDS发送ajax请求获取文件内容
3. 继续发起jsonp请求该chunk的增量更新
4. 接下来就是Hot Module plugin来处理给更新
5. 
## 文件指纹是什么？怎么用？

-   `Hash`：和整个项目的构建相关，只要项目文件有修改，整个项目构建的 hash 值就会更改
    
-   `Chunkhash`：和 Webpack 打包的 chunk 有关，不同的 entry 会生出不同的 chunkhash
    
-   `Contenthash`：根据文件内容来定义 hash，文件内容不变，则 contenthash 不变

## 是否写过Plugin？简单描述一下编写Plugin的思路？

webpack在运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在特定的阶段钩入想要添加的自定义功能。Webpack 的 Tapable 事件流机制保证了插件的有序性，使得整个系统扩展性良好。

## 是否写过Loader？简单描述一下编写loader的思路？

Loader 支持链式调用，所以开发上需要严格遵循“单一职责”，每个 Loader 只负责自己需要负责的事情。

1.  创建Loader文件：创建一个新的JavaScript文件，并导出一个函数。这个函数接收一个参数，即要转换的源代码内容。在函数内部，可以对源代码进行各种处理和转换，例如解析CSS文件、压缩代码、转换图片等。
2. 返回结果：Loader函数必须返回一个JavaScript字符串或一个JavaScript对象。返回的结果将被Webpack继续处理和打包。例如，如果编写的Loader用于处理CSS文件，则需要返回一个包含CSS样式的JavaScript字符串

## 聊一聊Babel原理吧

大多数JavaScript Parser遵循 `estree` 规范，Babel 最初基于 `acorn` 项目(轻量级现代 JavaScript 解析器) Babel大概分为三大部分：

-   解析：将代码转换成 AST
    -   词法分析：将代码(字符串)分割为token流，即语法单元成的数组
    -   语法分析：分析token流(上面生成的数组)并生成 AST
-   转换：访问 AST 的节点进行变换操作生产新的 AST
    -   [Taro](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2FNervJS%2Ftaro%2Fblob%2Fmaster%2Fpackages%2Ftaro-transformer-wx%2Fsrc%2Findex.ts%23L15 "https://github.com/NervJS/taro/blob/master/packages/taro-transformer-wx/src/index.ts#L15")就是利用 babel 完成的小程序语法转换
-   生成：以新的 AST 为基础生成代码


## webpack5

