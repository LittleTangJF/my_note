## 共同

标准回答 Cookie、SessionStorage、 LocalStorage都是浏览器的本地存储

## 区别

- 主体：cookie是由服务器端写入的，而SessionStorage、 LocalStorage都是由前端写入的
- 生命周期：cookie的生命周期是由服务器端在写入的时候就设置好的；LocalStorage是写入就一直存在，除非手动清除；SessionStorage是页面关闭的时候就会自动清除。
- 存储大小：cookie的存储空间比较小大概4KB，SessionStorage、 LocalStorage存储空间比较大，大概5M
- 数据共享：遵循同源原则，但SessionStorage还限制必须是同一个页面
- 发送是否携带：在前端给后端发送请求的时候会自动携带Cookie中的数据，但是SessionStorage、 LocalStorage不会
## 应用场景

- cookie：储登录验证信息SessionID或者token
- LocalStorage常用于存储不易变动的数据，减轻服务器的压力
- SessionStorage可以用来检测用户是否是刷新进入页面，如音乐播放器恢复播放进度条的功能。

## 关联问题

## 如何实现可过期的localstorage数据？

## 实现原理

- 惰性删除： 某个键值过期后；不会被马上删除；等到下次被使用的时候被检查到过期删除
- 定时删除：每隔一段时间执行一次删除操作