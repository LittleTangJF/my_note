## 1 安装插件

eslint

## 2 配置

```js
// setting.json
  // 自动格式化
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        "typescriptreact",
        "html",
    ],
```

## 2 fix错误

git 提交时自动启动 eslint --fix

```js
`eslint src/. --ext .js,.jsx,.tsx,.ts --fix --quiet`
// --fix : 该选项指示 ESLint 试图修复尽可能多的问题。修复只针对实际文件本身，而且剩下的未修复的问题才会输出。
// `--quiet`：该选项允许你禁止报告警告。如果开启这个选项，ESLint 只会报告错误。
```

### 3 配置eslint

```js
node_module/.bin/eslint --init

"env": {

"browser": true,

"es2021": true

},

"extends": [

"plugin:react/recommended",

"airbnb"

],

"parser": "@typescript-eslint/parser",

"parserOptions": {

"ecmaFeatures": {

"jsx": true

},

"ecmaVersion": 12,

"sourceType": "module"

},

"plugins": [

"react",

"@typescript-eslint"
```

## 4 解决eslint报错问题

```js
export NODE_OPTIONS=--max_old_space_size=4096

```javascript
--max-old-space-size=1024 index.js #increase to 1gb
--max-old-space-size=2048 index.js #increase to 2gb
--max-old-space-size=3072 index.js #increase to 3gb
--max-old-space-size=4096 index.js #increase to 4gb
--max-old-space-size=5120 index.js #increase to 5gb
--max-old-space-size=6144 index.js #increase to 6gb
--max-old-space-size=7168 index.js #increase to 7gb
--max-old-space-size=8192 index.js #increase to 8gb
```
```