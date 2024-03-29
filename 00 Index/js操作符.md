## 关键词

_  |  ,  |  ??  |  ?.  |  #  |  >>  |  >>> | ~ |  ^  |  ~~

## 1 数值运算符 _

```js
let number = 100_0000_0000_0000 // 0太多了不用数值分割符眼睛看花了
console.log(number)             // 输出 100000000000000
```

## 2  零合并操作符 ??

解决了零合并问题，之前用的 || 不会排除 `0 '' NaN`, 而??会排除这些值，只返回 null 、 undefined两个空值

```js
let a = {b: null, c: 10}
a.b ??= 20
a.c ??= 20
console.log(a)     // 输出 { b: 20, c: 10 }
```

## 3 位运算符

- 一般我们用 `>>` 来将一个数除 2，相当于先舍弃小数位然后进行一次 `Math.floor`：
- 左移运算符 `<<` 与之类似，左移很简单左边移除最高位，低位补 0：

### 3.1 异或^

相同为 0，不同为 1, 布尔值异或会转换成 0 和 1 再计算 

## 4 双位运算符

- 可以使用双位操作符来替代正数的 `Math.floor( )`，替代负数的 `Math.ceil( )`。
```js
Math.floor(4.9) === 4      // true
// 简写为：
~~4.9 === 4      // true
```

## 总结

### 优先级
![[Pasted image 20230322112049.png]]