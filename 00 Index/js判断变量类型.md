## 关键技术

typeof、instanceof、Object.prototype.toString.call()、 constructor (用于引用数据类型)

## 注意

- typeof（null和array返回的是“object”、NaN返回的是“number”）
- Object.prototype.toString 表示一个返回对象类型的字符串，call()方法可以改变this的指向
- constructor,除了undefined和null，其他类型的变量均能使用constructor判断出类型.
-  instanceof只能检测引用数据类型

### 注意

- 最好是用 `typeof` 来判断基本数据类型（包括`symbol`），避免对 null 的判断。
- `instanceof` 也可以判断一个实例是否是其父类型或者祖先类型的实例。

- [[判断空对象]]