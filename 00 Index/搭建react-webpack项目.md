## 1.搭建方式

- 官方cra+w
- 自定义
- 第三方cli

## 2.自定义搭建
[地址](https://github.com/LittleTangJF/react-webpack-custom)
### 2.1 安装webpack

```JS
// webpack-cli 用于在命令行运行webpack
yarn add webpack webpack-cli -D
```

### 2.2 安装html-plugin

```js
// 生成html5文件，在body中使用script标签引入你生成的bundle
yarn add html-webpack-plugin -D
```
### 2.3 清理打包文件
```js
yarn add clean-webpack-plugin -D
```

### 2.4 配置css less

```js
yarn add style-loader css-loader less less-loader -D
```

### 2.5 自动添加前缀

```js
yarn add postcss-loader autoprefixer -D
```

### 2.6 css提取到单独的文件

```js
yarn add mini-css-extract-plugin -D

```

### 2.7 配置多环境
```js
yarn add webpack-merge -D // 合并webpack config
```

#### 2.7.0 dev环境

```js
devtool : 'inline-source-map' // 生成 source map
devServer: {...}
yarn add webpack-dev-server -D
```

#### 2.7.1 正式环境

```js
yarn add css-minimizer-webpack-plugin -D //压缩css
```

### 2.8 react依赖

```js
yarn add react react-dom react-router-dom
```

### 2.9 安装babel

```js
yarn add @babel/core @babel/preset-env @babel/preset-react @babel/polyfill babel-loader -D
```

- `babel-loader`是webpack和Babel之间的桥梁，它将Babel与webpack集成。
- `@babel/core`是Babel的核心库。
- `@babel/preset-env`和`@babel/preset-react`是预设，用于指定Babel要如何转换代码

### 3.0 配置别名

### 3.1 分包splitChunks

### 3.2 压缩Image

```js
const ImageminPlugin = require('imagemin-webpack-plugin').default;
```

### 3.3 代码质量

```js
npm install eslint eslint-config-prettier eslint-plugin-prettier prettier -D
```

- 新建`.eslintrc.js`文件
- .prettierrc.js

### 3.4 提交前校验lint-staged

```js
npx mrm lint-staged
"lint-staged": { "*.{js,jsx,ts,tsx}": "eslint --fix" }
```

### 3.5 配置typescript

```js
yarn add typescript @babel/preset-typescript @types/react @types/react-dom -D
```
- 添加`tsconfig.json`文件