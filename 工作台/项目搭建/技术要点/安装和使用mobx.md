## 引入

```js
import { action, computed, makeObservable, observable, runInAction } from 'mobx'
import { observer } from 'mobx-react'
```

## 关键词

1. action: 修改状态 唯一修改state的东西
2. computed: 使用pure function从state中推导出的值
3. makeObservable:
4. observable: 将一个普通的值转换成可观察的
5. runInAction: 异步的情况下，修改数据要使用它，放在它的回调里面
6. mobx-react: 负责自动监听store和取消监听store的变化