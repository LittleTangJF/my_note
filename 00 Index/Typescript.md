## 关键词


关键字、映射类型、 范型


## 一、类型

### 1.1 基础类型

#### 1.1.1 元组Tuple

```ts
[string, number]
```

#### 1.1.2 枚举

#### 1.1.3 never


`never`类型表示的是那些永不存在的值的类型。

- 表示函数**永远不会正常返回**，即函数执行期间抛出了异常或者无限循环等；例如：抛出错误的函数没有返回值‘

```ts
function throwError(message: string): never {
  throw new Error(message);
}
```

- 用来标识一个函数永远不会结束
```ts
function infiniteLoop(): never {
  while (true) {}
}
```
`any`也不可以赋值给`never`

### 1.2 映射类型

 #### 1.2.1 Record

	把K的属性赋值给类型T，并返回新的类型

```ts
type Record<K extends keyof any, T> = { [P in K]: T; };
type proxyKType = Record<K,T> // K 可以是联合类型 枚举类型 
```

#### 1.2.2 Partial

	将类型定义的所有属性都修改为可选。

```ts
type Coord = Partial<Record<'x' | 'y', number>>;

// 等同于
type Coord = {
	x?: number;
	y?: number;
}
```

#### 1.2.3 Pick

	从类型定义的属性中，选取指定一组属性，返回一个新的类型定义。

```ts
type Coord = Record<'x' | 'y', number>;
type CoordX = Pick<Coord, 'x'>;

// 等用于
type CoordX = {
	x: number;
}
```


## 二、关键字


### 2.1 as

	断言

### 2.2 typeof

### 2.3 instanceof



## 三、范型


以下是范型的几个使用场景

### 3.1 范型变量

```ts
let output3: number = identityVar<number>(100);
```

### 3.2 范型函数

```ts
function identityFn<T>(arg: T): T { return arg; }
```

### 3.3 范型接口

```ts
// 泛型接口 
interface GenericIdentityFn<T> { (arg: T): T; }
```

### 3.4 范型类

```ts
// 泛型类 
class GenericNumber<T> { zeroValue: T; add: (x: T, y: T) => T; }
```

## 四、接口

常见的属性有可选` ？`  只读 `readonly`  

### 4.2 额外检查

```ts
interface SquareConfig {
    color?: string;
    width?: number;
    [propName: string]: any;
}
```

### 4.3 函数类型

```ts
interface SearchFunc {
  (source: string, subString: string): boolean;
}
```

### 4.4 可索引类型

```ts
interface StringArray {
  [index: number]: string;
}

let myArray: StringArray;
myArray = ["Bob", "Fred"];

let myStr: string = myArray[0];
```

### 4.5 类类型

### 4.6 继承接口

- extends

## 五、函数

### 5.1 函数重载


为同一个函数提供多个函数类型定义来进行函数重载

```ts
let suits = ["hearts", "spades", "clubs", "diamonds"];

function pickCard(x: {suit: string; card: number; }[]): number;
function pickCard(x: number): {suit: string; card: number; };
function pickCard(x): any {
    // Check to see if we're working with an object/array
    // if so, they gave us the deck and we'll pick the card
    if (typeof x == "object") {
        let pickedCard = Math.floor(Math.random() * x.length);
        return pickedCard;
    }
    // Otherwise just let them pick the card
    else if (typeof x == "number") {
        let pickedSuit = Math.floor(x / 13);
        return { suit: suits[pickedSuit], card: x % 13 };
    }
}

let myDeck = [{ suit: "diamonds", card: 2 }, { suit: "spades", card: 10 }, { suit: "hearts", card: 4 }];
let pickedCard1 = myDeck[pickCard(myDeck)];
alert("card: " + pickedCard1.card + " of " + pickedCard1.suit);

let pickedCard2 = pickCard(15);
alert("card: " + pickedCard2.card + " of " + pickedCard2.suit);
```

## 六、命名空间

记录它们类型的同时还不用担心与其它对象产生命名冲突。 因此，我们把验证器包裹到一个命名空间内，而不是把它们放在全局命名空间下

- namespace

## 七、声明合并

接口合并、命名空间合并

```ts
interface Box {
    height: number;
    width: number;
}

interface Box {
    scale: number;
}

let box: Box = {height: 5, width: 6, scale: 10};
```

## 八、装饰器

_装饰器_是一种特殊类型的声明，它能够被附加到[类声明](https://www.tslang.cn/docs/handbook/decorators.html#class-decorators)，[方法](https://www.tslang.cn/docs/handbook/decorators.html#method-decorators)， [访问符](https://www.tslang.cn/docs/handbook/decorators.html#accessor-decorators)，[属性](https://www.tslang.cn/docs/handbook/decorators.html#property-decorators)或[参数](https://www.tslang.cn/docs/handbook/decorators.html#parameter-decorators)上。 装饰器使用 `@expression`这种形式，`expression`求值后必须为一个函数，它会在运行时被调用，被装饰的声明信息做为参数传入。

[ts-装饰器](https://codesandbox.io/s/ts-zhuang-shi-qi-7fsub8?file=/src/index.ts)

## 总结

[[typescript总结]]


## 常见问题


- [[type和interface]]
- [[declare]]