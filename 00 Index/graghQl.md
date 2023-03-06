## 关键词

express-graghQl 、 GrachQLSchema
## 背景

为什么用？
1. 因为接口返回东西太多-字段冗余
2. 一个页面多次调用api
3. 需求改动后很难为单一的接口做精简逻辑

## 好处

- 数据整合
- 多次调用api问题
- N + 1  dataloader -- 比如10次可以查询一次
- APQ ： post请求--如何缓存  后端可以用redis控制某个字段是否缓存，和缓存时间
	- 如何缓存？第一次post，第二次发hash 后端把前端发的hash字符串--> redis取出来，
	- appllograghQl： apq
- 
## 特点

所有请求都是post
