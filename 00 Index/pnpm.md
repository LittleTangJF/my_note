## 关键词

扁平化问题、软链接、硬链接和符号链接

## 1. npm存在问题




- 1.  模块可以访问没有声明依赖的包
- 1.  扁平化一个依赖树的算法非常复杂（耗时）
- 1.  在项目的中有一些包被重复安装（版本不同）


## 2. pnpm如何解决

比如安装express， 只是一个`符号链接`，而依赖包的真正位置，在`.pnpm`目录下

## 3. 优势

-   npm/yarn在不同项目依赖同一个包的情况下，会将这个包安装多次在每个项目中，而pnpm安装的包会存储在可寻址的磁盘中，在多个项目同时引用时，只需要用一个硬链接指向该地址就可以使用，大大节约了磁盘空间
- 当依赖了同一个包的不同版本时，只对变更的文件进行更新，不需要重复下载没有变更的部分
- -   算法比 npm/yarn 的扁平化算法简单很多，节省时间