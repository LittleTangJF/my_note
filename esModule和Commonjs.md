## 关键词

export import、exports require、as

## 1 导入导出

-   `CommonJS`导入导出
    -   `require`
    -   `module.exports`
    -   `exports`
-   `ES Module`导入导出
    -   `import`
    -   `export`
    -   `export default`

## 2 ESM

- esModule是**编译**的时候运行
- esModule输出值的引用
	- 修改值后会发生改变（不会缓存，所以只要改了值就变化）
- export default会不一样
	- 赋值给 `default` 之后，只读引用与 `default` 关联，此时原变量 `name` 的任何修改都与 `default` 无关

## 3 commonjs

- commonJs是**被加载**的时候运行
- commonJs输出的是值的拷贝（简单类型和复杂类型有区别）
- commentJs具有缓存（以后都是从内存取）
	- 在第一次被加载时，会完整运行整个文件并输出一个对象，拷贝（浅拷贝）在内存中。下次加载文件时，直接从内存中取值