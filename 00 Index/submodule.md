## 一、添加

// 添加到 src/submodulePath 目录，并指定分支为 dev
git submodule add -b dev git@gitlab.apulis.com.cn:groupname/reponame.git  src/submodulePath


## 二、更新

clone仓库后
```js
git submodule init
git submodule update
```


## 三、删除


```js
rm -rf 子模块目录 删除子模块目录及源码
vi .gitmodules 删除项目目录下.gitmodules文件中子模块相关条目
vi .git/config 删除配置项中子模块相关条目
rm .git/module/* 删除模块下的子模块目录，每个子模块对应一个目录，注意只删除对应的子模块目录即可
```
