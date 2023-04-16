**ASCII 码是一种将字符映射为数字的编码方式，其中包括了 0-9 数字、大小写字母、标点符号以及一些特殊字符，总共 128 个字符。

## 简介

在 ASCII 码中，每个字符对应一个唯一的数字，也就是一个 7 位的二进制数，因为 7 位二进制数最多可以表示 2^7=128 种不同的组合，刚好可以对应 ASCII 码中的每一个字符。对于 26 个英文字母，它们在 ASCII 码表中的对应数字分别是 65-90 和 97-122，可以使用以下的 JavaScript 代码输出它们在 ASCII 码中对应的二进制数：


```js
for (let i = 65; i <= 90; i++) {
  console.log(`${String.fromCharCode(i)}: ${i.toString(2)}`);
}

for (let i = 97; i <= 122; i++) {
  console.log(`${String.fromCharCode(i)}: ${i.toString(2)}`);
}

```


- HEX: 十六进制
- DEC：十进制
- OCT： 八进制
- BIN：二进制