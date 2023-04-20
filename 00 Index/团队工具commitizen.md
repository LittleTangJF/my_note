## 1 安装和使用


```js
npm install -g commitizen
```

将以下配置添加进package.json

```js
  "config": {
    "commitizen": {
      "path": "node_modules/cz-customizable"
    }
  }
```

**项目根目录创建 _.cz-config.js_ 自定义提示文件**

```js
module.exports = {
  types: [
    {
      value: 'wip',
      name: '🚧wip:          进行中...',
    },
    {
      value: 'feat',
      name: '🎉feat:         新增功能',
    },
    {
      value: 'fix',
      name: '🐛fix:          修复BUG',
    },
    {
      value: 'merge',
      name: '🐛merge:        合并代码',
    },
    {
      value: 'style',
      name: '🎨style:        修改代码格式',
    },
    {
      value: 'ci',
      name: '👷‍ci:           修改持续化集成配置',
    },
    {
      value: 'refactor',
      name: '👍refactor:     代码重构',
    },
    {
      value: 'improvement',
      name: '🚀improvement:  提升性能',
    },
    {
      value: 'docs',
      name: '📓docs:         修改文档',
    },
    {
      value: 'test',
      name: '✅test:         修改测试用例',
    },
    {
      value: 'build',
      name: '🔨build:        变更项目构建或外部依赖',
    },
    {
      value: 'revert',
      name: '⏪revert:       版本回退',
    },
    {
      value: 'chore',
      name: '💩chore:        杂项',
    },
  ],
  scopes: [
    { name: 'global' },
    { name: 'datasets' },
    { name: 'virtual datasets' },
    { name: 'manual mlops' },
    { name: 'visual list' },
    { name: 'datapools' },
    { name: 'dataconnectors' },
    { name: 'datasources' },
    { name: 'etl' },
    { name: 'queriers' },
    { name: 'data modeling' },
    { name: 'visual list' },
    { name: 'visual chart' },
    { name: 'scene' },
    { name: 'projects' },
    { name: 'products' },
    { name: 'services' },
    { name: 'label template' },
    { name: 'product template' },
    { name: 'components' },
    { name: 'overview' },
    { name: 'config' },
    { name: 'plugins' },
    { name: 'api' },
    { name: 'other' },
  ],
  allowTicketNumber: false,
  isTicketNumberRequired: false,
  ticketNumberPrefix: 'TICKET-',
  ticketNumberRegExp: '\\d{1,5}',
  messages: {
    type: '(必填)选择您要提交的更改类型:',
    scope: '(必填)更改的范围:',
    // used if allowCustomScopes is true
    customScope: '(必填)更改的范围:\n',
    subject: '(必填)撰写简短的变更描述:\n',
    body: '(选填)撰写更改的详细描述, 使用"|"换行:\n',
    breaking: '(选填)不兼容变动:\n',
    footer: '(选填)要关闭的issue列表, 例: #31, #34:\n',
    confirmCommit: '🚨确认以上Commit-Message',
  },
  allowCustomScopes: false,
  allowBreakingChanges: ['feat', 'fix'],
  subjectLimit: 100,
};
```

**使用 _git cz_ 代替 _git commit_**

>使用git cz 代替 git [commit](https://so.csdn.net/so/search?q=commit&spm=1001.2101.3001.7020),即可看到提示内容
