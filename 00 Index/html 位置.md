在 HTML 中，每个元素都有位置属性，它们定义了元素的位置。位置属性通常包括以下几种：

1. offsetParent：返回元素最近的祖先定位元素，如果没有则是 body 元素。
2. offsetTop/offsetLeft：返回元素与其 offsetParent 元素之间的上/左边距离。
3. offsetWidth/offsetHeight：返回元素的宽度/高度，包括边框和内边距。
4. clientTop/clientLeft：返回元素的上/左边框宽度。
5. clientWidth/clientHeight：返回元素的内部宽度/高度，不包括边框和滚动条。
6. scrollWidth/scrollHeight：返回元素内容的总宽度/高度，包括被隐藏的部分和内边距。
7. scrollTop/scrollLeft：返回元素在垂直/水平方向滚动的像素数。

以上是 DOM 中位置属性的基本用法，可以通过它们获取元素的位置信息，用于实现一些交互效果或者布局计算等功能。