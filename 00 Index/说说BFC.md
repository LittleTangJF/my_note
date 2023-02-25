## 定义

块级格式化上下文，独立渲染的区域，不会影响到边界外的元素

## 形成条件

- float
- position：absolute fixed
- overflow： 不为visible
- display：inline-block table-cell table-caption flex 

## 解决问题

- 父元素高度坍塌
- 解决外边距合并问题
- 浮动元素重叠


