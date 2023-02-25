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

## 引出问题

### 为什么margin会重叠？

产生条件
1. 处于常规文本流的块级盒子
2. 没有padding和border讲他们隔开
3. 垂直方向相邻的外边距
场景
1. 相邻兄弟元素

