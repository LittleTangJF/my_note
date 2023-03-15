## 关键词

矢量图形  XML


## 定义

SVG是一种图形文件格式 ，用户可以直接用代码来描绘图像

```JS
<body>
    <svg version="1.1" xmlns="http://www.w3.org/2000/svg" style="height: 300px; width: 500px">
        <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />
    </svg>
</body>
```


## 引入方式

三种

```JS
<iframe src="example1.svg" style="width: 350px; height: 250px"></iframe>
<embed src="example2.svg" type="image/svg+xml" />
<object data="example3.svg" type="image/svg+xml"></object>
```


[参考文档](https://juejin.cn/post/7139099067023360037)