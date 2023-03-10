## 关键词

ReactElement、createElement、Component、词法分析、语法分析

## [如何转换的呢？](https://juejin.cn/post/7186132321219641400)

Babel 只负责串起整个流程，具体的编译交给 Babel 插件完成，核心的编译和生成 generator 的流程也能通过插件的方式进行扩展。
### 三个阶段

- parse：通过parse把源代码转成AST
	- 词法分析
	- 语法分析
- transform：通过遍历AST，调用各种插件对其优化-语法转换、代码优化等，生成新的AST
	- 插件
- generate：把转换后的AST打印成目标代码，并生成sourcemap


## 词法分析

```js
[ { "type": "Keyword", "value": "let" },]
```


## 语法分析
上一步的 token 数据进行递归的组装,生成 AST

```js
{
  "type": "Program",
  "body": [
    {
      "type": "VariableDeclaration",
      "declarations": [
        {
          "type": "VariableDeclarator",
          "id": {
            "type": "Identifier",
            "name": "name"
          },
          "init": {
            "type": "Literal",
            "value": "ljc",
            "raw": "\"ljc\""
          }
        }
      ],
      "kind": "let"
    }
  ],
  "sourceType": "module"
}
```

## 最总转换结果

### [在V16版本](https://juejin.cn/post/6844904131124002829#heading-1)

解析成`React.createElement`进行包裹
- 基于createElement把传递的参数处理为React虚拟Dom对象
- render把React虚拟Dom对象按照动态创建dom元素的方式插入到指定的容器中
```JS
// node： React组件  mountNode： 要挂载的DOM对象
ReactDOM.render(node, mountNode);
```
### 在V17版本

`jsx`的转换用`react/jsx-runtime`