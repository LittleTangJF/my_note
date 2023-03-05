## 关键词

pre-commit 、commit-msg  post-commit 、pre-push  ；[lint-staged](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fokonet%2Flint-staged "https://github.com/okonet/lint-staged")

pre-commit：代码进行检查、优化代码格式、或者对提交的图片进行压缩等等任务。
## lint-staged

- pre-commit会执行lint-staged命令，对本次commited中所有js css文件执行 `exlint --fix` 、 `stylelint --fix` 和 `git add`
- `prettier` 代码格式优化
