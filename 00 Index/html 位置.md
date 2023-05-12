在 HTML 中，每个元素都有位置属性，它们定义了元素的位置。位置属性通常包括以下几种：

1. offsetParent：返回元素最近的祖先`定位元素`，如果没有则是` body` 元素。
2. offsetTop/offsetLeft：返回元素与其 `offsetParent` 元素之间的上/左边距离。
3. offsetWidth/offsetHeight：返回`元素`的宽度/高度，包括`边框和内边距`。
4. clientTop/clientLeft：返回元素的上/左`边框`宽度。
5. clientWidth/clientHeight：返回元素的内部宽度/高度，`不包括边框和滚动条`。
6. scrollWidth/scrollHeight：返回元素内容的`总宽度/高度`，包括被`隐藏的部分和内边距`。
7. scrollTop/scrollLeft：返回元素在垂直/水平方向`滚动`的像素数。

以上是 DOM 中位置属性的基本用法，可以通过它们获取元素的位置信息，用于实现一些交互效果或者布局计算等功能。

[codesendbox实现链接](https://codesandbox.io/s/htmlwei-zhi-7qu39c?file=/index.html)

## 应用场景

比如在使用懒加载时用到 [[面试技术难点]]

方案一：位置计算 + 滚动scroll + dataset
公式：scrollHeight-scrollTop-offsetHeight< y

[参考链接](https://juejin.cn/post/6844903488124633096)