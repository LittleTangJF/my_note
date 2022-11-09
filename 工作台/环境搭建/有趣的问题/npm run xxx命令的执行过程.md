## Taro

**以taro为例**
1. npm run taro中的taro可以在node_modules/.bin文件中可以找到
2. 而node_modules/.bin会被临时加入系统的环境变量里面，所以可以直接运行taro
3. 在控制套利用ls -l 可以看到，.bin文件夹内的都是软连接，指向的地方是上级目录node_modules下的依赖
4. 找到对应依赖目录，可以看到里面的运行代码
![[Pasted image 20221109144549.png]]

## 总结

-   执行`npm run xxx`时，会先从当前目录下的`node_modules/.bin`中去查找对应的可执行程序执行；
-   如果无法找到，就会在npm的全局安装路径进行查找，也就是`npm i -g xxx`时安装的路径；
-   如果还找不到，就会从系统环境变量中查找；
-   再找不到就会报错了；

## 关联知识点

node - [[process.argv]]