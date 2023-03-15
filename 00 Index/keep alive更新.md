

## 如何更新？


activated或者beforeRouteEnter

```JS

activated(){
   this.getData() // 获取数据
}


beforeRouteEnter(to, from, next){
  next(vm=>{
    console.log(vm)
    // 每次进入路由执行
    vm.getData()  // 获取数据
  })
}
```