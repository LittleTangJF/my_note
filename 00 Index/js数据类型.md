## 基本类型

Number 、String、Boolean、BigInt、Symbol、Null、Undefined。
- Symbol(key)： 特点就是没有重复的数据；使用Symbol数据作为key不能使用for获取到这个key，需要使用Object.getOwnPropertySymbols(obj)获得这个obj对象中key
- BigInt(n)：特点就是数据涵盖的范围大 ，后面有个n代表它是BigInt类型  typeof 1n === 'bigint' 
## 引用类型

Object
- 对象
- 数组
- 正则
- 日期
- Math
- 