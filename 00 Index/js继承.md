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
            Children.prototype = new Parent();
```
## 原型式继承（用得少）


## 寄生式继承
```js
function createObje(obj) {
                let clone = Object.assign(obj); //接受到对象后，原封不动的创建一个新对象
                clone.prototype1 = "我是新增的prototype1"; //在新对象上新增属性，这就是所谓的寄生
                return clone; //返回新对象
            }
        // 和原型链继承一样，parent中的引用属性，会被所有示例共享
```
## 寄生组合式继承
优点：和组合继承一样，只不过没有组合继承的调用两次父类构造函数的缺点

```js
// 寄生
function inherProto(superType, subType) {
                //拷贝一个超类的原型副本
                let proto = {
                    ...superType.prototype
                };
                //将原型的超类副本作为子类的原型对象，也就是第一种中的原型链继承方式，只不过继承的是超类原型的副本
                subType.prototype = proto;
                //这一步比较迷，官方的说法是，我们在拷贝超类的原型的时候，拷贝的proto对象，将会丢失默认自己的构造函数，也就是superType，
                //所以我们这里将它的构造函数补全为subType。貌似不做这一步也没啥问题，但是缺了点东西可能会有其他的副作用，所以还是补上
                proto.constructor = subType;
            }
             function Sub() {
                this.subProto = "sub proto";
                this.name = "sub name";
                //这里还是借用构造函数的套路
                Super.call(this);
            }
            Super.prototype.getName = function () {
                console.log(this.name);
            }
        //省略了Children.prototype = new Parent();
```