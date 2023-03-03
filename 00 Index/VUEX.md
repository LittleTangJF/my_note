## 关键词
state、mutations、getters、actions、module、store.commit、store.dispatch

## 定义

Vuex是集中管理项目公共数据的。Vuex 有state、mutations 、getters、actions、module属性。

-  state 属性用来存储公共管理的数据
-  mutations 属性定义改变state中数据的方法，
- getters 属性可以认为是定义 store 的计算属性。
- Action 提交的是 mutation，而不是直接变更状态。Action 可以包含任意异步操作。
- moudle属性是将store分割成模块。
- 可以使用mapState、mapMutations、mapAction、mapGetters一次性获取每个属性下对应的多个方法。
  