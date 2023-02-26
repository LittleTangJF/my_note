## 关键词

原型链继承、借用构造函数继承、组合继承、原型式继承、寄生式继承、寄生组合式继承

## 原型链继承

```JS
Children.prototype = new Parent();
// 缺点：Parent 中的引用属性会被每个子类示例共享
```

## 借用构造函数继承

```JS
function Children() {
               Parent.call(this);
         }
     // 优点 避免了子类实例共享引用属性
 //  //缺点 此时Parent()会再次创建一个fn函数，这个是没有必要的
```
## 组合继承（原型+构造）

避免了子类共享引用属性同时避免了父类构造函数重复对function属性的创建
```JS
 //Parent中的方法，在原型上定义
            Parent.prototype.pFn = function () {
                console.log('我是Parent中的方法');
            }

            function Children() {
                //Parent中的属性仍然在构造函数中继承
                Parent.call(this);
            }
```
## 原型式继承

