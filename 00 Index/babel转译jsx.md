## 关键词

ReactElement、createElement、Component


## 在V16版本

解析成`React.createElement`进行包裹
- 基于createElement把传递的参数处理为jsx对象
- ____基于render把jsx对象按照动态创建dom元素的方式插入到指定的容器中____

## 在V17版本

`jsx`的转换用`react/jsx-runtime`