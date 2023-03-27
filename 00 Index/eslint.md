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