1. 存储用户日志
2. request请求封装，对不常数据变更的接口进行缓存
3. 大文件切片上传，分片，避免网络失败，刷新页面等导致中断的问题
	1.文件切片后存储到indexDB库，动态更新上传状态，异常情况可取出再继续定位到未上传的的切片继续上传


[参考链接](https://juejin.cn/post/7239259798267904059?searchId=202310261216586F45149D1F2ADA6E07C7)