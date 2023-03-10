[地址](https://juejin.cn/post/7035104240217358350)

1. 在合成事件是异步的
2. 在hooks中是异步的
3. 在脱离了react掌控，是同步的，如setTimeout、Promiset.then等
![[Pasted image 20230209165704.png]]


A：默认是异步的，但有时候是同步的；在react控制内的事件处理函数onClick、onChange等合成事件，以及生命周期函数点用setState时表现为异步，react可以把多个setState合并成一次进行批量更新；在setTimeout或者原生事件中，setState是同步的（比如setTimeout/setInterval/Promise.then(fn)/fetch 回调/xhr 网络回调）。


## 如何获取最新值

- 回调中获取--参数
- useEffect ---监听
