这是一个flex的巩固学习、补充 [练习地址](https://codesandbox.io/s/flex-learning-vzlj9l)
## 考点一 flex：1 


```js
// flex: 1; === flex: 1 1 0%;
// 第一个参数： flex-grow 定义了项目的放大比例，默认值：0，含义是即使有剩余空间，也不放大
// 第二个参数：flex-shrink 定义了缩小比例，默认值是 1，含义是如果空间不足，改盒子将缩小
// 第三个参数：flex-basis 給上面两个属性分配多余空间之前，计算项目是否有多余空间，默认是：auto，含义是本身盒子大小
```
### 1、flex-grow

定义了项目的放大比例，默认值：0 表示：即使有剩余空间，也不放大
```js
// 计算公式
项目宽度 = (( flex-grow / flex-grow 总个数) * 可用空间）+ 初始项目宽度
```

###  2、flex-shrink

定义了缩小比例，默认值是 1，含义是如果空间不足(小于视窗的宽度)，改盒子将缩小 到跟视窗一样的宽度
```js
// 在视口宽度大于300px时，宽度为300px，少于 300px，该项目的宽度就被压缩成跟视口一样的宽度
```

### 3、flex-basis

flex-basis 可以设置和height和width一样的值， 默认值是auto，即本身盒子大小

## 各参数代表含义

### flex： 1
```css
div{
   flex-grow: 1;
   flex-shrink: 1;
   flex-basis: 0%;
}
```

### flex: auto

```css
div{
   flex-grow: 1;
   flex-shrink: 1;
   flex-basis: auto;
}

```

### 两个长度 flex: 1 1;

```css
div{
   flex-grow: 1;
   flex-shrink: 1;
   flex-basis: 0;
}

```

### 一个宽度 flex:  100px;

```css
div{
   flex-grow: 1;
   flex-shrink: 1;
   flex-basis: 100px;
}

```

### 