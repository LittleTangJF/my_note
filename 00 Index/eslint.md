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
```