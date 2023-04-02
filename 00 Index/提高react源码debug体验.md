## 源码调试

- -   git clone 下载 react 源码
- -   yarn build react, shared, scheduler, react-reconciler, react-dom --type=NODE
- -   cd build/node_modules/react
- -   yarn link
- -   cd build/node_modules/react-dom
- -   yarn link
- -   然后创建一个新项目，比如 mini-react
- -   在 mini-react 中执行 yarn link react react-dom 即可

**这种方法对阅读源码来说体验相当不好！！！**

## 1 方案一

