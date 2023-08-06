[参考链接](https://github1s.com/sindresorhus/p-limit/blob/HEAD/index.js)

## 使用方式

```js
import pLimit from 'p-limit';

const limit = pLimit(1);

const input = [
	limit(() => fetchSomething('foo')),
	limit(() => fetchSomething('bar')),
	limit(() => doSomething())
];

// Only one promise is run at once
const result = await Promise.all(input);
console.log(result);
```

### 源码用到的知识点

1. Number.isInteger：用于检查给定的值是否为整数
2. Number.POSITIVE_INFINITY：表示正无穷大